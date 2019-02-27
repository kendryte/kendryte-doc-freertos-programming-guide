# DVP

## Overview

Digital Video Port (DVP) unit is a camera interface unit that supports
forwarding camera input image data to KPU or memory.

## Features

The DVP unit has the following features:

- Support RGB565, RGB422 and single channel Y gray scale input mode
- Support for setting frame interrupt
- Support setting transfer address
- Supports writing data to two addresses at the same time (output format is RGB888 and RGB565 respectively)
- Support for discarding frames that do not need to be processed

## API

Corresponding header file `devices.h`

Provide the following interfaces

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

Configure the frequency of DVP XCLK.

#### Function prototype

```c
double dvp_xclk_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name |                             Description                             | Input or output |
| -------------- | ------------------------------------------------------------------- | --------------- |
| file           | DVP device handle                                                   | Input           |
| clock_rate     | Configure the frequency of XCLK, such as OV5640 configured to 20MHz | Input           |

#### Return value

The actual frequency after setting.

### dvp\_config

#### Description

Configure the DVP device.

#### Function prototype

```c
void dvp_config(handle_t file, uint32_t width, uint32_t height, bool auto_enable);
```

#### Parameter

| Parameter name |              Description              | Input or output |
| -------------- | ------------------------------------- | --------------- |
| file           | DVP device handle                     | Input           |
| width          | Frame width                           | Input           |
| height         | Frame height                          | Input           |
| auto_enable    | Automatically enable frame processing | Input           |

#### Return value

None.

### dvp\_enable\_frame

#### Description

Enable processing of the current frame.

#### Function prototype

```c
void dvp_enable_frame(handle_t file);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |

#### Return value

None.

### dvp\_get\_output\_num

#### Description

Get the number of outputs of the DVP device.

#### Function prototype

```c
uint32_t dvp_get_output_num(handle_t file);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |

#### Return value

Output number.

### dvp\_set\_signal

#### Description

Set the DVP signal status.

#### Function prototype

```c
void dvp_set_signal(handle_t file, dvp_signal_type_t type, bool value);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |
| type           | Signal type       | Input           |
| value          | Status value      | Input           |

#### Return value

None.

### dvp\_set\_output\_enable

#### Description

Set whether DVP output is enabled.

#### Function prototype

```c
void dvp_set_output_enable(handle_t file, uint32_t index, bool enable);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |
| index          | Output index      | Input           |
| enable         | Whether to enable | Input           |

#### Return value

None.

### dvp\_set\_output\_attributes

#### Description

Set the DVP output attributes.

#### Function prototype

```c
void dvp_set_output_attributes(handle_t file, uint32_t index, video_format_t format, void *output_buffer);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |
| index          | Output index      | Input           |
| format         | Video format      | Input           |
| output\_buffer | Output buffer     | Output          |

#### Return value

None.

### dvp\_set\_frame\_event\_enable

#### Description

Set whether DVP frame events are enabled.

#### Function prototype

```c
void dvp_set_frame_event_enable(handle_t file, dvp_frame_event_t event, bool enable);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |
| event          | Frame event       | Input           |
| enable         | Whether to enable | Input           |

#### Return value

None.

### dvp\_set\_on\_frame\_event

#### Description

Set up a DVP frame event handler.

#### Function prototype

```c
void dvp_set_on_frame_event(handle_t file, dvp_on_frame_event_t handler, void *userdata);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DVP device handle | Input           |
| handler        | Handler           | Input           |
| userdata       | Handler user data | Input           |

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

- [video\_format\_t](#videoformatt)：Video format.
- [dvp\_frame\_event_t](#dvpframeeventt)：DVP frame event.
- [dvp\_signal\_type\_t](#dvpsignaltypet)：DVP signal type.
- [dvp\_on\_frame\_event\_t](#dvponframeeventt)：The handler when the frame event is triggered.

### video\_format\_t

#### Description

Video format.

#### Type definition

```c
typedef enum _video_format
{
    VIDEO_FMT_RGB565,
    VIDEO_FMT_RGB24_PLANAR
} video_format_t;
```

#### Enumeration element

|       Element name        | Description  |
| ------------------------- | ------------ |
| VIDEO\_FMT\_RGB565        | RGB565       |
| VIDEO\_FMT\_RGB24\_PLANAR | RGB24 Planar |

### dvp\_frame\_event_t

#### Description

DVP frame event.

#### Type definition

```c
typedef enum _video_frame_event
{
    VIDEO_FE_BEGIN,
    VIDEO_FE_END
} dvp_frame_event_t;
```

#### Enumeration element

|   Element name   | Description  |
| ---------------- | ------------ |
| VIDEO\_FE\_BEGIN | Frame start  |
| VIDEO\_FE\_END   | End of frame |

### dvp\_signal\_type\_t

#### Description

DVP signal type.

#### Type definition

```c
typedef enum _dvp_signal_type
{
    DVP_SIG_POWER_DOWN,
    DVP_SIG_RESET
} dvp_signal_type_t;
```

#### Enumeration element

|     Element name      |    Description    |
| --------------------- | ----------------- |
| DVP\_SIG\_POWER\_DOWN | Power down signal |
| DVP\_SIG\_RESET       | Reset signal      |

### dvp\_on\_frame\_event\_t

#### Description

The handler when the frame event is triggered.

#### Type definition

```c
typedef void (*dvp_on_frame_event_t)(dvp_frame_event_t event, void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| userdata       | User data   | Input           |