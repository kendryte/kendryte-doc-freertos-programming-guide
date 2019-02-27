# Standard IO

## Overview

The standard IO module is the basic interface for accessing peripherals.

## Features

The standard IO module has the following features:

- Find peripherals based on the path
- Unified read and write and control interface

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [io\_open](#ioopen)
- [io\_close](#ioclose)
- [io\_read](#ioread)
- [io\_write](#iowrite)
- [io\_control](#iocontrol)

### io\_open

#### Description

Open a device.

#### Function prototype

```c
handle_t io_open(const char *name);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| name           | Device path | Input           |

#### Return value

| Return value |  Description  |
| ------------ | ------------- |
| 0            | Fail          |
| Others       | device handle |

### io\_close

#### Description

Close a device.

#### Function prototype

```c
int io_close(handle_t file);
```

#### Parameter

| Parameter name |  Description  | Input or output |
| -------------- | ------------- | --------------- |
| file           | device handle | Input           |

#### Return value

| Return value | Description |
| ------------ | ----------- |
| 0            | Success     |
| Others       | Fail        |

### io\_read

#### Description

Read from the device.

#### Function prototype

```c
int io_read(handle_t file, uint8_t *buffer, size_t len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | Device handle                | Input           |
| buffer         | Destination buffer           | Output          |
| len            | Maximum number of bytes read | Input           |

#### Return value

The number of bytes actually read.

### io\_write

#### Description

Write to the device.

#### Function prototype

```c
int io_write(handle_t file, const uint8_t *buffer, size_t len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | Device handle                | Input           |
| buffer         | Source buffer                | Input           |
| len            | The number of bytes to write | Input           |

#### Return value

| Return value | Description |
| ------------ | ----------- |
| len          | Success     |
| Others       | Fail        |

### io\_control

#### Description

Send control information to the device.

#### Function prototype

```c
int io_control(handle_t file, uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | Device handle                | Input           |
| control\_code  | Control code                 | Input           |
| write\_buffer  | Source buffer                | Input           |
| write\_len     | The number of bytes to write | Input           |
| read\_buffer   | Destination buffer           | Output          |
| read\_len      | Maximum number of bytes read | Input           |

#### Return value

The number of bytes actually read.

### Example

```c
handle_t uart = io_open("/dev/uart1");
io_write(uart, "hello\n", 6);
io_close(uart);
```