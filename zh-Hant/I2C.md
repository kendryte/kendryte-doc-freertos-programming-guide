# 集成電路內置匯流排 (I²C)

## 概述

I²C 匯流排用於和多個外部裝置進行通信。多個外部裝置可以共用一個 I²C 匯流排。

## 功能描述

I²C 模組具有以下功能：

- 獨立的 I²C 裝置封裝外部裝置相關參數
- 自動處理多裝置匯流排爭用
- 支持從模式

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [i2c\_get\_device](#i2cgetdevice)
- [i2c\_dev\_set\_clock\_rate](#i2cdevsetclockrate)
- [i2c\_dev\_transfer\_sequential](#i2cdevtransfersequential)
- [i2c\_config\_as\_slave](#i2cconfigasslave)
- [i2c\_slave\_set\_clock\_rate](#i2cslavesetclockrate)

### i2c\_get\_device

#### 描述

註冊並打開一個 I²C 裝置。

#### 函數原型

```c
handle_t i2c_get_device(handle_t file, const char *name, uint32_t slave_address, uint32_t address_width);
```

#### 參數

| 參數名稱          |   描述             |  輸入輸出  |
| ---------------- | ------------------ | --------- |
| file             | I²C 控制器句柄      | 輸入      |
| name             | 指定訪問該裝置的路徑 | 輸入      |
| slave\_address   | 從裝置地址          | 輸入      |
| address\_width   | 從裝置地址寬度      | 輸入      |

#### 返回值

I²C 裝置句柄。

### i2c\_dev\_set\_clock\_rate

#### 描述

配置 I²C 裝置的時脈速率。

#### 函數原型

```c
double i2c_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### 參數

| 參數名稱          |   描述        |  輸入輸出  |
| ---------------- | ------------- | --------- |
| file             | I²C 裝置句柄   | 輸入       |
| clock\_rate      | 期望的時脈速率 | 輸入       |

#### 返回值

設置後的實際速率。

### i2c\_dev\_transfer\_sequential

#### 描述

對 I²C 裝置先讀後寫。

#### 函數原型

```c
int i2c_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### 參數

| 參數名稱       |   描述         |  輸入輸出  |
| ------------- | -------------- | --------- |
| file          | I²C 裝置句柄    | 輸入      |
| write\_buffer | 源緩衝區        | 輸入      |
| write\_len    | 要寫入的位元組數   | 輸入      |
| read\_buffer  | 目標緩衝區      | 輸出      |
| read\_len     | 最多讀取的位元組數 | 輸入      |

#### 返回值

實際讀取的位元組數。

### i2c\_config\_as\_slave

#### 描述

配置 I²C 控制器為從模式。

#### 函數原型

```c
void i2c_config_as_slave(handle_t file, uint32_t slave_address, uint32_t address_width, i2c_slave_handler_t *handler);
```

#### 參數

| 參數名稱          |   描述        |  輸入輸出  |
| ---------------- | ------------- | --------- |
| file             | I²C 控制器句柄 | 輸入       |
| slave\_address   | 從裝置地址     | 輸入       |
| address\_width   | 從裝置地址寬度 | 輸入       |
| handler          | 從裝置處理程序 | 輸入       |

#### 返回值

無。

### spi\_dev\_set\_clock\_rate

#### 描述

配置 I²C 從模式的時脈速率。

#### 函數原型

```c
double i2c_slave_set_clock_rate(handle_t file, double clock_rate);
```

#### 參數

| 參數名稱          |   描述        |  輸入輸出  |
| ---------------- | ------------- | --------- |
| file             | I²C 控制器句柄 | 輸入       |
| clock\_rate      | 期望的時脈速率 | 輸入       |

#### 返回值

設置後的實際速率。

### 舉例

```c
handle_t i2c = io_open("/dev/i2c0");
/* i2c外部裝置地址是0x32, 7位地址，速率200K */
handle_t dev0 = i2c_get_device(i2c, "/dev/i2c0/dev0", 0x32, 7);
i2c_dev_set_clock_rate(dev0, 200000);

uint8_t reg = 0;
uint8_t data_buf[2] = { 0x00,0x01 };
data_buf[0] = reg;
/* 向0寄存器寫0x01 */
io_write(dev0, data_buf, 2);
/* 從0寄存器讀取1位元組資料 */
i2c_dev_transfer_sequential(dev0, &reg, 1, data_buf, 1);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [i2c\_event\_t](#i2ceventt)：I²C 事件。
- [i2c\_slave\_handler\_t](#i2cslavehandlert)：I²C 從裝置處理程序。

### i2c\_event\_t

#### 描述

I²C 事件。

#### 定義

```c
typedef enum _i2c_event
{
    I2C_EV_START,
    I2C_EV_RESTART,
    I2C_EV_STOP
} i2c_event_t;
```

#### 成員

| 成員名稱            | 描述             |
| ------------------ | ---------------- |
| I2C\_EV\_START     | 收到 Start 信號   |
| I2C\_EV\_RESTART   | 收到 Restart 信號 |
| I2C\_EV\_STOP      | 收到 Stop 信號    |

### i2c\_slave\_handler\_t

#### 描述

I²C 從裝置處理程序。

#### 定義

```c
typedef struct _i2c_slave_handler
{
    void (*on_receive)(uint32_t data);
    uint32_t (*on_transmit)();
    void (*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### 成員

| 成員名稱          | 描述               |
| ---------------- | ------------------ |
| on\_receive      | 收到資料時被調用     |
| on\_transmit     | 需要發送資料時被調用 |
| on\_event        | 發生事件時被調用     |