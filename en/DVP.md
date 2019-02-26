# 数字摄像头接口 (DVP)

## Overview

DVP 是摄像头接口模块，支持把摄像头输入图像数据转发给 AI 模块或者内存。

## Features

DVP 模块具有以下功能：

- RGB565 和 RGB24Planar 共 2 个视频数据输出端口
- 支持丢弃不需要处理的帧

## API

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

#### Description

配置 DVP XCLK的频率。

#### Function prototype

```c
double dvp_xclk_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name            |   Description       |  Input or output  |
| ------------------ | ------------ | --------- |
| file               | DVP 设备句柄  | Input      |
| clock_rate         | 配置XCLK的频率，如OV5640配置为20MHz| Input      |

#### Return value

设置后的实际频率。

### dvp\_config

#### Description

配置 DVP 设备。

#### Function prototype

```c
void dvp_config(handle_t file, uint32_t width, uint32_t height, bool auto_enable);
```

#### Parameter

| Parameter name            |   Description       |  Input or output  |
| ------------------ | ------------ | --------- |
| file               | DVP 设备句柄  | Input      |
| width              | 帧宽度        | Input      |
| height             | 帧高度        | Input      |
| auto_enable        | 自动启用帧处理 | Input      |

#### Return value

None.

### dvp\_enable\_frame

#### Description

启用对当前帧的处理。

#### Function prototype

```c
void dvp_enable_frame(handle_t file);
```

#### Parameter

| Parameter name             |   Description             |  Input or output  |
| ------------------- | ------------------ | --------- |
| file                | DVP 设备句柄        | Input      |

#### Return value

None.

### dvp\_get\_output\_num

#### Description

获取 DVP 设备的Output数目。

#### Function prototype

```c
uint32_t dvp_get_output_num(handle_t file);
```

#### Parameter

| Parameter name          |   Description        |  Input or output  |
| ---------------- | ------------- | --------- |
| file             | DVP 设备句柄   | Input       |

#### Return value

Output数目。

### dvp\_set\_signal

#### Description

设置 DVP 信号状态。

#### Function prototype

```c
void dvp_set_signal(handle_t file, dvp_signal_type_t type, bool value);
```

#### Parameter

| Parameter name |   Description         |  Input or output  |
| ------- | -------------- | --------- |
| file    | DVP 设备句柄    | Input      |
| type    | 信号类型        | Input      |
| value   | 状态值          | Input      |

#### Return value

None.

### dvp\_set\_output\_enable

#### Description

设置 DVP Output是否启用。

#### Function prototype

```c
void dvp_set_output_enable(handle_t file, uint32_t index, bool enable);
```

#### Parameter

| Parameter name |   Description         |  Input or output  |
| ------- | -------------- | --------- |
| file    | DVP 设备句柄    | Input      |
| index   | Output索引        | Input      |
| enable  | 是否启用        | Input      |

#### Return value

None.

### dvp\_set\_output\_attributes

#### Description

设置 DVP Output特性。

#### Function prototype

```c
void dvp_set_output_attributes(handle_t file, uint32_t index, video_format_t format, void *output_buffer);
```

#### Parameter

| Parameter name          |   Description      |  Input or output  |
| ---------------- | ----------- | --------- |
| file             | DVP 设备句柄 | Input      |
| index            | Output索引     | Input      |
| format           | 视频格式     | Input      |
| output\_buffer   | Output缓冲     | Output      |

#### Return value

None.

### dvp\_set\_frame\_event\_enable

#### Description

设置 DVP 帧事件是否启用。

#### Function prototype

```c
void dvp_set_frame_event_enable(handle_t file, dvp_frame_event_t event, bool enable);
```

#### Parameter

| Parameter name          |   Description      |  Input or output  |
| ---------------- | ----------- | --------- |
| file             | DVP 设备句柄 | Input      |
| event            | 帧事件       | Input      |
| enable           | 是否启用     | Input      |

#### Return value

None.

### dvp\_set\_on\_frame\_event

#### Description

设置 DVP 帧事件处理程序。

#### Function prototype

```c
void dvp_set_on_frame_event(handle_t file, dvp_on_frame_event_t handler, void *userdata);
```

#### Parameter

| Parameter name          |   Description         |  Input or output  |
| ---------------- | -------------- | --------- |
| file             | DVP 设备句柄    | Input      |
| handler          | 处理程序        | Input      |
| userdata         | 处理程序用户数据 | Input      |

#### Return value

None.

### Example

```c
handle_t dvp = io_open("/dev/dvp0");

dvp_config(dvp, 320, 240, false);
dvp_set_on_frame_event(dvp, on_frame_isr, NULL);
dvp_set_frame_event_enable(dvp, VIDEO_FE_BEGIN, true);
dvp_set_output_attributes(dvp, 0, VIDEO_FMT_RGB565, lcd_gram0);
dvp_set_output_enable(dvp, 0, true);
```

## Data type

The relevant data types and data structures are defined as follows:

- [video\_format\_t](#videoformatt)：视频格式。
- [dvp\_frame\_event_t](#dvpframeeventt)：DVP 帧事件。
- [dvp\_signal\_type\_t](#dvpsignaltypet)：DVP 信号类型。
- [dvp\_on\_frame\_event\_t](#dvponframeeventt)：DVP 帧事件处理程序。

### video\_format\_t

#### Description

视频格式。

#### Type definition

```c
typedef enum _video_format
{
    VIDEO_FMT_RGB565,
    VIDEO_FMT_RGB24_PLANAR
} video_format_t;
```

#### Enumeration element

| Element name                   | Description         |
| ------------------------- | ------------ |
| VIDEO\_FMT\_RGB565        | RGB565       |
| VIDEO\_FMT\_RGB24\_PLANAR | RGB24 Planar |

### dvp\_frame\_event_t

#### Description

DVP 帧事件。

#### Type definition

```c
typedef enum _video_frame_event
{
    VIDEO_FE_BEGIN,
    VIDEO_FE_END
} dvp_frame_event_t;
```

#### Enumeration element

| Element name           | Description  |
| ----------------- | ----- |
| VIDEO\_FE\_BEGIN  | 帧开始 |
| VIDEO\_FE\_END    | 帧结束 |

### dvp\_signal\_type\_t

#### Description

DVP 信号类型。

#### Type definition

```c
typedef enum _dvp_signal_type
{
    DVP_SIG_POWER_DOWN,
    DVP_SIG_RESET
} dvp_signal_type_t;
```

#### Enumeration element

| Element name                | Description     |
| ---------------------- | -------- |
| DVP\_SIG\_POWER\_DOWN  | 掉电     |
| DVP\_SIG\_RESET        | 复位     |

### dvp\_on\_frame\_event\_t

#### Description

TIMER 触发时的处理程序。

#### Type definition

```c
typedef void (*dvp_on_frame_event_t)(dvp_frame_event_t event, void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | Input      |