# 标准 IO

## Overview

标准 IO 模块是访问外设的基本接口。

## Features

标准 IO 模块具有以下功能：

- 根据路径寻找外设
- 统一的读写和控制接口

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

打开一个设备。

#### Function prototype

```c
handle_t io_open(const char *name);
```

#### Parameter

| Parameter name   |   Description     |  Input or output  |
| --------- | ---------- | --------- |
| name      | 设备路径    | Input      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| 0     | Fail    |
| 其他  | device handle |

### io\_close

#### Description

关闭一个设备。

#### Function prototype

```c
int io_close(handle_t file);
```

#### Parameter

| Parameter name   |   Description     |  Input or output  |
| --------- | ---------- | --------- |
| file      | device handle    | Input      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| 0     | Success    |
| 其他  | Fail    |

### io\_read

#### Description

从设备读取。

#### Function prototype

```c
int io_read(handle_t file, uint8_t *buffer, size_t len);
```

#### Parameter

| Parameter name   |   Description         |  Input or output  |
| --------- | -------------- | --------- |
| file      | device handle        | Input      |
| buffer    | 目标缓冲区      | Output      |
| len       | 最多读取的字节数 | Input      |

#### Return value

实际读取的字节数。

### io\_write

#### Description

向设备写入。

#### Function prototype

```c
int io_write(handle_t file, const uint8_t *buffer, size_t len);
```

#### Parameter

| Parameter name   |   Description       |  Input or output  |
| --------- | ------------ | --------- |
| file      | device handle      | Input      |
| buffer    | 源缓冲区      | Input      |
| len       | 要写入的字节数 | Input      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| len   | Success    |
| 其他  | Fail    |

### io\_control

#### Description

向设备发送控制信息。

#### Function prototype

```c
int io_control(handle_t file, uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### Parameter

| Parameter name       |   Description         |  Input or output  |
| ------------- | -------------- | --------- |
| file          | device handle        | Input      |
| control\_code | 控制码          | Input      |
| write\_buffer | 源缓冲区        | Input      |
| write\_len    | 要写入的字节数   | Input      |
| read\_buffer  | 目标缓冲区      | Output      |
| read\_len     | 最多读取的字节数 | Input      |

#### Return value

实际读取的字节数。

### Example

```c
handle_t uart = io_open("/dev/uart1");
io_write(uart, "hello\n", 6);
io_close(uart);
```