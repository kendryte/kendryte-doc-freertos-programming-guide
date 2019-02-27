# I²C

## Overview

The I²C (Inter-Integrated Circuit) bus is used to communicate with multiple
external I²C devices. Multiple external I²C devices can share an I²C bus.

## Features

The I²C unit has the following features:

- Independent I²C controller
- Automatic processing of multi-device bus contention
- Support slave mode

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [i2c\_get\_device](#i2cgetdevice)
- [i2c\_dev\_set\_clock\_rate](#i2cdevsetclockrate)
- [i2c\_dev\_transfer\_sequential](#i2cdevtransfersequential)
- [i2c\_config\_as\_slave](#i2cconfigasslave)
- [i2c\_slave\_set\_clock\_rate](#i2cslavesetclockrate)

### i2c\_get\_device

#### Description

Register and open an I²C device.

#### Function prototype

```c
handle_t i2c_get_device(handle_t file, const char *name, uint32_t slave_address, uint32_t address_width);
```

#### Parameter

| Parameter name |              Description              | Input or output |
| -------------- | ------------------------------------- | --------------- |
| file           | I²C controller handle                 | Input           |
| name           | Specify the path to access the device | Input           |
| slave\_address | Slave address                         | Input           |
| address\_width | Slave address width                   | Input           |

#### Return value

I²C device handle.

### i2c\_dev\_set\_clock\_rate

#### Description

Configure the clock rate of the I²C device.

#### Function prototype

```c
double i2c_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name |     Description     | Input or output |
| -------------- | ------------------- | --------------- |
| file           | I²C device handle   | Input           |
| clock\_rate    | Expected clock rate | Input           |

#### Return value

The actual clock rate after setting.

### i2c\_dev\_transfer\_sequential

#### Description

Read the I²C device, then write it.

#### Function prototype

```c
int i2c_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | I²C device handle            | Input           |
| write\_buffer  | Source buffer                | Input           |
| write\_len     | The number of bytes to write | Input           |
| read\_buffer   | Destination buffer           | Output          |
| read\_len      | Maximum number of bytes read | Input           |

#### Return value

The number of bytes actually read.

### i2c\_config\_as\_slave

#### Description

Configure the I²C controller to be in slave mode.

#### Function prototype

```c
void i2c_config_as_slave(handle_t file, uint32_t slave_address, uint32_t address_width, i2c_slave_handler_t *handler);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I²C controller handle | Input           |
| slave\_address | Slave address         | Input           |
| address\_width | Slave address width   | Input           |
| handler        | Slave device handler  | Input           |

#### Return value

None.

### spi\_dev\_set\_clock\_rate

#### Description

Configure the clock rate for the I²C Slave mode.

#### Function prototype

```c
double i2c_slave_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name |      Description      | Input or output |
| -------------- | --------------------- | --------------- |
| file           | I²C controller handle | Input           |
| clock\_rate    | Expected clock rate   | Input           |

#### Return value

The actual clock rate after setting.

### Example

```c
handle_t i2c = io_open("/dev/i2c0");
/* The i2c peripheral address is 0x32, 7-bit address, rate 200K */
handle_t dev0 = i2c_get_device(i2c, "/dev/i2c0/dev0", 0x32, 7);
i2c_dev_set_clock_rate(dev0, 200000);

uint8_t reg = 0;
uint8_t data_buf[2] = { 0x00,0x01 };
data_buf[0] = reg;
/* Write 0x01 to the 0 register */
io_write(dev0, data_buf, 2);
/* Read 1 byte data from 0 register */
i2c_dev_transfer_sequential(dev0, &reg, 1, data_buf, 1);
```

## Data type

The relevant data types and data structures are defined as follows:

- [i2c\_event\_t](#i2ceventt): I²C event.
- [i2c\_slave\_handler\_t](#i2cslavehandlert): I²C slave device handler.

### i2c\_event\_t

#### Description

I²C event.

#### Type definition

```c
typedef enum _i2c_event
{
    I2C_EV_START,
    I2C_EV_RESTART,
    I2C_EV_STOP
} i2c_event_t;
```

#### Enumeration element

|   Element name   |       Description       |
| ---------------- | ----------------------- |
| I2C\_EV\_START   | Received start signal   |
| I2C\_EV\_RESTART | Received restart signal |
| I2C\_EV\_STOP    | Received stop signal    |

### i2c\_slave\_handler\_t

#### Description

I²C slave device handler.

#### Type definition

```c
typedef struct _i2c_slave_handler
{
    void (*on_receive)(uint32_t data);
    uint32_t (*on_transmit)();
    void (*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### Enumeration element

| Element name |            Description            |
| ------------ | --------------------------------- |
| on\_receive  | Called when data is received      |
| on\_transmit | Called when data needs to be sent |
| on\_event    | Called when an event occurs       |