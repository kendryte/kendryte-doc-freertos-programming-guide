# 数字摄像头接口 (DVP)

## 概述

DVP 是摄像头接口模块，支持把摄像头输入图像数据转发给 AI 模块或者内存。

## 功能描述

DVP 模块具有以下功能：

- RGB565 和 RGB24Planar 共 2 个视频数据输出端口
- 支持丢弃不需要处理的帧

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

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

配置 DVP XCLK的频率。

#### 函数原型

```c
double dvp_xclk_set_clock_rate(handle_t file, double clock_rate);
```

#### 参数

| 参数名称            |   描述       |  输入输出  |
| ------------------ | ------------ | --------- |
| file               | DVP 设备句柄  | 输入      |
| clock_rate         | 配置XCLK的频率，如OV5640配置为20MHz| 输入      |

#### 返回值

设置后的实际频率。

### dvp\_config

#### 描述

配置 DVP 设备。

#### 函数原型

```c
void dvp_config(handle_t file, uint32_t width, uint32_t height, bool auto_enable);
```

#### 参数

| 参数名称            |   描述       |  输入输出  |
| ------------------ | ------------ | --------- |
| file               | DVP 设备句柄  | 输入      |
| width              | 帧宽度        | 输入      |
| height             | 帧高度        | 输入      |
| auto_enable        | 自动启用帧处理 | 输入      |

#### 返回值

无。

### dvp\_enable\_frame

#### 描述

启用对当前帧的处理。

#### 函数原型

```c
void dvp_enable_frame(handle_t file);
```

#### 参数

| 参数名称             |   描述             |  输入输出  |
| ------------------- | ------------------ | --------- |
| file                | DVP 设备句柄        | 输入      |

#### 返回值

无。

### dvp\_get\_output\_num

#### 描述

获取 DVP 设备的输出数目。

#### 函数原型

```c
uint32_t dvp_get_output_num(handle_t file);
```

#### 参数

| 参数名称          |   描述        |  输入输出  |
| ---------------- | ------------- | --------- |
| file             | DVP 设备句柄   | 输入       |

#### 返回值

输出数目。

### dvp\_set\_signal

#### 描述

设置 DVP 信号状态。

#### 函数原型

```c
void dvp_set_signal(handle_t file, dvp_signal_type_t type, bool value);
```

#### 参数

| 参数名称 |   描述         |  输入输出  |
| ------- | -------------- | --------- |
| file    | DVP 设备句柄    | 输入      |
| type    | 信号类型        | 输入      |
| value   | 状态值          | 输入      |

#### 返回值

无。

### dvp\_set\_output\_enable

#### 描述

设置 DVP 输出是否启用。

#### 函数原型

```c
void dvp_set_output_enable(handle_t file, uint32_t index, bool enable);
```

#### 参数

| 参数名称 |   描述         |  输入输出  |
| ------- | -------------- | --------- |
| file    | DVP 设备句柄    | 输入      |
| index   | 输出索引        | 输入      |
| enable  | 是否启用        | 输入      |

#### 返回值

无。

### dvp\_set\_output\_attributes

#### 描述

设置 DVP 输出特性。

#### 函数原型

```c
void dvp_set_output_attributes(handle_t file, uint32_t index, video_format_t format, void *output_buffer);
```

#### 参数

| 参数名称          |   描述      |  输入输出  |
| ---------------- | ----------- | --------- |
| file             | DVP 设备句柄 | 输入      |
| index            | 输出索引     | 输入      |
| format           | 视频格式     | 输入      |
| output\_buffer   | 输出缓冲     | 输出      |

#### 返回值

无。

### dvp\_set\_frame\_event\_enable

#### 描述

设置 DVP 帧事件是否启用。

#### 函数原型

```c
void dvp_set_frame_event_enable(handle_t file, dvp_frame_event_t event, bool enable);
```

#### 参数

| 参数名称          |   描述      |  输入输出  |
| ---------------- | ----------- | --------- |
| file             | DVP 设备句柄 | 输入      |
| event            | 帧事件       | 输入      |
| enable           | 是否启用     | 输入      |

#### 返回值

无。

### dvp\_set\_on\_frame\_event

#### 描述

设置 DVP 帧事件处理程序。

#### 函数原型

```c
void dvp_set_on_frame_event(handle_t file, dvp_on_frame_event_t handler, void *userdata);
```

#### 参数

| 参数名称          |   描述         |  输入输出  |
| ---------------- | -------------- | --------- |
| file             | DVP 设备句柄    | 输入      |
| handler          | 处理程序        | 输入      |
| userdata         | 处理程序用户数据 | 输入      |

#### 返回值

无。

### 举例

```c
handle_t dvp = io_open("/dev/dvp0");

dvp_config(dvp, 320, 240, false);
dvp_set_on_frame_event(dvp, on_frame_isr, NULL);
dvp_set_frame_event_enable(dvp, VIDEO_FE_BEGIN, true);
dvp_set_output_attributes(dvp, 0, VIDEO_FMT_RGB565, lcd_gram0);
dvp_set_output_enable(dvp, 0, true);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [video\_format\_t](#videoformatt)：视频格式。
- [dvp\_frame\_event_t](#dvpframeeventt)：DVP 帧事件。
- [dvp\_signal\_type\_t](#dvpsignaltypet)：DVP 信号类型。
- [dvp\_on\_frame\_event\_t](#dvponframeeventt)：DVP 帧事件处理程序。

### video\_format\_t

#### 描述

视频格式。

#### 定义

```c
typedef enum _video_format
{
    VIDEO_FMT_RGB565,
    VIDEO_FMT_RGB24_PLANAR
} video_format_t;
```

#### 成员

| 成员名称                   | 描述         |
| ------------------------- | ------------ |
| VIDEO\_FMT\_RGB565        | RGB565       |
| VIDEO\_FMT\_RGB24\_PLANAR | RGB24 Planar |

### dvp\_frame\_event_t

#### 描述

DVP 帧事件。

#### 定义

```c
typedef enum _video_frame_event
{
    VIDEO_FE_BEGIN,
    VIDEO_FE_END
} dvp_frame_event_t;
```

#### 成员

| 成员名称           | 描述  |
| ----------------- | ----- |
| VIDEO\_FE\_BEGIN  | 帧开始 |
| VIDEO\_FE\_END    | 帧结束 |

### dvp\_signal\_type\_t

#### 描述

DVP 信号类型。

#### 定义

```c
typedef enum _dvp_signal_type
{
    DVP_SIG_POWER_DOWN,
    DVP_SIG_RESET
} dvp_signal_type_t;
```

#### 成员

| 成员名称                | 描述     |
| ---------------------- | -------- |
| DVP\_SIG\_POWER\_DOWN  | 掉电     |
| DVP\_SIG\_RESET        | 复位     |

### dvp\_on\_frame\_event\_t

#### 描述

TIMER 触发时的处理程序。

#### 定义

```c
typedef void (*dvp_on_frame_event_t)(dvp_frame_event_t event, void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |