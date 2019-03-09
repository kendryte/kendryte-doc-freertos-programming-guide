# SCCB

## Overview

Serial Camera Control Bus (SCCB) interface.
The SCCB protocol is very similar to the I²C protocol.

## Features

The SCCB module has the following features:

- Independently packaged peripheral related parameters
- Automatic processing of multi-device bus contention

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [sccb\_get\_device](#sccbgetdevice)
- [sccb\_dev\_read\_byte](#sccbdevreadbyte)
- [sccb\_dev\_write\_byte](#sccbdevwritebyte)

### sccb\_get\_device

#### Description

Register and open an SCCB device.

#### Function prototype

```c
handle_t sccb_get_device(handle_t file, const char *name, size_t slave_address, size_t reg_address_width);
```

#### Parameter

|   Parameter name   |              Description              | Input or output |
| ------------------ | ------------------------------------- | --------------- |
| file               | SCCB controller handle                | Input           |
| name               | Specify the path to access the device | Input           |
| slave\_address     | Slave address                         | Input           |
| reg_address\_width | Register address width                | Input           |

#### Return value

SCCB device handle.

### sccb\_dev\_read\_byte

#### Description

Read a byte from the SCCB device.

#### Function prototype

```c
uint8_t sccb_dev_read_byte(handle_t file, uint16_t reg_address);
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| file           | SCCB device handle | Input           |
| reg\_address   | Register address   | Input           |

#### Return value

The byte read.

### sccb\_dev\_write\_byte

#### Description

Write a byte to the SCCB device.

#### Function prototype

```c
void sccb_dev_write_byte(handle_t file, uint16_t reg_address, uint8_t value);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | SCCB device handle     | Input           |
| reg\_address   | Register address       | Input           |
| value          | The byte to be written | Input           |

#### Return value

None.

### Example

```c
handle_t sccb = io_open("/dev/sccb0");
handle_t dev0 = sccb_get_device(sccb, "/dev/sccb0/dev0", 0x60, 8);

sccb_dev_write_byte(dev0, 0xFF, 0);
uint8_t value = sccb_dev_read_byte(dev0, 0xFF);
```
