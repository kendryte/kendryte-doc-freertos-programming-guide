# I2S

## Overview

The Integrated Inter-IC Sound Bus (I2S) is a serial bus interface standard used for connecting digital audio devices together.

The I2S bus defines three types of signals: the clock signal BCK, the channel selection signal WS, and the serial data signal SD. A basic I2S bus has one master and one slave. The roles of the master and slave remain unchanged during the communication process. The I2S unit includes separate transmit and receive channels for excellent communication performance.

## Features

The I2S module has the following features:

- Automatically configure the device according to the audio format (supports 16, 24, 32 bit depth, 44100 sample rate, 1 - 4 channels)
- Configurable for playback or recording mode
- Automatic management of audio buffers

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

Configure the I2S controller to be in output mode.

#### Function prototype

```c
void i2s_config_as_render(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I2S controller handle | Input           |
| format         | Audio format          | Input           |
| delay\_ms      | Buffer delay time     | Input           |
| align\_mode    | Align mode            | Input           |
| channels\_mask | Channel mask          | Input           |

#### Return value

None.

### i2s\_config\_as\_capture

#### Description

Configure the I2S controller to capture mode.

#### Function prototype

```c
void i2s_config_as_capture(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I2S controller handle | Input           |
| format         | Audio format          | Input           |
| delay\_ms      | Buffer delay time     | Input           |
| align\_mode    | Align mode            | Input           |
| channels\_mask | Channel mask          | Input           |

#### Return value

None.

### i2s\_get\_buffer

#### Description

Get the audio buffer.

#### Function prototype

```c
void i2s_get_buffer(handle_t file, uint8_t **buffer, size_t *frames);
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| file           | I2S controller handle   | Input           |
| buffer         | Buffer                  | Output          |
| frames         | Number of buffer frames | Output          |

#### Return value

None.

### i2s\_release\_buffer

#### Description

Release the audio buffer.

#### Function prototype

```c
void i2s_release_buffer(handle_t file, size_t frames);
```

#### Parameter

| Parameter name |                         Description                         | Input or output |
| -------------- | ----------------------------------------------------------- | --------------- |
| file           | I2S controller handle                                       | Input           |
| frames         | Confirm the number of frames that have been read or written | Input           |

#### Return value

None.

### i2s\_start

#### Description

Start playing or recording.

#### Function prototype

```c
void i2s_start(handle_t file);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I2S controller handle | Input           |

#### Return value

None.

### i2s\_stop

#### Description

Stop playing or recording.

#### Function prototype

```c
void i2s_stop(handle_t file);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I2S controller handle | Input           |

#### Return value

None.

### Example

```c
/* Loop play PCM audio */
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

- [audio\_format\_type\_t](#audioformattypet): Audio format type.
- [audio\_format\_t](#[audioformatt): Audio format.
- [i2s\_align\_mode\_t](#i2salignmodet): I2S align mode.

### audio\_format\_type\_t

#### Description

Audio format type.

#### Type definition

```c
typedef enum _audio_format_type
{
    AUDIO_FMT_PCM
} audio_format_type_t;
```

#### Enumeration element

|  Element name   | Description |
| --------------- | ----------- |
| AUDIO\_FMT\_PCM | PCM         |

### audio\_format\_t

#### Description

Audio format.

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

|   Element name    |       Description        |
| ----------------- | ------------------------ |
| type              | Audio format type        |
| bits\_per\_sample | Sampling bits per sample |
| sample\_rate      | Sample rate              |
| channels          | Number of channels       |

### i2s\_align\_mode\_t

#### Description

I2S align mode.

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

|   Element name    |     Description      |
| ----------------- | -------------------- |
| I2S\_AM\_STANDARD | Standard mode        |
| I2S\_AM\_RIGHT    | Right justified mode |
| I2S\_AM\_LEFT     | Left justified mode  |