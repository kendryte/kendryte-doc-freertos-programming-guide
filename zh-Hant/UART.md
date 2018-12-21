# 通用异步收发传输器 (UART)

## 概述

嵌入式应用通常要求一个简单的并且占用系统资源少的方法来传输数据。通用异步收发传输器 (UART) 即可以满足这些要求，它能够灵活地与外部设备进行全双工数据交换。

## 功能描述

UART 模块具有以下功能：

- 配置 UART 参数
- 自动收取数据到缓冲区

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

- [uart\_config](#uartconfig)

### uart\_config

#### 描述

配置 UART 设备。

#### 函数原型

```c
void uart_config(handle_t file, uint32_t baud_rate, uint32_t databits, uart_stopbits_t stopbits, uart_parity_t parity);
```

#### 参数

| 参数名称    |   描述       |  输入输出  |
| ---------- | ------------ | --------- |
| file       | UART 设备句柄 | 输入      |
| baud\_rate | 波特率        | 输入      |
| databits   | 数据位 (5-8)  | 输入      |
| stopbits   | 停止位        | 输入      |
| parity     | 校验位        | 输入      |

#### 返回值

无。

### 举例

```c
handle_t uart = io_open("/dev/uart1");

uint8_t b = 1;
/* 写入 1 个字节 */
io_write(uart, &b, 1);
/* 读取 1 个字节 */
while (io_read(uart, &b, 1) != 1);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [uart\_stopbits\_t](#uartstopbitst)：UART 停止位。
- [uart\_parity\_t](#uartparityt)：UART 校验位。

### uart\_stopbits\_t

#### 描述

UART 停止位。

#### 定义

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;  
```

#### 成员

| 成员名称          | 描述        |
| ---------------- | ----------- |
| UART\_STOP\_1    | 1 个停止位   |
| UART\_STOP\_1\_5 | 1.5 个停止位 |
| UART\_STOP\_2    | 2 个停止位   |

### uart\_parity\_t

#### 描述

UART 校验位。

#### 定义

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| UART\_PARITY\_NONE | 无校验位    |
| UART\_PARITY\_ODD  | 奇校验      |
| UART\_PARITY\_EVEN | 偶校验      |