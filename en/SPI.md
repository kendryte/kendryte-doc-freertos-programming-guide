# SPI

## Overview

The Serial Peripheral Interface (SPI) is a synchronous serial communication interface.
It is a high speed, full duplex, synchronous communication interface.

## Features

The SPI module has the following features:

- Independent SPI device interface with peripheral related parameters
- Automatic processing of multi-device bus contention
- Support standard, two-wire, four-wire, eight-wire mode
- Supports write-before-read and full-duplex read and write
- Supports sending a series of identical data frames, often used for clearing screens, filling storage sectors, etc.

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [spi\_get\_device](#spigetdevice)
- [spi\_dev\_config\_non\_standard](#spidevconfignonstandard)
- [spi\_dev\_set\_clock\_rate](#spidevsetclockrate)
- [spi\_dev\_transfer\_full\_duplex](#spidevtransferfullduplex)
- [spi\_dev\_transfer\_sequential](#spidevtransfersequential)
- [spi\_dev\_fill](#spidevfill)

### spi\_get\_device

#### Description

Register and open an SPI device.

#### Function prototype

```c
handle_t spi_get_device(handle_t file, const char *name, spi_mode mode, spi_frame_format frame_format, uint32_t chip_select_mask, uint32_t data_bit_length);
```

#### Parameter

|   Parameter name   |              Description              | Input or output |
| ------------------ | ------------------------------------- | --------------- |
| file               | SPI controller handle                 | Input           |
| name               | Specify the path to access the device | Input           |
| mode               | SPI mode                              | Input           |
| frame\_format      | Frame format                          | Input           |
| chip\_select\_mask | Chip select mask                      | Input           |
| data\_bit\_length  | Data bit length                       | Input           |

#### Return value

SPI device handle.

### spi\_dev\_config\_non\_standard

#### Description

Configure non-standard frame format parameters for the SPI device.

#### Function prototype

```c
void spi_dev_config_non_standard(handle_t file, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_inst_addr_trans_mode_t trans_mode);
```

#### Parameter

|   Parameter name    |            Description            | Input or output |
| ------------------- | --------------------------------- | --------------- |
| file                | SPI device handle                 | Input           |
| instruction\_length | Instruction length                | Input           |
| address\_length     | Address length                    | Input           |
| wait\_cycles        | Number of waiting cycles          | Input           |
| trans\_mode         | Command and address transfer mode | Input           |

#### Return value

None.

### spi\_dev\_set\_clock\_rate

#### Description

Configure the clock rate of the SPI device.

#### Function prototype

```c
double spi_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name |     Description     | Input or output |
| -------------- | ------------------- | --------------- |
| file           | SPI device handle   | Input           |
| clock\_rate    | Expected clock rate | Input           |

#### Return value

The actual rate after setting.

### spi\_dev\_transfer\_full\_duplex

#### Description

Full-duplex transmission of SPI devices.

**Note:** Only standard frame formats are supported.

#### Function prototype

```c
int spi_dev_transfer_full_duplex(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | SPI device handle            | Input           |
| write\_buffer  | Source buffer                | Input           |
| write\_len     | The number of bytes to write | Input           |
| read\_buffer   | Target buffer                | Output          |
| read\_len      | Maximum number of bytes read | Input           |

#### Return value

The number of bytes actually read.

### spi\_dev\_transfer\_sequential

#### Description

Write the SPI device first and then read it.

**Note:** Only standard frame formats are supported.

#### Function prototype

```c
int spi_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name |         Description          | Input or output |
| -------------- | ---------------------------- | --------------- |
| file           | SPI device handle            | Input           |
| write\_buffer  | Source buffer                | Input           |
| write\_len     | The number of bytes to write | Input           |
| read\_buffer   | Target buffer                | Output          |
| read\_len      | Maximum number of bytes read | Input           |

#### Return value

The number of bytes actually read.

### spi\_dev\_fill

#### Description

Fill the SPI device with a sequence of identical frames.

**Note:** Only standard frame formats are supported.

#### Function prototype

```c
void spi_dev_fill(handle_t file, uint32_t instruction, uint32_t address, uint32_t value, size_t count);
```

#### Parameter

| Parameter name |                  Description                   | Input or output |
| -------------- | ---------------------------------------------- | --------------- |
| file           | SPI device handle                              | Input           |
| instruction    | Instruction (ignored in standard frame format) | Input           |
| address        | Address (ignored in standard frame format)     | Input           |
| value          | Frame data                                     | Output          |
| count          | Number of frames                               | Input           |

#### Return value

None.

### Example

```c
handle_t spi = io_open("/dev/spi0");
/* dev0 works in MODE0 (Standard SPI mode), single transmission, 8-bit data and using chip select 0 */
handle_t dev0 = spi_get_device(spi, "/dev/spi0/dev0", SPI_MODE_0, SPI_FF_STANDARD, 0b1, 8);
uint8_t data_buf[] = { 0x06, 0x01, 0x02, 0x04, 0, 1, 2, 3 };
/* Send instruction 0x06. Send 0,1,2,3 four bytes of data to address 0x010204 */
io_write(dev0, data_buf, sizeof(data_buf));
/* Send instruction 0x06. Receive four bytes of data from address 0x010204 */
spi_dev_transfer_sequential(dev0, data_buf, 4, data_buf, 4);
```

## Data type

The relevant data types and data structures are defined as follows:

- [spi\_mode\_t](#spimodet): SPI mode.
- [spi\_frame\_format\_t](#spiframeformatt): SPI frame format.
- [spi\_inst\_addr\_trans\_mode\_t](#spiinstaddrtransmodet): The transfer mode of the SPI instruction and address.

### spi\_mode\_t

#### Description

SPI mode.

#### Type definition

```c
typedef enum _spi_mode
{
    SPI_MODE_0,
    SPI_MODE_1,
    SPI_MODE_2,
    SPI_MODE_3,
} spi_mode_t;
```

#### Enumeration element

| Element name | Description |
| ------------ | ----------- |
| SPI\_MODE\_0 | SPI mode 0  |
| SPI\_MODE\_1 | SPI mode 1  |
| SPI\_MODE\_2 | SPI mode 2  |
| SPI\_MODE\_3 | SPI mode 3  |

### spi\_frame\_format\_t

#### Description

SPI frame format.

#### Type definition

```c
typedef enum _spi_frame_format
{
    SPI_FF_STANDARD,
    SPI_FF_DUAL,
    SPI_FF_QUAD,
    SPI_FF_OCTAL
} spi_frame_format_t;
```

#### Enumeration element

|   Element name    |                    Description                     |
| ----------------- | -------------------------------------------------- |
| SPI\_FF\_STANDARD | Standard                                           |
| SPI\_FF\_DUAL     | Dual wire (2 wires)                                |
| SPI\_FF\_QUAD     | Duad wire (4 wires)                                |
| SPI\_FF\_OCTAL    | Octal wire (8 wires, `/dev/spi3` is not supported) |

### spi\_inst\_addr\_trans\_mode\_t

#### Description

The transfer mode of the SPI instruction and address.

#### Type definition

```c
typedef enum _spi_inst_addr_trans_mode
{
    SPI_AITM_STANDARD,
    SPI_AITM_ADDR_STANDARD,
    SPI_AITM_AS_FRAME_FORMAT
} spi_inst_addr_trans_mode_t;
```

#### Enumeration element

|         Element name         |                                       Description                                        |
| ---------------------------- | ---------------------------------------------------------------------------------------- |
| SPI\_AITM\_STANDARD          | All use the standard frame format                                                        |
| SPI\_AITM\_ADDR\_STANDARD    | The instruction uses the configured value and the address uses the standard frame format |
| SPI\_AITM\_AS\_FRAME\_FORMAT | All use the configured values                                                            |