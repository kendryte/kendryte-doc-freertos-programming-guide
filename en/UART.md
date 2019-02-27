# 通用异步收发传输器 (UART)

## Overview

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。通用异步收发传输器 (UART) 即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。

## Features

UART 模块具有以下功能：

- 配置 UART 参数
- 自动收取数据到缓冲区

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [uart\_config](#uartconfig)

### uart\_config

#### Description

配置 UART 设备。

#### Function prototype

```c
void uart_config(handle_t file, uint32_t baud_rate, uint32_t databits, uart_stopbits_t stopbits, uart_parity_t parity);
```

#### Parameter

| Parameter name    |   Description       |  Input or output  |
| ---------- | ------------ | --------- |
| file       | UART device handle | Input      |
| baud\_rate | 波特率        | Input      |
| databits   | 数据位 (5-8)  | Input      |
| stopbits   | 停止位        | Input      |
| parity     | 校验位        | Input      |

#### Return value

None.

### Example

```c
handle_t uart = io_open("/dev/uart1");

uint8_t b = 1;
/* 写入 1 个字节 */
io_write(uart, &b, 1);
/* 读取 1 个字节 */
while (io_read(uart, &b, 1) != 1);
```

## Data type

The relevant data types and data structures are defined as follows:

- [uart\_stopbits\_t](#uartstopbitst)：UART 停止位。
- [uart\_parity\_t](#uartparityt)：UART 校验位。

### uart\_stopbits\_t

#### Description

UART 停止位。

#### Type definition

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;  
```

#### Enumeration element

| Element name          | Description        |
| ---------------- | ----------- |
| UART\_STOP\_1    | 1 个停止位   |
| UART\_STOP\_1\_5 | 1.5 个停止位 |
| UART\_STOP\_2    | 2 个停止位   |

### uart\_parity\_t

#### Description

UART 校验位。

#### Type definition

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| UART\_PARITY\_NONE | 无校验位    |
| UART\_PARITY\_ODD  | 奇校验      |
| UART\_PARITY\_EVEN | 偶校验      |