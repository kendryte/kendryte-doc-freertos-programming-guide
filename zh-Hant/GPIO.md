# 通用輸入/輸出 (GPIO)

## 概述

晶片有 32 個高速 GPIO 和 8 個通用 GPIO。

## 功能描述

GPIO 模組具有以下功能：

- 可配置上下拉驅動模式
- 支持正緣、負緣和雙緣觸發

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [gpio\_get\_pin\_count](#gpiogetpincount)
- [gpio\_set\_drive\_mode](#gpiosetdrivemode)
- [gpio\_set\_pin\_edge](#gpiosetpinedge)
- [gpio\_set\_on_\changed](#gpiosetonchanged)
- [gpio\_get\_pin\_value](#gpiogetpinvalue)
- [gpio\_set\_pin\_value](#gpiosetpinvalue)

### gpio\_get\_pin\_count

#### 描述

獲取 GPIO 腳位數量。

#### 函數原型

```c
uint32_t gpio_get_pin_count(handle_t file);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |

#### 返回值

腳位數量。

### gpio\_set\_drive\_mode

#### 描述

設置 GPIO 腳位驅動模式。

#### 函數原型

```c
void gpio_set_drive_mode(handle_t file, uint32_t pin, gpio_drive_mode_t mode);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |
| pin        | 腳位編號        | 輸入      |
| mode       | 驅動模式        | 輸入      |

#### 返回值

無。

### gpio\_set\_pin\_edge

#### 描述

設置 GPIO 腳位邊緣觸發模式。

**註：**`/dev/gpio1` 暫不支持。

#### 函數原型

```c
void gpio_set_pin_edge(handle_t file, uint32_t pin, gpio_pin_edge_t edge);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |
| pin        | 腳位編號        | 輸入      |
| edge       | 邊緣觸發模式    | 輸入      |

#### 返回值

無。

### gpio\_set\_on\_changed

#### 描述

設置 GPIO 腳位邊緣觸發處理程序。

**註：**`/dev/gpio1` 暫不支持。

#### 函數原型

```c
void gpio_set_on_changed(handle_t file, uint32_t pin, gpio_on_changed_t callback, void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |
| pin        | 腳位編號        | 輸入      |
| callback   | 處理程序        | 輸入      |
| userdata   | 處理程序用戶資料 | 輸入      |

#### 返回值

無。

### gpio\_get\_pin\_value

#### 描述

獲取 GPIO 腳位的值。

#### 函數原型

```c
gpio_pin_value_t gpio_get_pin_value(handle_t file, uint32_t pin);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |
| pin        | 腳位編號        | 輸入      |

#### 返回值

GPIO 腳位的值。

### gpio\_set\_pin\_value

#### 描述

設置 GPIO 腳位的值。

#### 函數原型

```c
void gpio_set_pin_value(handle_t file, uint32_t pin, gpio_pin_value_t value);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 輸入      |
| pin        | 腳位編號        | 輸入      |
| value      | 要設置的值      | 輸入      |

#### 返回值

無。

### 舉例

```c
handle_t gpio = io_open("/dev/gpio0");

gpio_set_drive_mode(gpio, 0, GPIO_DM_OUTPUT);
gpio_set_pin_value(gpio, 0, GPIO_PV_LOW);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [gpio\_drive\_mode\_t](#gpiodrivemodet)：GPIO 驅動模式。
- [gpio\_pin\_edge\_t](#gpiopinedget)：GPIO 邊緣觸發模式。
- [gpio\_pin\_value\_t](#gpiopinvaluet)：GPIO 值。
- [gpio\_on\_changed\_t](#gpioonchangedt)：GPIO 邊緣觸發處理程序。

### gpio\_drive\_mode\_t

#### 描述

GPIO 驅動模式。

#### 定義

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT
} gpio_drive_mode_t;
```

#### 成員

| 成員名稱                     | 描述        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | 輸入        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | 輸入下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | 輸入上拉     |
| GPIO\_DM\_OUTPUT            | 輸出         |

### gpio\_pin\_edge\_t

#### 描述

GPIO 邊緣觸發模式。

#### 定義

```c
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH
} gpio_pin_edge_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不觸發      |
| GPIO\_PE\_FALLING  | 負緣觸發  |
| GPIO\_PE\_RISING   | 正緣觸發  |
| GPIO\_PE\_BOTH     | 雙緣觸發    |

### gpio\_pin\_value\_t

#### 描述

GPIO 值。

#### 定義

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |

### gpio\_on_changed\_t

#### 描述

GPIO 邊緣觸發處理程序。

#### 定義

```c
typedef void (*gpio_on_changed_t)(uint32_t pin, void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| pin        | 腳位編號        | 輸入      |
| userdata   | 用戶資料        | 輸入      |