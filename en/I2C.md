# 集成电路内置总线 (I2C)

## Overview

I2C 总线用于和多个外部设备进行通信。多个外部设备可以共用一个 I2C 总线。

## Features

I2C 模块具有以下功能:

- 独立的 I2C 设备封装外设相关参数
- 自动处理多设备总线争用
- 支持从模式

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

注册并打开一个 I2C 设备。

#### Function prototype

```c
handle_t i2c_get_device(handle_t file, const char *name, uint32_t slave_address, uint32_t address_width);
```

#### Parameter

| Parameter name          |   Description             |  Input or output  |
| ---------------- | ------------------ | --------- |
| file             | I2C 控制器句柄      | Input      |
| name             | 指定访问该设备的路径 | Input      |
| slave\_address   | 从设备地址          | Input      |
| address\_width   | 从设备地址宽度      | Input      |

#### Return value

I2C 设备句柄。

### i2c\_dev\_set\_clock\_rate

#### Description

配置 I2C 设备的时钟速率。

#### Function prototype

```c
double i2c_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name          |   Description        |  Input or output  |
| ---------------- | ------------- | --------- |
| file             | I2C device handle   | Input       |
| clock\_rate      | 期望的时钟速率 | Input       |

#### Return value

设置后的实际速率。

### i2c\_dev\_transfer\_sequential

#### Description

对 I2C 设备先读后写。

#### Function prototype

```c
int i2c_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name       |   Description         |  Input or output  |
| ------------- | -------------- | --------- |
| file          | I2C device handle    | Input      |
| write\_buffer | 源缓冲区        | Input      |
| write\_len    | 要写入的字节数   | Input      |
| read\_buffer  | 目标缓冲区      | Output      |
| read\_len     | 最多读取的字节数 | Input      |

#### Return value

实际读取的字节数。

### i2c\_config\_as\_slave

#### Description

配置 I2C 控制器为从模式。

#### Function prototype

```c
void i2c_config_as_slave(handle_t file, uint32_t slave_address, uint32_t address_width, i2c_slave_handler_t *handler);
```

#### Parameter

| Parameter name          |   Description        |  Input or output  |
| ---------------- | ------------- | --------- |
| file             | I2C 控制器句柄 | Input       |
| slave\_address   | 从设备地址     | Input       |
| address\_width   | 从设备地址宽度 | Input       |
| handler          | 从设备Handler | Input       |

#### Return value

None.

### spi\_dev\_set\_clock\_rate

#### Description

配置 I2C 从模式的时钟速率。

#### Function prototype

```c
double i2c_slave_set_clock_rate(handle_t file, double clock_rate);
```

#### Parameter

| Parameter name          |   Description        |  Input or output  |
| ---------------- | ------------- | --------- |
| file             | I2C 控制器句柄 | Input       |
| clock\_rate      | 期望的时钟速率 | Input       |

#### Return value

设置后的实际速率。

### Example

```c
handle_t i2c = io_open("/dev/i2c0");
/* i2c外设地址是0x32, 7位地址，速率200K */
handle_t dev0 = i2c_get_device(i2c, "/dev/i2c0/dev0", 0x32, 7);
i2c_dev_set_clock_rate(dev0, 200000);

uint8_t reg = 0;
uint8_t data_buf[2] = { 0x00,0x01 };
data_buf[0] = reg;
/* 向0寄存器写0x01 */
io_write(dev0, data_buf, 2);
/* 从0寄存器读取1字节数据 */
i2c_dev_transfer_sequential(dev0, &reg, 1, data_buf, 1);
```

## Data type

The relevant data types and data structures are defined as follows:

- [i2c\_event\_t](#i2ceventt): I2C 事件。
- [i2c\_slave\_handler\_t](#i2cslavehandlert): I2C 从设备Handler。

### i2c\_event\_t

#### Description

I2C 事件。

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

| Element name            | Description             |
| ------------------ | ---------------- |
| I2C\_EV\_START     | 收到 Start 信号   |
| I2C\_EV\_RESTART   | 收到 Restart 信号 |
| I2C\_EV\_STOP      | 收到 Stop 信号    |

### i2c\_slave\_handler\_t

#### Description

I2C 从设备Handler。

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

| Element name          | Description               |
| ---------------- | ------------------ |
| on\_receive      | 收到数据时被调用     |
| on\_transmit     | 需要发送数据时被调用 |
| on\_event        | 发生事件时被调用     |