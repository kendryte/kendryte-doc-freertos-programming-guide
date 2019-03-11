# 串列外部裝置介面 (SPI)

## 概述

SPI 是一種高速的，全雙工，同步的通信匯流排。

## 功能描述

SPI 模組具有以下功能：

- 獨立的 SPI 裝置封裝外部裝置相關參數
- 自動處理多裝置匯流排爭用
- 支持標準、雙線、四線、八線模式
- 支持先寫後讀和全雙工讀寫
- 支持發送一串相同的資料幀，常用於清屏、填充存儲扇區等場景

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [spi\_get\_device](#spigetdevice)
- [spi\_dev\_config\_non\_standard](#spidevconfignonstandard)
- [spi\_dev\_set\_clock\_rate](#spidevsetclockrate)
- [spi\_dev\_transfer\_full\_duplex](#spidevtransferfullduplex)
- [spi\_dev\_transfer\_sequential](#spidevtransfersequential)
- [spi\_dev\_fill](#spidevfill)

### spi\_get\_device

#### 描述

註冊並打開一個 SPI 裝置。

#### 函數原型

```c
handle_t spi_get_device(handle_t file, const char *name, spi_mode mode, spi_frame_format frame_format, uint32_t chip_select_mask, uint32_t data_bit_length);
```

#### 參數

| 參數名稱            |   描述             |  輸入輸出  |
| ------------------ | ------------------ | --------- |
| file               | SPI 控制器句柄      | 輸入       |
| name               | 指定訪問該裝置的路徑 | 輸入       |
| mode               | SPI 模式            | 輸入       |
| frame\_format      | 幀格式              | 輸入       |
| chip\_select\_mask | 片選掩碼            | 輸入       |
| data\_bit\_length  | 資料位長度          | 輸入       |

#### 返回值

SPI 裝置句柄。

### spi\_dev\_config\_non\_standard

#### 描述

配置 SPI 裝置的非標準幀格式參數。

#### 函數原型

```c
void spi_dev_config_non_standard(handle_t file, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_inst_addr_trans_mode_t trans_mode);
```

#### 參數

| 參數名稱             |   描述             |  輸入輸出  |
| ------------------- | ------------------ | --------- |
| file                | SPI 裝置句柄        | 輸入      |
| instruction\_length | 指令長度            | 輸入      |
| address\_length     | 地址長度            | 輸入      |
| wait\_cycles        | 等待周期數          | 輸入      |
| trans\_mode         | 指令和地址的傳輸模式 | 輸入      |

#### 返回值

無。

### spi\_dev\_set\_clock\_rate

#### 描述

配置 SPI 裝置的時脈速率。

#### 函數原型

```c
double spi_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### 參數

| 參數名稱          |   描述        |  輸入輸出  |
| ---------------- | ------------- | --------- |
| file             | SPI 裝置句柄   | 輸入       |
| clock\_rate      | 期望的時脈速率 | 輸入       |

#### 返回值

設置後的實際速率。

### spi\_dev\_transfer\_full\_duplex

#### 描述

對 SPI 裝置進行全雙工傳輸。

**註：** 僅支持標準幀格式。

#### 函數原型

```c
int spi_dev_transfer_full_duplex(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### 參數

| 參數名稱          |   描述         |  輸入輸出  |
| ---------------- | -------------- | --------- |
| file             | SPI 裝置句柄    | 輸入      |
| write\_buffer    | 源緩衝區        | 輸入      |
| write\_len       | 要寫入的位元組數   | 輸入      |
| read\_buffer     | 目標緩衝區       | 輸出      |
| read\_len        | 最多讀取的位元組數 | 輸入      |

#### 返回值

實際讀取的位元組數。

### spi\_dev\_transfer\_sequential

#### 描述

對 SPI 裝置進行先寫後讀。

**註：** 僅支持標準幀格式。

#### 函數原型

```c
int spi_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### 參數

| 參數名稱          |   描述         |  輸入輸出  |
| ---------------- | -------------- | --------- |
| file             | SPI 裝置句柄    | 輸入      |
| write\_buffer    | 源緩衝區        | 輸入      |
| write\_len       | 要寫入的位元組數   | 輸入      |
| read\_buffer     | 目標緩衝區       | 輸出      |
| read\_len        | 最多讀取的位元組數 | 輸入      |

#### 返回值

實際讀取的位元組數。

### spi\_dev\_fill

#### 描述

對 SPI 裝置填充一串相同的幀。

**註：** 僅支持標準幀格式。

#### 函數原型

```c
void spi_dev_fill(handle_t file, uint32_t instruction, uint32_t address, uint32_t value, size_t count);
```

#### 參數

| 參數名稱          |   描述                 |  輸入輸出  |
| ---------------- | ---------------------- | --------- |
| file             | SPI 裝置句柄            | 輸入      |
| instruction      | 指令（標準幀格式下忽略） | 輸入      |
| address          | 地址（標準幀格式下忽略） | 輸入      |
| value            | 幀資料                 | 輸出      |
| count            | 幀數                   | 輸入      |

#### 返回值

無。

### 舉例

```c
handle_t spi = io_open("/dev/spi0");
/* dev0 工作在 MODE0 模式 標準 SPI 模式 單次發送 8 位資料 使用片選 0 */
handle_t dev0 = spi_get_device(spi, "/dev/spi0/dev0", SPI_MODE_0, SPI_FF_STANDARD, 0b1, 8);
uint8_t data_buf[] = { 0x06, 0x01, 0x02, 0x04, 0, 1, 2, 3 };
/* 發送指令 0x06 向地址 0x010204 發送 0，1，2，3 四個位元組資料 */
io_write(dev0, data_buf, sizeof(data_buf));
/* 發送指令 0x06 地址 0x010204 接收四個位元組的資料 */
spi_dev_transfer_sequential(dev0, data_buf, 4, data_buf, 4);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [spi\_mode\_t](#spimodet)：SPI 模式。
- [spi\_frame\_format\_t](#spiframeformatt)：SPI 幀格式。
- [spi\_inst\_addr\_trans\_mode\_t](#spiinstaddrtransmodet)：SPI 指令和地址的傳輸模式。

### spi\_mode\_t

#### 描述

SPI 模式。

#### 定義

```c
typedef enum _spi_mode
{
    SPI_MODE_0,
    SPI_MODE_1,
    SPI_MODE_2,
    SPI_MODE_3,
} spi_mode_t;
```

#### 成員

| 成員名稱       | 描述        |
| ------------- | ----------- |
| SPI\_MODE\_0  | SPI 模式 0  |
| SPI\_MODE\_1  | SPI 模式 1  |
| SPI\_MODE\_2  | SPI 模式 2  |
| SPI\_MODE\_3  | SPI 模式 3  |

### spi\_frame\_format\_t

#### 描述

SPI 幀格式。

#### 定義

```c
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### 成員

| 成員名稱            | 描述                      |
| ------------------ | ------------------------- |
| SPI\_FF\_STANDARD  | 標準                      |
| SPI\_FF\_DUAL      | 雙線                      |
| SPI\_FF\_QUAD      | 四線                      |
| SPI\_FF\_OCTAL     | 八線（`/dev/spi3` 不支持） |

### spi\_inst\_addr\_trans\_mode\_t

#### 描述

SPI 指令和地址的傳輸模式。

#### 定義

```c
typedef enum _spi_inst_addr_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_inst_addr_trans_mode_t;
```

#### 成員

| 成員名稱                      | 描述               |
| ---------------------------- | ------------------ |
| SPI\_AITM\_STANDARD          | 均使用標準幀格式     |
| SPI\_AITM\_ADDR\_STANDARD    | 指令使用配置的值，地址使用標準幀格式 |
| SPI\_AITM\_AS\_FRAME\_FORMAT | 均使用配置的值     |