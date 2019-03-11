# 系統控制

## 概述

系統控制模組提供對操作系統的配置功能。

## 功能描述

系統控制模組具有以下功能：

- 設置 CPU 頻率
- 安裝自定義驅動

## API 參考

對應的頭文件 `hal.h`

為用戶提供以下介面：

- [system\_set\_cpu\_frequency](#systemsetcpufrequency)
- [system\_install\_custom\_driver](#systeminstallcustomdriver)

### system\_set\_cpu\_frequency

#### 描述

設置 CPU 頻率。

#### 函數原型

```c
uint32_t system_set_cpu_frequency(uint32_t frequency);
```

#### 參數

| 參數名稱     |   描述           |  輸入輸出  |
| ----------- | ---------------- | --------- |
| frequency   | 要設置的頻率（Hz） | 輸入      |

#### 返回值

設置後的實際頻率（Hz）。

### system\_install\_custom\_driver

#### 描述

安裝自定義驅動。

#### 函數原型

```c
void system_install_custom_driver(const char *name, const custom_driver_t *driver);
```

#### 參數

| 參數名稱     |   描述             |  輸入輸出  |
| ----------- | ------------------ | --------- |
| name        | 指定訪問該裝置的路徑 | 輸入      |
| driver      | 自定義驅動實現      | 輸入      |

#### 返回值

無。

### 舉例

```c
/* 設置 CPU 頻率為 400MHz */
system_set_cpu_frequency(400000000);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [driver\_base\_t](#driverbaset)：驅動實現基類。
- [custom\_driver\_t](#customdrivert)：自定義驅動實現。

### driver\_base\_t

#### 描述

驅動實現基類。

#### 定義

```c
typedef struct _driver_base
{
    void *userdata;
    void (*install)(void *userdata);
    int (*open)(void *userdata);
    void (*close)(void *userdata);
} driver_base_t;
```

#### 成員

| 成員名稱   | 描述        |
| --------- | ----------- |
| userdata  | 用戶資料     |
| install   | 安裝時被調用 |
| open      | 打開時被調用 |
| close     | 關閉時被調用 |

### custom\_driver\_t

#### 描述

自定義驅動實現。

#### 定義

```c
typedef struct _custom_driver
{
    driver_base_t base;
    int (*io_control)(uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len, void *userdata);
} custom_driver_t;
```

#### 成員

| 成員名稱     | 描述               |
| ----------- | ------------------ |
| base        | 驅動實現基類        |
| io\_control | 收到控制資訊時被調用 |