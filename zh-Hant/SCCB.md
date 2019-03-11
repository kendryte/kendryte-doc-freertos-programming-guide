# 串列攝像機控制匯流排 (SCCB)

## 概述

SCCB 是一種串列攝像機控制匯流排。

## 功能描述

SCCB 模組具有以下功能：

- 獨立的 SCCB 裝置封裝外部裝置相關參數
- 自動處理多裝置匯流排爭用

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [sccb\_get\_device](#sccbgetdevice)
- [sccb\_dev\_read\_byte](#sccbdevreadbyte)
- [sccb\_dev\_write\_byte](#sccbdevwritebyte)

### sccb\_get\_device

#### 描述

註冊並打開一個 SCCB 裝置。

#### 函數原型

```c
handle_t sccb_get_device(handle_t file, const char *name, size_t slave_address, size_t reg_address_width);
```

#### 參數

| 參數名稱            |   描述             |  輸入輸出  |
| ------------------ | ------------------ | --------- |
| file               | SCCB 控制器句柄      | 輸入      |
| name               | 指定訪問該裝置的路徑 | 輸入      |
| slave\_address     | 從裝置地址          | 輸入      |
| reg_address\_width | 寄存器地址寬度      | 輸入      |

#### 返回值

SCCB 裝置句柄。

### sccb\_dev\_read\_byte

#### 描述

從 SCCB 裝置讀取一個位元組。

#### 函數原型

```c
uint8_t sccb_dev_read_byte(handle_t file, uint16_t reg_address);
```

#### 參數

| 參數名稱       |   描述         |  輸入輸出  |
| ------------- | -------------- | --------- |
| file          | SCCB 裝置句柄   | 輸入      |
| reg\_address  | 寄存器地址      | 輸入      |

#### 返回值

讀取的位元組。

### sccb\_dev\_write\_byte

#### 描述

向 SCCB 裝置寫入一個位元組。

#### 函數原型

```c
void sccb_dev_write_byte(handle_t file, uint16_t reg_address, uint8_t value);
```

#### 參數

| 參數名稱          |   描述         |  輸入輸出  |
| ---------------- | -------------- | --------- |
| file             | SCCB 裝置句柄   | 輸入       |
| reg\_address     | 寄存器地址      | 輸入       |
| value            | 要寫入的位元組    | 輸入       |

#### 返回值

無。

### 舉例

```c
handle_t sccb = io_open("/dev/sccb0");
handle_t dev0 = sccb_get_device(sccb, "/dev/sccb0/dev0", 0x60, 8);

sccb_dev_write_byte(dev0, 0xFF, 0);
uint8_t value = sccb_dev_read_byte(dev0, 0xFF);
```