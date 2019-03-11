# 標準 IO

## 概述

標準 IO 模組是訪問外部裝置的基本介面。

## 功能描述

標準 IO 模組具有以下功能：

- 根據路徑尋找外部裝置
- 統一的讀寫和控制介面

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [io\_open](#ioopen)
- [io\_close](#ioclose)
- [io\_read](#ioread)
- [io\_write](#iowrite)
- [io\_control](#iocontrol)

### io\_open

#### 描述

打開一個裝置。

#### 函數原型

```c
handle_t io_open(const char *name);
```

#### 參數

| 參數名稱   |   描述     |  輸入輸出  |
| --------- | ---------- | --------- |
| name      | 裝置路徑    | 輸入      |

#### 返回值

| 返回值 |  描述   |
| ----- | ------- |
| 0     | 失敗    |
| 其他  | 裝置句柄 |

### io\_close

#### 描述

關閉一個裝置。

#### 函數原型

```c
int io_close(handle_t file);
```

#### 參數

| 參數名稱   |   描述     |  輸入輸出  |
| --------- | ---------- | --------- |
| file      | 裝置句柄    | 輸入      |

#### 返回值

| 返回值 |  描述   |
| ----- | ------- |
| 0     | 成功    |
| 其他  | 失敗    |

### io\_read

#### 描述

從裝置讀取。

#### 函數原型

```c
int io_read(handle_t file, uint8_t *buffer, size_t len);
```

#### 參數

| 參數名稱   |   描述         |  輸入輸出  |
| --------- | -------------- | --------- |
| file      | 裝置句柄        | 輸入      |
| buffer    | 目標緩衝區      | 輸出      |
| len       | 最多讀取的位元組數 | 輸入      |

#### 返回值

實際讀取的位元組數。

### io\_write

#### 描述

向裝置寫入。

#### 函數原型

```c
int io_write(handle_t file, const uint8_t *buffer, size_t len);
```

#### 參數

| 參數名稱   |   描述       |  輸入輸出  |
| --------- | ------------ | --------- |
| file      | 裝置句柄      | 輸入      |
| buffer    | 源緩衝區      | 輸入      |
| len       | 要寫入的位元組數 | 輸入      |

#### 返回值

| 返回值 |  描述   |
| ----- | ------- |
| len   | 成功    |
| 其他  | 失敗    |

### io\_control

#### 描述

向裝置發送控制資訊。

#### 函數原型

```c
int io_control(handle_t file, uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### 參數

| 參數名稱       |   描述         |  輸入輸出  |
| ------------- | -------------- | --------- |
| file          | 裝置句柄        | 輸入      |
| control\_code | 控制碼          | 輸入      |
| write\_buffer | 源緩衝區        | 輸入      |
| write\_len    | 要寫入的位元組數   | 輸入      |
| read\_buffer  | 目標緩衝區      | 輸出      |
| read\_len     | 最多讀取的位元組數 | 輸入      |

#### 返回值

實際讀取的位元組數。

### 舉例

```c
handle_t uart = io_open("/dev/uart1");
io_write(uart, "hello\n", 6);
io_close(uart);
```