# 标准 IO

## Overview

标准 IO 模块是访问外设的基本接口。

## Features

标准 IO 模块具有以下功能：

- 根据路径寻找外设
- 统一的读写和控制接口

## API

对应的头文件 `devices.h`

为用户提供以下接口：

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
| name      | 设备路径    | 输入      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| 0     | 失败    |
| 其他  | 设备句柄 |

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
| file      | 设备句柄    | 输入      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| 0     | 成功    |
| 其他  | 失败    |

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
| file      | 设备句柄        | 输入      |
| buffer    | 目标缓冲区      | 输出      |
| len       | 最多读取的字节数 | 输入      |

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
| file      | 设备句柄      | 输入      |
| buffer    | 源缓冲区      | 输入      |
| len       | 要写入的字节数 | 输入      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| len   | 成功    |
| 其他  | 失败    |

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
| file          | 设备句柄        | 输入      |
| control\_code | 控制码          | 输入      |
| write\_buffer | 源缓冲区        | 输入      |
| write\_len    | 要写入的字节数   | 输入      |
| read\_buffer  | 目标缓冲区      | 输出      |
| read\_len     | 最多读取的字节数 | 输入      |

#### Return value

实际读取的字节数。

### Example

```c
handle_t uart = io_open("/dev/uart1");
io_write(uart, "hello\n", 6);
io_close(uart);
```