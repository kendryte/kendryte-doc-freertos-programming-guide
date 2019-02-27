# DMA

## Overview

Direct Memory Access (DMA) controller is used to provide high-speed data transfer between peripherals and memory and between memory and memory.
This improves CPU efficiency by quickly moving data through DMA without any CPU operation.

## Features

The DMA controller has the following features:

- Automatically select an idle DMA channel for transmission
- Automatic selection of software or hardware handshake protocol based on source and destination addresses
- Supports 1, 2, 4, and 8 byte element sizes, source and target sizes do not have to be consistent
- Asynchronous or synchronous transfer function
- Loop transmission function, often used to refresh scenes such as screen or audio recording and playback

## API

Corresponding header file `hal.h`

Provide the following interfaces

- [dma\_open\_free](#dmaopenfree)
- [dma\_close](#dmaclose)
- [dma\_set\_request\_source](#dmasetrequestsource)
- [dma\_transmit\_async](#dmatransmitasync)
- [dma\_transmit](#dmatransmit)
- [dma\_loop\_async](#dmaloopasync)

### dma\_open\_free

#### Description

Open an available DMA device.

#### Function prototype

```c
handle_t dma_open_free();
```

#### Return value

DMA device handle.

### dma\_close

#### Description

Close the DMA device.

#### Function prototype

```c
void dma_close(handle_t file);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | DMA device handle | Input           |

#### Return value

None.

### dma\_set\_request\_source

#### Description

Set the DMA request source.

#### Function prototype

```c
void dma_set_request_source(handle_t file, uint32_t request);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | DMA device handle     | Input           |
| request        | Request source number | Input           |

#### Return value

None.

### dma\_transmit\_async

#### Description

Perform DMA asynchronous transfer.

#### Function prototype

```c
void dma_transmit_async(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, SemaphoreHandle_t completion_event);
```

#### Parameter

|  Parameter name   |                  Description                  | Input or output |
| ----------------- | --------------------------------------------- | --------------- |
| file              | DMA device handle                             | Input           |
| src               | Source address                                | Input           |
| dest              | Destination address                           | Output          |
| src\_inc          | Whether the source address is increasing      | Input           |
| dest\_inc         | Whether the destination address is increasing | Input           |
| element\_size     | Element size (bytes)                          | Input           |
| count             | Element count                                 | Input           |
| burst\_size       | Burst transfer size                           | Input           |
| completion\_event | Transfer completion event                     | Input           |

#### Return value

None.

### dma\_transmit

#### Description

Perform DMA synchronous transfer.

#### Function prototype

```c
void dma_transmit(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size);
```

#### Parameter

| Parameter name |                  Description                  | Input or output |
| -------------- | --------------------------------------------- | --------------- |
| file           | DMA device handle                             | Input           |
| src            | Source address                                | Input           |
| dest           | Destination address                           | Output          |
| src\_inc       | Whether the source address is increasing      | Input           |
| dest\_inc      | Whether the destination address is increasing | Input           |
| element\_size  | Element size (bytes)                          | Input           |
| count          | Element count                                 | Input           |
| burst\_size    | Burst transfer size                           | Input           |

#### Return value

None.

### dma\_loop\_async

#### Description

Perform DMA asynchronous loop transfer.

#### Function prototype

```c
void dma_loop_async(handle_t file, const volatile void **srcs, size_t src_num, volatile void **dests, size_t dest_num, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, dma_stage_completion_handler_t stage_completion_handler, void *stage_completion_handler_data, SemaphoreHandle_t completion_event, int *stop_signal);
```

#### Parameter

|         Parameter name          |                  Description                  | Input or output |
| ------------------------------- | --------------------------------------------- | --------------- |
| file                            | DMA device handle                             | Input           |
| srcs                            | Source address list                           | Input           |
| src\_num                        | Source address count                          | Input           |
| dests                           | Destination address list                      | Output          |
| dest\_num                       | Destination address count                     | Input           |
| src\_inc                        | Whether the source address is increasing      | Input           |
| dest\_inc                       | Whether the destination address is increasing | Input           |
| element\_size                   | Element size (bytes)                          | Input           |
| count                           | Element count                                 | Input           |
| burst\_size                     | Burst transfer size                           | Input           |
| stage\_completion\_handler      | Stage completion handler [^stage_completion]  | Input           |
| stage\_completion\_handler_data | Stage completion handler user data            | Input           |
| completion\_event               | Transfer completion event                     | Input           |
| stop\_signal                    | Stop signal                                   | Input           |

[^stage_completion]: Stage completion refers to the completion of the transfer of a single source to a destination N elements. N is elements count.

#### Return value

None.

### Example

```c
int src[256] = { [0 ... 255] = 1 };
int dest[256];
handle_t dma = dma_open_free();
dma_transmit(dma, src, dest, true, true, sizeof(int), 256, 4);
assert(dest[0] == src[0]);
dma_close(dma);
```

## Data type

The relevant data types and data structures are defined as follows:

- [dma\_stage\_completion\_handler\_t](#dmastagecompletionhandlert)：DMA stage completion handler。

### dma\_stage\_completion\_handler\_t

#### Description

DMA stage completion handler。

#### Type definition

```c
typedef void (*dma_stage_completion_handler_t)(void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| userdata       | User data   | Input           |