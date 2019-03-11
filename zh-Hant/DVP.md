# 數位攝像頭介面 (DVP)

## 概述

DVP 是攝像頭介面模組，支持把攝像頭輸入圖像資料轉發給 AI 模組或者內部儲存。

## 功能描述

DVP 模組具有以下功能：

- 支持RGB565、RGB422與單通道Y灰度輸入模式
- 支持設置幀中斷
- 支持設置傳輸地址
- 支持同時向兩個地址寫資料（輸出格式分別是RGB888與RGB565）
- 支持丟棄不需要處理的幀

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [dvp\_xclk\_set\_clock\_rate](#dvpxclksetclockrate)
- [dvp\_config](#dvpconfig)
- [dvp\_enable\_frame](#dvpenableframe)
- [dvp\_get\_output\_num](#dvpgetoutputnum)
- [dvp\_set\_signal](#dvpsetsignal)
- [dvp\_set\_output\_enable](#dvpsetoutputenable)
- [dvp\_set\_output\_attributes](#dvpsetoutputattributes)
- [dvp\_set\_frame\_event\_enable](#dvpsetframeeventenable)
- [dvp\_set\_on\_frame\_event](#dvpsetonframeevent)

### dvp\_xclk\_set\_clock\_rate

#### 描述

配置 DVP XCLK的頻率。

#### 函數原型

```c
double dvp_xclk_set_clock_rate(handle_t file, double clock_rate);
```

#### 參數

| 參數名稱            |   描述       |  輸入輸出  |
| ------------------ | ------------ | --------- |
| file               | DVP 裝置句柄  | 輸入      |
| clock_rate         | 配置XCLK的頻率，如OV5640配置為20MHz| 輸入      |

#### 返回值

設置後的實際頻率。

### dvp\_config

#### 描述

配置 DVP 裝置。

#### 函數原型

```c
void dvp_config(handle_t file, uint32_t width, uint32_t height, bool auto_enable);
```

#### 參數

| 參數名稱            |   描述       |  輸入輸出  |
| ------------------ | ------------ | --------- |
| file               | DVP 裝置句柄  | 輸入      |
| width              | 幀寬度        | 輸入      |
| height             | 幀高度        | 輸入      |
| auto_enable        | 自動啟用幀處理 | 輸入      |

#### 返回值

無。

### dvp\_enable\_frame

#### 描述

啟用對當前幀的處理。

#### 函數原型

```c
void dvp_enable_frame(handle_t file);
```

#### 參數

| 參數名稱             |   描述             |  輸入輸出  |
| ------------------- | ------------------ | --------- |
| file                | DVP 裝置句柄        | 輸入      |

#### 返回值

無。

### dvp\_get\_output\_num

#### 描述

獲取 DVP 裝置的輸出數目。

#### 函數原型

```c
uint32_t dvp_get_output_num(handle_t file);
```

#### 參數

| 參數名稱          |   描述        |  輸入輸出  |
| ---------------- | ------------- | --------- |
| file             | DVP 裝置句柄   | 輸入       |

#### 返回值

輸出數目。

### dvp\_set\_signal

#### 描述

設置 DVP 信號狀態。

#### 函數原型

```c
void dvp_set_signal(handle_t file, dvp_signal_type_t type, bool value);
```

#### 參數

| 參數名稱 |   描述         |  輸入輸出  |
| ------- | -------------- | --------- |
| file    | DVP 裝置句柄    | 輸入      |
| type    | 信號類型        | 輸入      |
| value   | 狀態值          | 輸入      |

#### 返回值

無。

### dvp\_set\_output\_enable

#### 描述

設置 DVP 輸出是否啟用。

#### 函數原型

```c
void dvp_set_output_enable(handle_t file, uint32_t index, bool enable);
```

#### 參數

| 參數名稱 |   描述         |  輸入輸出  |
| ------- | -------------- | --------- |
| file    | DVP 裝置句柄    | 輸入      |
| index   | 輸出索引        | 輸入      |
| enable  | 是否啟用        | 輸入      |

#### 返回值

無。

### dvp\_set\_output\_attributes

#### 描述

設置 DVP 輸出特性。

#### 函數原型

```c
void dvp_set_output_attributes(handle_t file, uint32_t index, video_format_t format, void *output_buffer);
```

#### 參數

| 參數名稱          |   描述      |  輸入輸出  |
| ---------------- | ----------- | --------- |
| file             | DVP 裝置句柄 | 輸入      |
| index            | 輸出索引     | 輸入      |
| format           | 視訊格式     | 輸入      |
| output\_buffer   | 輸出緩衝     | 輸出      |

#### 返回值

無。

### dvp\_set\_frame\_event\_enable

#### 描述

設置 DVP 幀事件是否啟用。

#### 函數原型

```c
void dvp_set_frame_event_enable(handle_t file, dvp_frame_event_t event, bool enable);
```

#### 參數

| 參數名稱          |   描述      |  輸入輸出  |
| ---------------- | ----------- | --------- |
| file             | DVP 裝置句柄 | 輸入      |
| event            | 幀事件       | 輸入      |
| enable           | 是否啟用     | 輸入      |

#### 返回值

無。

### dvp\_set\_on\_frame\_event

#### 描述

設置 DVP 幀事件處理程序。

#### 函數原型

```c
void dvp_set_on_frame_event(handle_t file, dvp_on_frame_event_t handler, void *userdata);
```

#### 參數

| 參數名稱          |   描述         |  輸入輸出  |
| ---------------- | -------------- | --------- |
| file             | DVP 裝置句柄    | 輸入      |
| handler          | 處理程序        | 輸入      |
| userdata         | 處理程序用戶資料 | 輸入      |

#### 返回值

無。

### 舉例

```c
handle_t dvp = io_open("/dev/dvp0");

dvp_config(dvp, 320, 240, false);
dvp_set_on_frame_event(dvp, on_frame_isr, NULL);
dvp_set_frame_event_enable(dvp, VIDEO_FE_BEGIN, true);
dvp_set_output_attributes(dvp, 0, VIDEO_FMT_RGB565, lcd_gram0);
dvp_set_output_enable(dvp, 0, true);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [video\_format\_t](#videoformatt)：視訊格式。
- [dvp\_frame\_event_t](#dvpframeeventt)：DVP 幀事件。
- [dvp\_signal\_type\_t](#dvpsignaltypet)：DVP 信號類型。
- [dvp\_on\_frame\_event\_t](#dvponframeeventt)：DVP 幀事件處理程序。

### video\_format\_t

#### 描述

視訊格式。

#### 定義

```c
typedef enum _video_format
{
    VIDEO_FMT_RGB565,
    VIDEO_FMT_RGB24_PLANAR
} video_format_t;
```

#### 成員

| 成員名稱                   | 描述         |
| ------------------------- | ------------ |
| VIDEO\_FMT\_RGB565        | RGB565       |
| VIDEO\_FMT\_RGB24\_PLANAR | RGB24 Planar |

### dvp\_frame\_event_t

#### 描述

DVP 幀事件。

#### 定義

```c
typedef enum _video_frame_event
{
    VIDEO_FE_BEGIN,
    VIDEO_FE_END
} dvp_frame_event_t;
```

#### 成員

| 成員名稱           | 描述  |
| ----------------- | ----- |
| VIDEO\_FE\_BEGIN  | 幀開始 |
| VIDEO\_FE\_END    | 幀結束 |

### dvp\_signal\_type\_t

#### 描述

DVP 信號類型。

#### 定義

```c
typedef enum _dvp_signal_type
{
    DVP_SIG_POWER_DOWN,
    DVP_SIG_RESET
} dvp_signal_type_t;
```

#### 成員

| 成員名稱                | 描述     |
| ---------------------- | -------- |
| DVP\_SIG\_POWER\_DOWN  | 掉電     |
| DVP\_SIG\_RESET        | 複位     |

### dvp\_on\_frame\_event\_t

#### 描述

TIMER 觸發時的處理程序。

#### 定義

```c
typedef void (*dvp_on_frame_event_t)(dvp_frame_event_t event, void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| userdata   | 用戶資料        | 輸入      |