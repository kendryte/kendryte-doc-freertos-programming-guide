# 集成电路内置音频总线 (I2S)

## Overview

I2S 标准总线定义了三种信号: 时钟信号 BCK、声道选择信号 WS 和串行数据信号 SD。一个基本的I2S 数据总线有一个主机和一个从机。主机和从机的角色在通信过程中保持不变。I2S 模块包含独立的发送和接收声道，能够保证优良的通信性能。

## Features

I2S 模块具有以下功能: 

- 根据音频格式自动配置设备（支持 16、24、32 位深，44100 采样率，1 - 4 声道）
- 可配置为播放或录音模式
- 自动管理音频缓冲区

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [i2s\_config\_as\_render](#i2sconfigasrender)
- [i2s\_config\_as\_capture](#i2sconfigascapture)
- [i2s\_get\_buffer](#i2sgetbuffer)
- [i2s\_release\_buffer](#i2sreleasebuffer)
- [i2s\_start](#i2sstart)
- [i2s\_stop](#i2sstop)

### i2s\_config\_as\_render

#### Description

配置 I2S 控制器为输出模式。

#### Function prototype

```c
void i2s_config_as_render(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### Parameter

| Parameter name          |   Description             |  Input or output  |
| ---------------- | ------------------ | --------- |
| file             | I2S 控制器句柄      | Input      |
| format           | 音频格式            | Input      |
| delay\_ms        | 缓冲区长度          | Input      |
| align\_mode      | 对齐模式            | Input      |
| channels\_mask   | 通道掩码            | Input      |

#### Return value

None.

### i2s\_config\_as\_capture

#### Description

配置 I2S 控制器为捕获模式。

#### Function prototype

```c
void i2s_config_as_capture(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### Parameter

| Parameter name          |   Description             |  Input or output  |
| ---------------- | ------------------ | --------- |
| file             | I2S 控制器句柄      | Input      |
| format           | 音频格式            | Input      |
| delay\_ms        | 缓冲区长度          | Input      |
| align\_mode      | 对齐模式            | Input      |
| channels\_mask   | 通道掩码            | Input      |

#### Return value

None.

### i2s\_get\_buffer

#### Description

获取音频缓冲区。

#### Function prototype

```c
void i2s_get_buffer(handle_t file, uint8_t **buffer, size_t *frames);
```

#### Parameter

| Parameter name    |   Description        |  Input or output  |
| ---------- | ------------- | --------- |
| file       | I2S 控制器句柄 | Input       |
| buffer     | 缓冲区         | Output       |
| frames     | 缓冲区帧数     | Output       |

#### Return value

None.

### i2s\_release\_buffer

#### Description

释放音频缓冲区。

#### Function prototype

```c
void i2s_release_buffer(handle_t file, size_t frames);
```

#### Parameter

| Parameter name    |   Description               |  Input or output  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | Input       |
| frames     | 确认已读取或写入的帧数 | Input       |

#### Return value

None.

### i2s\_start

#### Description

开始播放或录音。

#### Function prototype

```c
void i2s_start(handle_t file);
```

#### Parameter

| Parameter name    |   Description               |  Input or output  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | Input       |

#### Return value

None.

### i2s\_stop

#### Description

停止播放或录音。

#### Function prototype

```c
void i2s_stop(handle_t file);
```

#### Parameter

| Parameter name    |   Description               |  Input or output  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | Input       |

#### Return value

None.

### Example

```c
/* 循环播放 PCM 音频 */
handle_t i2s = io_open("/dev/i2s0");
audio_format_t audio_fmt = { .type = AUDIO_FMT_PCM, .bits_per_sample = 16, .sample_rate = 44100, .channels = 2 };
i2s_config_as_render(i2s, &audio_fmt, 100, I2S_AM_RIGHT, 0b11);
i2s_start(i2s);

while (1)
{
    uint8_t *buffer;
    size_t frames;
    i2s_get_buffer(i2s, &buffer, &frames);
    memcpy(buffer, pcm, 4 * frames);
    i2s_release_buffer(i2s, frames);
    pcm += frames;
    if (pcm >= pcm_end)
        pcm = pcm_start;
}
```

## Data type

The relevant data types and data structures are defined as follows:

- [audio\_format\_type\_t](#audioformattypet): 音频格式类型。
- [audio\_format\_t](#[audioformatt): 音频格式。
- [i2s\_align\_mode\_t](#i2salignmodet): I2S 对齐模式。

### audio\_format\_type\_t

#### Description

音频格式类型。

#### Type definition

```c
typedef enum _audio_format_type
{
    AUDIO_FMT_PCM
} audio_format_type_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| AUDIO\_FMT\_PCM    | PCM         |

### audio\_format\_t

#### Description

音频格式。

#### Type definition

```c
typedef struct _audio_format
{
    audio_format_type_t type;
    uint32_t bits_per_sample;
    uint32_t sample_rate;
    uint32_t channels;
} audio_format_t;
```

#### Enumeration element

| Element name           | Description          |
| ----------------- | ------------- |
| type              | 音频格式类型   |
| bits\_per\_sample | 采样深度       |
| sample\_rate      | 采样率         |
| channels          | 声道数         |

### i2s\_align\_mode\_t

#### Description

I2S 对齐模式。

#### Type definition

```c
typedef enum _i2s_align_mode
{
    I2S_AM_STANDARD,
    I2S_AM_RIGHT,
    I2S_AM_LEFT
} i2s_align_mode_t;
```

#### Enumeration element

| Element name           | Description        |
| ----------------- | ----------- |
| I2S\_AM\_STANDARD | 标准模式     |
| I2S\_AM\_RIGHT    | 右对齐       |
| I2S\_AM\_LEFT     | 左对齐       |