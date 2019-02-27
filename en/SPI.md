# 串行外设接口 (SPI)

## Overview

SPI 是一种高速的，全双工，同步的通信总线。

## Features

SPI 模块具有以下功能:

- 独立的 SPI 设备封装外设相关参数
- 自动处理多设备总线争用
- 支持标准、双线、四线、八线模式
- 支持先写后读和全双工读写
- 支持发送一串相同的数据帧，常用于清屏、填充存储扇区等场景

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

注册并打开一个 SPI 设备。

#### Function prototype

```c
handle_t spi_get_device(handle_t file, const char *name, spi_mode mode, spi_frame_format frame_format, uint32_t chip_select_mask, uint32_t data_bit_length);
```

#### Parameter

| Parameter name            |   Description             |  Input or output  |
| ------------------ | ------------------ | --------- |
| file               | SPI 控制器句柄      | Input       |
| name               | 指定访问该设备的路径 | Input       |
| mode               | SPI 模式            | Input       |
| frame\_format      | 帧格式              | Input       |
| chip\_select\_mask | 片选掩码            | Input       |
| data\_bit\_length  | 数据位长度          | Input       |

#### Return value

SPI 设备句柄。

### spi\_dev\_config\_non\_standard

#### Description

配置 SPI 设备的非标准帧格式参数。

#### Function prototype

```c
void spi_dev_config_non_standard(handle_t file, uint32_t instruction_length, uint32_t address_length, uint32_t wait_cycles, spi_inst_addr_trans_mode_t trans_mode);
```

#### Parameter

| Parameter name             |   Description             |  Input or output  |
| ------------------- | ------------------ | --------- |
| file                | SPI device handle        | Input      |
| instruction\_length | 指令长度            | Input      |
| address\_length     | 地址长度            | Input      |
| wait\_cycles        | 等待周期数          | Input      |
| trans\_mode         | 指令和地址的传输模式 | Input      |

#### Return value

None.

### spi\_dev\_set\_clock\_rate

#### Description

配置 SPI 设备的时钟速率。

#### Function prototype

```c
double spi_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name          |   Description        |  Input or output  |
| ---------------- | ------------- | --------- |
| file             | SPI device handle   | Input       |
| clock\_rate      | 期望的时钟速率 | Input       |

#### Return value

设置后的实际速率。

### spi\_dev\_transfer\_full\_duplex

#### Description

对 SPI 设备进行全双工传输。

**Note:** 仅支持标准帧格式。

#### Function prototype

```c
int spi_dev_transfer_full_duplex(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name          |   Description         |  Input or output  |
| ---------------- | -------------- | --------- |
| file             | SPI device handle    | Input      |
| write\_buffer    | 源缓冲区        | Input      |
| write\_len       | 要写入的字节数   | Input      |
| read\_buffer     | 目标缓冲区       | Output      |
| read\_len        | 最多读取的字节数 | Input      |

#### Return value

实际读取的字节数。

### spi\_dev\_transfer\_sequential

#### Description

对 SPI 设备进行先写后读。

**Note:** 仅支持标准帧格式。

#### Function prototype

```c
int spi_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name          |   Description         |  Input or output  |
| ---------------- | -------------- | --------- |
| file             | SPI device handle    | Input      |
| write\_buffer    | 源缓冲区        | Input      |
| write\_len       | 要写入的字节数   | Input      |
| read\_buffer     | 目标缓冲区       | Output      |
| read\_len        | 最多读取的字节数 | Input      |

#### Return value

实际读取的字节数。

### spi\_dev\_fill

#### Description

对 SPI 设备填充一串相同的帧。

**Note:** 仅支持标准帧格式。

#### Function prototype

```c
void spi_dev_fill(handle_t file, uint32_t instruction, uint32_t address, uint32_t value, size_t count);
```

#### Parameter

| Parameter name          |   Description                 |  Input or output  |
| ---------------- | ---------------------- | --------- |
| file             | SPI device handle            | Input      |
| instruction      | 指令（标准帧格式下忽略） | Input      |
| address          | 地址（标准帧格式下忽略） | Input      |
| value            | 帧数据                 | Output      |
| count            | 帧数                   | Input      |

#### Return value

None.

### Example

```c
handle_t spi = io_open("/dev/spi0");
/* dev0 工作在 MODE0 模式 标准 SPI 模式 单次发送 8 位数据 使用片选 0 */
handle_t dev0 = spi_get_device(spi, "/dev/spi0/dev0", SPI_MODE_0, SPI_FF_STANDARD, 0b1, 8);
uint8_t data_buf[] = { 0x06, 0x01, 0x02, 0x04, 0, 1, 2, 3 };
/* 发送指令 0x06 向地址 0x010204 发送 0，1，2，3 四个字节数据 */
io_write(dev0, data_buf, sizeof(data_buf));
/* 发送指令 0x06 地址 0x010204 接收四个字节的数据 */
spi_dev_transfer_sequential(dev0, data_buf, 4, data_buf, 4);
```

## Data type

The relevant data types and data structures are defined as follows:

- [spi\_mode\_t](#spimodet): SPI 模式。
- [spi\_frame\_format\_t](#spiframeformatt): SPI 帧格式。
- [spi\_inst\_addr\_trans\_mode\_t](#spiinstaddrtransmodet): SPI 指令和地址的传输模式。

### spi\_mode\_t

#### Description

SPI 模式。

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

| Element name       | Description        |
| ------------- | ----------- |
| SPI\_MODE\_0  | SPI 模式 0  |
| SPI\_MODE\_1  | SPI 模式 1  |
| SPI\_MODE\_2  | SPI 模式 2  |
| SPI\_MODE\_3  | SPI 模式 3  |

### spi\_frame\_format\_t

#### Description

SPI 帧格式。

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

| Element name            | Description                      |
| ------------------ | ------------------------- |
| SPI\_FF\_STANDARD  | 标准                      |
| SPI\_FF\_DUAL      | 双线                      |
| SPI\_FF\_QUAD      | 四线                      |
| SPI\_FF\_OCTAL     | 八线（`/dev/spi3` 不支持） |

### spi\_inst\_addr\_trans\_mode\_t

#### Description

SPI 指令和地址的传输模式。

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

| Element name                      | Description               |
| ---------------------------- | ------------------ |
| SPI\_AITM\_STANDARD          | 均使用标准帧格式     |
| SPI\_AITM\_ADDR\_STANDARD    | 指令使用配置的值，地址使用标准帧格式 |
| SPI\_AITM\_AS\_FRAME\_FORMAT | 均使用配置的值     |