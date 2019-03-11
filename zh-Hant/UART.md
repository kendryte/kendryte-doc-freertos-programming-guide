# 通用非同步收發傳輸器 (UART)

## 概述

嵌入式應用通常要求一個簡單的並且占用系統資源少的方法來傳輸資料。通用非同步收發傳輸器 (UART) 即可以滿足這些要求，它能夠靈活地與外部裝置進行全雙工資料交換。

## 功能描述

UART 模組具有以下功能：

- 配置 UART 參數
- 自動收取資料到緩衝區

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [uart\_config](#uartconfig)

### uart\_config

#### 描述

配置 UART 裝置。

#### 函數原型

```c
void uart_config(handle_t file, uint32_t baud_rate, uint32_t databits, uart_stopbits_t stopbits, uart_parity_t parity);
```

#### 參數

| 參數名稱    |   描述       |  輸入輸出  |
| ---------- | ------------ | --------- |
| file       | UART 裝置句柄 | 輸入      |
| baud\_rate | 波特率        | 輸入      |
| databits   | 資料位 (5-8)  | 輸入      |
| stopbits   | 停止位        | 輸入      |
| parity     | 校驗位        | 輸入      |

#### 返回值

無。

### 舉例

```c
handle_t uart = io_open("/dev/uart1");

uint8_t b = 1;
/* 寫入 1 個位元組 */
io_write(uart, &b, 1);
/* 讀取 1 個位元組 */
while (io_read(uart, &b, 1) != 1);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [uart\_stopbits\_t](#uartstopbitst)：UART 停止位。
- [uart\_parity\_t](#uartparityt)：UART 校驗位。

### uart\_stopbits\_t

#### 描述

UART 停止位。

#### 定義

```c
typedef enum _uart_stopbits
{
    UART_STOP_1,
    UART_STOP_1_5,
    UART_STOP_2
} uart_stopbits_t;  
```

#### 成員

| 成員名稱          | 描述        |
| ---------------- | ----------- |
| UART\_STOP\_1    | 1 個停止位   |
| UART\_STOP\_1\_5 | 1.5 個停止位 |
| UART\_STOP\_2    | 2 個停止位   |

### uart\_parity\_t

#### 描述

UART 校驗位。

#### 定義

```c
typedef enum _uart_parity
{
    UART_PARITY_NONE,
    UART_PARITY_ODD,
    UART_PARITY_EVEN
} uart_parity_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| UART\_PARITY\_NONE | 無校驗位    |
| UART\_PARITY\_ODD  | 奇校驗      |
| UART\_PARITY\_EVEN | 偶校驗      |