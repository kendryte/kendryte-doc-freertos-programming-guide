# UART

## Overview

Universal Asynchronous Receiver/Transmitter (UART).

Embedded applications typically require a simple method that consumes less system resources to transfer data. The Universal Asynchronous Receiver/Transmitter (UART) meets these requirements with the flexibility to perform full-duplex data exchange with external devices.

## Features

The UART module has the following features:

- Configuring UART parameters
- Automatically charge data to the buffer

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [uart\_config](#uartconfig)

### uart\_config

#### Description

Configure the UART device.

#### Function prototype

```c
void uart_config(handle_t file, uint32_t baud_rate, uint32_t databits, uart_stopbits_t stopbits, uart_parity_t parity);
```

#### Parameter

| Parameter name |    Description     | Input or output |
| -------------- | ------------------ | --------------- |
| file           | UART device handle | Input           |
| baud\_rate     | Baud rate          | Input           |
| databits       | Data bits (5-8)    | Input           |
| stopbits       | Stop bit           | Input           |
| parity         | Parity bit         | Input           |

#### Return value

None.

### Example

```c
handle_t uart = io_open("/dev/uart1");

uint8_t b = 1;
/* Write 1 byte */
io_write(uart, &b, 1);
/* Read 1 byte */
while (io_read(uart, &b, 1) != 1);
```

## Data type

The relevant data types and data structures are defined as follows:

- [uart\_stopbits\_t](#uartstopbitst): UART stop bits.
- [uart\_parity\_t](#uartparityt): UART parity bit.

### uart\_stopbits\_t

#### Description

UART stop bits.

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

|   Element name   |  Description  |
| ---------------- | ------------- |
| UART\_STOP\_1    | 1 stop bit    |
| UART\_STOP\_1\_5 | 1.5 stop bits |
| UART\_STOP\_2    | 2 stop bits   |

### uart\_parity\_t

#### Description

UART parity bit.

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

|    Element name    |  Description  |
| ------------------ | ------------- |
| UART\_PARITY\_NONE | No parity bit |
| UART\_PARITY\_ODD  | Odd parity    |
| UART\_PARITY\_EVEN | Even parity   |
