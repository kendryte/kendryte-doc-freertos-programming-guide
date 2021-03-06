# 管脚配置

## 概述

管脚配置包含 FPIOA 和电源域配置等。

## 功能描述

- 支持 IO 的可编程功能选择
- 配置电源域

## 数据类型

对应的头文件 `pin_cfg.h`

相关数据类型、数据结构定义如下：

- [fpioa\_function\_t](#fpioafunctiont)：管脚的功能编号。
- [fpioa\_cfg\_item\_t](#fpioacfgitemt)：FPIOA 管脚配置。
- [fpioa\_cfg\_t](#fpioacfgt)：FPIOA 配置。
- [sysctl\_power\_bank\_t](#sysctlpowerbankt)：电源域编号。
- [sysctl\_io\_power\_mode\_t](#sysctlpowerbankt)：IO 输出电压值。
- [power\_bank\_item\_t](#powerbankitemt)：单个电源域配置。
- [power\_bank\_cfg\_t](#powerbankcfgt)：电源域配置。
- [pin\_cfg\_t](#pincfgt)：管脚配置。

### fpioa\_function\_t

#### 描述

管脚的功能编号。

#### 定义

```c
typedef enum _fpioa_function
{
    FUNC_JTAG_TCLK        = 0,      /*!< JTAG Test Clock */
    FUNC_JTAG_TDI         = 1,      /*!< JTAG Test Data In */
    FUNC_JTAG_TMS         = 2,      /*!< JTAG Test Mode Select */
    FUNC_JTAG_TDO         = 3,      /*!< JTAG Test Data Out */
    FUNC_SPI0_D0          = 4,      /*!< SPI0 Data 0 */
    FUNC_SPI0_D1          = 5,      /*!< SPI0 Data 1 */
    FUNC_SPI0_D2          = 6,      /*!< SPI0 Data 2 */
    FUNC_SPI0_D3          = 7,      /*!< SPI0 Data 3 */
    FUNC_SPI0_D4          = 8,      /*!< SPI0 Data 4 */
    FUNC_SPI0_D5          = 9,      /*!< SPI0 Data 5 */
    FUNC_SPI0_D6          = 10,     /*!< SPI0 Data 6 */
    FUNC_SPI0_D7          = 11,     /*!< SPI0 Data 7 */
    FUNC_SPI0_SS0         = 12,     /*!< SPI0 Chip Select 0 */
    FUNC_SPI0_SS1         = 13,     /*!< SPI0 Chip Select 1 */
    FUNC_SPI0_SS2         = 14,     /*!< SPI0 Chip Select 2 */
    FUNC_SPI0_SS3         = 15,     /*!< SPI0 Chip Select 3 */
    FUNC_SPI0_ARB         = 16,     /*!< SPI0 Arbitration */
    FUNC_SPI0_SCLK        = 17,     /*!< SPI0 Serial Clock */
    FUNC_UARTHS_RX        = 18,     /*!< UART High speed Receiver */
    FUNC_UARTHS_TX        = 19,     /*!< UART High speed Transmitter */
    FUNC_CLK_IN1          = 20,     /*!< Clock Input 1 */
    FUNC_CLK_IN2          = 21,     /*!< Clock Input 2 */
    FUNC_CLK_SPI1         = 22,     /*!< Clock SPI1 */
    FUNC_CLK_I2C1         = 23,     /*!< Clock I2C1 */
    FUNC_GPIOHS0          = 24,     /*!< GPIO High speed 0 */
    FUNC_GPIOHS1          = 25,     /*!< GPIO High speed 1 */
    FUNC_GPIOHS2          = 26,     /*!< GPIO High speed 2 */
    FUNC_GPIOHS3          = 27,     /*!< GPIO High speed 3 */
    FUNC_GPIOHS4          = 28,     /*!< GPIO High speed 4 */
    FUNC_GPIOHS5          = 29,     /*!< GPIO High speed 5 */
    FUNC_GPIOHS6          = 30,     /*!< GPIO High speed 6 */
    FUNC_GPIOHS7          = 31,     /*!< GPIO High speed 7 */
    FUNC_GPIOHS8          = 32,     /*!< GPIO High speed 8 */
    FUNC_GPIOHS9          = 33,     /*!< GPIO High speed 9 */
    FUNC_GPIOHS10         = 34,     /*!< GPIO High speed 10 */
    FUNC_GPIOHS11         = 35,     /*!< GPIO High speed 11 */
    FUNC_GPIOHS12         = 36,     /*!< GPIO High speed 12 */
    FUNC_GPIOHS13         = 37,     /*!< GPIO High speed 13 */
    FUNC_GPIOHS14         = 38,     /*!< GPIO High speed 14 */
    FUNC_GPIOHS15         = 39,     /*!< GPIO High speed 15 */
    FUNC_GPIOHS16         = 40,     /*!< GPIO High speed 16 */
    FUNC_GPIOHS17         = 41,     /*!< GPIO High speed 17 */
    FUNC_GPIOHS18         = 42,     /*!< GPIO High speed 18 */
    FUNC_GPIOHS19         = 43,     /*!< GPIO High speed 19 */
    FUNC_GPIOHS20         = 44,     /*!< GPIO High speed 20 */
    FUNC_GPIOHS21         = 45,     /*!< GPIO High speed 21 */
    FUNC_GPIOHS22         = 46,     /*!< GPIO High speed 22 */
    FUNC_GPIOHS23         = 47,     /*!< GPIO High speed 23 */
    FUNC_GPIOHS24         = 48,     /*!< GPIO High speed 24 */
    FUNC_GPIOHS25         = 49,     /*!< GPIO High speed 25 */
    FUNC_GPIOHS26         = 50,     /*!< GPIO High speed 26 */
    FUNC_GPIOHS27         = 51,     /*!< GPIO High speed 27 */
    FUNC_GPIOHS28         = 52,     /*!< GPIO High speed 28 */
    FUNC_GPIOHS29         = 53,     /*!< GPIO High speed 29 */
    FUNC_GPIOHS30         = 54,     /*!< GPIO High speed 30 */
    FUNC_GPIOHS31         = 55,     /*!< GPIO High speed 31 */
    FUNC_GPIO0            = 56,     /*!< GPIO pin 0 */
    FUNC_GPIO1            = 57,     /*!< GPIO pin 1 */
    FUNC_GPIO2            = 58,     /*!< GPIO pin 2 */
    FUNC_GPIO3            = 59,     /*!< GPIO pin 3 */
    FUNC_GPIO4            = 60,     /*!< GPIO pin 4 */
    FUNC_GPIO5            = 61,     /*!< GPIO pin 5 */
    FUNC_GPIO6            = 62,     /*!< GPIO pin 6 */
    FUNC_GPIO7            = 63,     /*!< GPIO pin 7 */
    FUNC_UART1_RX         = 64,     /*!< UART1 Receiver */
    FUNC_UART1_TX         = 65,     /*!< UART1 Transmitter */
    FUNC_UART2_RX         = 66,     /*!< UART2 Receiver */
    FUNC_UART2_TX         = 67,     /*!< UART2 Transmitter */
    FUNC_UART3_RX         = 68,     /*!< UART3 Receiver */
    FUNC_UART3_TX         = 69,     /*!< UART3 Transmitter */
    FUNC_SPI1_D0          = 70,     /*!< SPI1 Data 0 */
    FUNC_SPI1_D1          = 71,     /*!< SPI1 Data 1 */
    FUNC_SPI1_D2          = 72,     /*!< SPI1 Data 2 */
    FUNC_SPI1_D3          = 73,     /*!< SPI1 Data 3 */
    FUNC_SPI1_D4          = 74,     /*!< SPI1 Data 4 */
    FUNC_SPI1_D5          = 75,     /*!< SPI1 Data 5 */
    FUNC_SPI1_D6          = 76,     /*!< SPI1 Data 6 */
    FUNC_SPI1_D7          = 77,     /*!< SPI1 Data 7 */
    FUNC_SPI1_SS0         = 78,     /*!< SPI1 Chip Select 0 */
    FUNC_SPI1_SS1         = 79,     /*!< SPI1 Chip Select 1 */
    FUNC_SPI1_SS2         = 80,     /*!< SPI1 Chip Select 2 */
    FUNC_SPI1_SS3         = 81,     /*!< SPI1 Chip Select 3 */
    FUNC_SPI1_ARB         = 82,     /*!< SPI1 Arbitration */
    FUNC_SPI1_SCLK        = 83,     /*!< SPI1 Serial Clock */
    FUNC_SPI_SLAVE_D0     = 84,     /*!< SPI Slave Data 0 */
    FUNC_SPI_SLAVE_SS     = 85,     /*!< SPI Slave Select */
    FUNC_SPI_SLAVE_SCLK   = 86,     /*!< SPI Slave Serial Clock */
    FUNC_I2S0_MCLK        = 87,     /*!< I2S0 Master Clock */
    FUNC_I2S0_SCLK        = 88,     /*!< I2S0 Serial Clock(BCLK) */
    FUNC_I2S0_WS          = 89,     /*!< I2S0 Word Select(LRCLK) */
    FUNC_I2S0_IN_D0       = 90,     /*!< I2S0 Serial Data Input 0 */
    FUNC_I2S0_IN_D1       = 91,     /*!< I2S0 Serial Data Input 1 */
    FUNC_I2S0_IN_D2       = 92,     /*!< I2S0 Serial Data Input 2 */
    FUNC_I2S0_IN_D3       = 93,     /*!< I2S0 Serial Data Input 3 */
    FUNC_I2S0_OUT_D0      = 94,     /*!< I2S0 Serial Data Output 0 */
    FUNC_I2S0_OUT_D1      = 95,     /*!< I2S0 Serial Data Output 1 */
    FUNC_I2S0_OUT_D2      = 96,     /*!< I2S0 Serial Data Output 2 */
    FUNC_I2S0_OUT_D3      = 97,     /*!< I2S0 Serial Data Output 3 */
    FUNC_I2S1_MCLK        = 98,     /*!< I2S1 Master Clock */
    FUNC_I2S1_SCLK        = 99,     /*!< I2S1 Serial Clock(BCLK) */
    FUNC_I2S1_WS          = 100,    /*!< I2S1 Word Select(LRCLK) */
    FUNC_I2S1_IN_D0       = 101,    /*!< I2S1 Serial Data Input 0 */
    FUNC_I2S1_IN_D1       = 102,    /*!< I2S1 Serial Data Input 1 */
    FUNC_I2S1_IN_D2       = 103,    /*!< I2S1 Serial Data Input 2 */
    FUNC_I2S1_IN_D3       = 104,    /*!< I2S1 Serial Data Input 3 */
    FUNC_I2S1_OUT_D0      = 105,    /*!< I2S1 Serial Data Output 0 */
    FUNC_I2S1_OUT_D1      = 106,    /*!< I2S1 Serial Data Output 1 */
    FUNC_I2S1_OUT_D2      = 107,    /*!< I2S1 Serial Data Output 2 */
    FUNC_I2S1_OUT_D3      = 108,    /*!< I2S1 Serial Data Output 3 */
    FUNC_I2S2_MCLK        = 109,    /*!< I2S2 Master Clock */
    FUNC_I2S2_SCLK        = 110,    /*!< I2S2 Serial Clock(BCLK) */
    FUNC_I2S2_WS          = 111,    /*!< I2S2 Word Select(LRCLK) */
    FUNC_I2S2_IN_D0       = 112,    /*!< I2S2 Serial Data Input 0 */
    FUNC_I2S2_IN_D1       = 113,    /*!< I2S2 Serial Data Input 1 */
    FUNC_I2S2_IN_D2       = 114,    /*!< I2S2 Serial Data Input 2 */
    FUNC_I2S2_IN_D3       = 115,    /*!< I2S2 Serial Data Input 3 */
    FUNC_I2S2_OUT_D0      = 116,    /*!< I2S2 Serial Data Output 0 */
    FUNC_I2S2_OUT_D1      = 117,    /*!< I2S2 Serial Data Output 1 */
    FUNC_I2S2_OUT_D2      = 118,    /*!< I2S2 Serial Data Output 2 */
    FUNC_I2S2_OUT_D3      = 119,    /*!< I2S2 Serial Data Output 3 */
    FUNC_RESV0            = 120,    /*!< Reserved function */
    FUNC_RESV1            = 121,    /*!< Reserved function */
    FUNC_RESV2            = 122,    /*!< Reserved function */
    FUNC_RESV3            = 123,    /*!< Reserved function */
    FUNC_RESV4            = 124,    /*!< Reserved function */
    FUNC_RESV5            = 125,    /*!< Reserved function */
    FUNC_I2C0_SCLK        = 126,    /*!< I2C0 Serial Clock */
    FUNC_I2C0_SDA         = 127,    /*!< I2C0 Serial Data */
    FUNC_I2C1_SCLK        = 128,    /*!< I2C1 Serial Clock */
    FUNC_I2C1_SDA         = 129,    /*!< I2C1 Serial Data */
    FUNC_I2C2_SCLK        = 130,    /*!< I2C2 Serial Clock */
    FUNC_I2C2_SDA         = 131,    /*!< I2C2 Serial Data */
    FUNC_CMOS_XCLK        = 132,    /*!< DVP System Clock */
    FUNC_CMOS_RST         = 133,    /*!< DVP System Reset */
    FUNC_CMOS_PWND        = 134,    /*!< DVP Power Down Mode */
    FUNC_CMOS_VSYNC       = 135,    /*!< DVP Vertical Sync */
    FUNC_CMOS_HREF        = 136,    /*!< DVP Horizontal Reference output */
    FUNC_CMOS_PCLK        = 137,    /*!< Pixel Clock */
    FUNC_CMOS_D0          = 138,    /*!< Data Bit 0 */
    FUNC_CMOS_D1          = 139,    /*!< Data Bit 1 */
    FUNC_CMOS_D2          = 140,    /*!< Data Bit 2 */
    FUNC_CMOS_D3          = 141,    /*!< Data Bit 3 */
    FUNC_CMOS_D4          = 142,    /*!< Data Bit 4 */
    FUNC_CMOS_D5          = 143,    /*!< Data Bit 5 */
    FUNC_CMOS_D6          = 144,    /*!< Data Bit 6 */
    FUNC_CMOS_D7          = 145,    /*!< Data Bit 7 */
    FUNC_SCCB_SCLK        = 146,    /*!< SCCB Serial Clock */
    FUNC_SCCB_SDA         = 147,    /*!< SCCB Serial Data */
    FUNC_UART1_CTS        = 148,    /*!< UART1 Clear To Send */
    FUNC_UART1_DSR        = 149,    /*!< UART1 Data Set Ready */
    FUNC_UART1_DCD        = 150,    /*!< UART1 Data Carrier Detect */
    FUNC_UART1_RI         = 151,    /*!< UART1 Ring Indicator */
    FUNC_UART1_SIR_IN     = 152,    /*!< UART1 Serial Infrared Input */
    FUNC_UART1_DTR        = 153,    /*!< UART1 Data Terminal Ready */
    FUNC_UART1_RTS        = 154,    /*!< UART1 Request To Send */
    FUNC_UART1_OUT2       = 155,    /*!< UART1 User-designated Output 2 */
    FUNC_UART1_OUT1       = 156,    /*!< UART1 User-designated Output 1 */
    FUNC_UART1_SIR_OUT    = 157,    /*!< UART1 Serial Infrared Output */
    FUNC_UART1_BAUD       = 158,    /*!< UART1 Transmit Clock Output */
    FUNC_UART1_RE         = 159,    /*!< UART1 Receiver Output Enable */
    FUNC_UART1_DE         = 160,    /*!< UART1 Driver Output Enable */
    FUNC_UART1_RS485_EN   = 161,    /*!< UART1 RS485 Enable */
    FUNC_UART2_CTS        = 162,    /*!< UART2 Clear To Send */
    FUNC_UART2_DSR        = 163,    /*!< UART2 Data Set Ready */
    FUNC_UART2_DCD        = 164,    /*!< UART2 Data Carrier Detect */
    FUNC_UART2_RI         = 165,    /*!< UART2 Ring Indicator */
    FUNC_UART2_SIR_IN     = 166,    /*!< UART2 Serial Infrared Input */
    FUNC_UART2_DTR        = 167,    /*!< UART2 Data Terminal Ready */
    FUNC_UART2_RTS        = 168,    /*!< UART2 Request To Send */
    FUNC_UART2_OUT2       = 169,    /*!< UART2 User-designated Output 2 */
    FUNC_UART2_OUT1       = 170,    /*!< UART2 User-designated Output 1 */
    FUNC_UART2_SIR_OUT    = 171,    /*!< UART2 Serial Infrared Output */
    FUNC_UART2_BAUD       = 172,    /*!< UART2 Transmit Clock Output */
    FUNC_UART2_RE         = 173,    /*!< UART2 Receiver Output Enable */
    FUNC_UART2_DE         = 174,    /*!< UART2 Driver Output Enable */
    FUNC_UART2_RS485_EN   = 175,    /*!< UART2 RS485 Enable */
    FUNC_UART3_CTS        = 176,    /*!< UART3 Clear To Send */
    FUNC_UART3_DSR        = 177,    /*!< UART3 Data Set Ready */
    FUNC_UART3_DCD        = 178,    /*!< UART3 Data Carrier Detect */
    FUNC_UART3_RI         = 179,    /*!< UART3 Ring Indicator */
    FUNC_UART3_SIR_IN     = 180,    /*!< UART3 Serial Infrared Input */
    FUNC_UART3_DTR        = 181,    /*!< UART3 Data Terminal Ready */
    FUNC_UART3_RTS        = 182,    /*!< UART3 Request To Send */
    FUNC_UART3_OUT2       = 183,    /*!< UART3 User-designated Output 2 */
    FUNC_UART3_OUT1       = 184,    /*!< UART3 User-designated Output 1 */
    FUNC_UART3_SIR_OUT    = 185,    /*!< UART3 Serial Infrared Output */
    FUNC_UART3_BAUD       = 186,    /*!< UART3 Transmit Clock Output */
    FUNC_UART3_RE         = 187,    /*!< UART3 Receiver Output Enable */
    FUNC_UART3_DE         = 188,    /*!< UART3 Driver Output Enable */
    FUNC_UART3_RS485_EN   = 189,    /*!< UART3 RS485 Enable */
    FUNC_TIMER0_TOGGLE1   = 190,    /*!< TIMER0 Toggle Output 1 */
    FUNC_TIMER0_TOGGLE2   = 191,    /*!< TIMER0 Toggle Output 2 */
    FUNC_TIMER0_TOGGLE3   = 192,    /*!< TIMER0 Toggle Output 3 */
    FUNC_TIMER0_TOGGLE4   = 193,    /*!< TIMER0 Toggle Output 4 */
    FUNC_TIMER1_TOGGLE1   = 194,    /*!< TIMER1 Toggle Output 1 */
    FUNC_TIMER1_TOGGLE2   = 195,    /*!< TIMER1 Toggle Output 2 */
    FUNC_TIMER1_TOGGLE3   = 196,    /*!< TIMER1 Toggle Output 3 */
    FUNC_TIMER1_TOGGLE4   = 197,    /*!< TIMER1 Toggle Output 4 */
    FUNC_TIMER2_TOGGLE1   = 198,    /*!< TIMER2 Toggle Output 1 */
    FUNC_TIMER2_TOGGLE2   = 199,    /*!< TIMER2 Toggle Output 2 */
    FUNC_TIMER2_TOGGLE3   = 200,    /*!< TIMER2 Toggle Output 3 */
    FUNC_TIMER2_TOGGLE4   = 201,    /*!< TIMER2 Toggle Output 4 */
    FUNC_CLK_SPI2         = 202,    /*!< Clock SPI2 */
    FUNC_CLK_I2C2         = 203,    /*!< Clock I2C2 */
    FUNC_INTERNAL0        = 204,    /*!< Internal function signal 0 */
    FUNC_INTERNAL1        = 205,    /*!< Internal function signal 1 */
    FUNC_INTERNAL2        = 206,    /*!< Internal function signal 2 */
    FUNC_INTERNAL3        = 207,    /*!< Internal function signal 3 */
    FUNC_INTERNAL4        = 208,    /*!< Internal function signal 4 */
    FUNC_INTERNAL5        = 209,    /*!< Internal function signal 5 */
    FUNC_INTERNAL6        = 210,    /*!< Internal function signal 6 */
    FUNC_INTERNAL7        = 211,    /*!< Internal function signal 7 */
    FUNC_INTERNAL8        = 212,    /*!< Internal function signal 8 */
    FUNC_INTERNAL9        = 213,    /*!< Internal function signal 9 */
    FUNC_INTERNAL10       = 214,    /*!< Internal function signal 10 */
    FUNC_INTERNAL11       = 215,    /*!< Internal function signal 11 */
    FUNC_INTERNAL12       = 216,    /*!< Internal function signal 12 */
    FUNC_INTERNAL13       = 217,    /*!< Internal function signal 13 */
    FUNC_INTERNAL14       = 218,    /*!< Internal function signal 14 */
    FUNC_INTERNAL15       = 219,    /*!< Internal function signal 15 */
    FUNC_INTERNAL16       = 220,    /*!< Internal function signal 16 */
    FUNC_INTERNAL17       = 221,    /*!< Internal function signal 17 */
    FUNC_CONSTANT         = 222,    /*!< Constant function */
    FUNC_INTERNAL18       = 223,    /*!< Internal function signal 18 */
    FUNC_DEBUG0           = 224,    /*!< Debug function 0 */
    FUNC_DEBUG1           = 225,    /*!< Debug function 1 */
    FUNC_DEBUG2           = 226,    /*!< Debug function 2 */
    FUNC_DEBUG3           = 227,    /*!< Debug function 3 */
    FUNC_DEBUG4           = 228,    /*!< Debug function 4 */
    FUNC_DEBUG5           = 229,    /*!< Debug function 5 */
    FUNC_DEBUG6           = 230,    /*!< Debug function 6 */
    FUNC_DEBUG7           = 231,    /*!< Debug function 7 */
    FUNC_DEBUG8           = 232,    /*!< Debug function 8 */
    FUNC_DEBUG9           = 233,    /*!< Debug function 9 */
    FUNC_DEBUG10          = 234,    /*!< Debug function 10 */
    FUNC_DEBUG11          = 235,    /*!< Debug function 11 */
    FUNC_DEBUG12          = 236,    /*!< Debug function 12 */
    FUNC_DEBUG13          = 237,    /*!< Debug function 13 */
    FUNC_DEBUG14          = 238,    /*!< Debug function 14 */
    FUNC_DEBUG15          = 239,    /*!< Debug function 15 */
    FUNC_DEBUG16          = 240,    /*!< Debug function 16 */
    FUNC_DEBUG17          = 241,    /*!< Debug function 17 */
    FUNC_DEBUG18          = 242,    /*!< Debug function 18 */
    FUNC_DEBUG19          = 243,    /*!< Debug function 19 */
    FUNC_DEBUG20          = 244,    /*!< Debug function 20 */
    FUNC_DEBUG21          = 245,    /*!< Debug function 21 */
    FUNC_DEBUG22          = 246,    /*!< Debug function 22 */
    FUNC_DEBUG23          = 247,    /*!< Debug function 23 */
    FUNC_DEBUG24          = 248,    /*!< Debug function 24 */
    FUNC_DEBUG25          = 249,    /*!< Debug function 25 */
    FUNC_DEBUG26          = 250,    /*!< Debug function 26 */
    FUNC_DEBUG27          = 251,    /*!< Debug function 27 */
    FUNC_DEBUG28          = 252,    /*!< Debug function 28 */
    FUNC_DEBUG29          = 253,    /*!< Debug function 29 */
    FUNC_DEBUG30          = 254,    /*!< Debug function 30 */
    FUNC_DEBUG31          = 255,    /*!< Debug function 31 */
    FUNC_MAX              = 256,    /*!< Function numbers */
} fpioa_function_t;
```

#### 成员

|        成员名称        |          描述           |
| :--------------------- | :---------------------- |
| FUNC\_JTAG\_TCLK       | JTAG时钟接口            |
| FUNC\_JTAG\_TDI        | JTAG数据输入接口        |
| FUNC\_JTAG\_TMS        | JTAG控制TAP状态机的转换 |
| FUNC\_JTAG\_TDO        | JTAG数据输出接口        |
| FUNC\_SPI0\_D0         | SPI0数据线0             |
| FUNC\_SPI0\_D1         | SPI0数据线1             |
| FUNC\_SPI0\_D2         | SPI0数据线2             |
| FUNC\_SPI0\_D3         | SPI0数据线3             |
| FUNC\_SPI0\_D4         | SPI0数据线4             |
| FUNC\_SPI0\_D5         | SPI0数据线5             |
| FUNC\_SPI0\_D6         | SPI0数据线6             |
| FUNC\_SPI0\_D7         | SPI0数据线7             |
| FUNC\_SPI0\_SS0        | SPI0片选信号0           |
| FUNC\_SPI0\_SS1        | SPI0片选信号1           |
| FUNC\_SPI0\_SS2        | SPI0片选信号2           |
| FUNC\_SPI0\_SS3        | SPI0片选信号3           |
| FUNC\_SPI0\_ARB        | SPI0仲裁信号            |
| FUNC\_SPI0\_SCLK       | SPI0时钟                |
| FUNC\_UARTHS\_RX       | UART高速接收数据接口    |
| FUNC\_UARTHS\_TX       | UART高速发送数据接口    |
| FUNC\_RESV6            | 保留功能                |
| FUNC\_RESV7            | 保留功能                |
| FUNC\_CLK\_SPI1        | SPI1时钟                |
| FUNC\_CLK\_I2C1        | I2C1时钟                |
| FUNC\_GPIOHS0          | 高速GPIO0               |
| FUNC\_GPIOHS1          | 高速GPIO1               |
| FUNC\_GPIOHS2          | 高速GPIO2               |
| FUNC\_GPIOHS3          | 高速GPIO3               |
| FUNC\_GPIOHS4          | 高速GPIO4               |
| FUNC\_GPIOHS5          | 高速GPIO5               |
| FUNC\_GPIOHS6          | 高速GPIO6               |
| FUNC\_GPIOHS7          | 高速GPIO7               |
| FUNC\_GPIOHS8          | 高速GPIO8               |
| FUNC\_GPIOHS9          | 高速GPIO9               |
| FUNC\_GPIOHS10         | 高速GPIO10              |
| FUNC\_GPIOHS11         | 高速GPIO11              |
| FUNC\_GPIOHS12         | 高速GPIO12              |
| FUNC\_GPIOHS13         | 高速GPIO13              |
| FUNC\_GPIOHS14         | 高速GPIO14              |
| FUNC\_GPIOHS15         | 高速GPIO15              |
| FUNC\_GPIOHS16         | 高速GPIO16              |
| FUNC\_GPIOHS17         | 高速GPIO17              |
| FUNC\_GPIOHS18         | 高速GPIO18              |
| FUNC\_GPIOHS19         | 高速GPIO19              |
| FUNC\_GPIOHS20         | 高速GPIO20              |
| FUNC\_GPIOHS21         | 高速GPIO21              |
| FUNC\_GPIOHS22         | 高速GPIO22              |
| FUNC\_GPIOHS23         | 高速GPIO23              |
| FUNC\_GPIOHS24         | 高速GPIO24              |
| FUNC\_GPIOHS25         | 高速GPIO25              |
| FUNC\_GPIOHS26         | 高速GPIO26              |
| FUNC\_GPIOHS27         | 高速GPIO27              |
| FUNC\_GPIOHS28         | 高速GPIO28              |
| FUNC\_GPIOHS29         | 高速GPIO29              |
| FUNC\_GPIOHS30         | 高速GPIO30              |
| FUNC\_GPIOHS31         | 高速GPIO31              |
| FUNC\_GPIO0            | GPIO0                   |
| FUNC\_GPIO1            | GPIO1                   |
| FUNC\_GPIO2            | GPIO2                   |
| FUNC\_GPIO3            | GPIO3                   |
| FUNC\_GPIO4            | GPIO4                   |
| FUNC\_GPIO5            | GPIO5                   |
| FUNC\_GPIO6            | GPIO6                   |
| FUNC\_GPIO7            | GPIO7                   |
| FUNC\_UART1\_RX        | UART1接收数据接口       |
| FUNC\_UART1\_TX        | UART1发送数据接口       |
| FUNC\_UART2\_RX        | UART2接收数据接口       |
| FUNC\_UART2\_TX        | UART2发送数据接口       |
| FUNC\_UART3\_RX        | UART3接收数据接口       |
| FUNC\_UART3\_TX        | UART3发送数据接口       |
| FUNC\_SPI1\_D0         | SPI1数据线0             |
| FUNC\_SPI1\_D1         | SPI1数据线1             |
| FUNC\_SPI1\_D2         | SPI1数据线2             |
| FUNC\_SPI1\_D3         | SPI1数据线3             |
| FUNC\_SPI1\_D4         | SPI1数据线4             |
| FUNC\_SPI1\_D5         | SPI1数据线5             |
| FUNC\_SPI1\_D6         | SPI1数据线6             |
| FUNC\_SPI1\_D7         | SPI1数据线7             |
| FUNC\_SPI1\_SS0        | SPI1片选信号0           |
| FUNC\_SPI1\_SS1        | SPI1片选信号1           |
| FUNC\_SPI1\_SS2        | SPI1片选信号2           |
| FUNC\_SPI1\_SS3        | SPI1片选信号3           |
| FUNC\_SPI1\_ARB        | SPI1仲裁信号            |
| FUNC\_SPI1\_SCLK       | SPI1时钟                |
| FUNC\_SPI\_SLAVE\_D0   | SPI从模式数据线0        |
| FUNC\_SPI\_SLAVE\_SS   | SPI从模式片选信号       |
| FUNC\_SPI\_SLAVE\_SCLK | SPI从模式时钟           |
| FUNC\_I2S0\_MCLK       | I2S0主时钟（系统时钟）  |
| FUNC\_I2S0\_SCLK       | I2S0串行时钟（位时钟）  |
| FUNC\_I2S0\_WS         | I2S0帧时钟              |
| FUNC\_I2S0\_IN\_D0     | I2S0串行输入数据接口0   |
| FUNC\_I2S0\_IN\_D1     | I2S0串行输入数据接口1   |
| FUNC\_I2S0\_IN\_D2     | I2S0串行输入数据接口2   |
| FUNC\_I2S0\_IN\_D3     | I2S0串行输入数据接口3   |
| FUNC\_I2S0\_OUT\_D0    | I2S0串行输出数据接口0   |
| FUNC\_I2S0\_OUT\_D1    | I2S0串行输出数据接口1   |
| FUNC\_I2S0\_OUT\_D2    | I2S0串行输出数据接口2   |
| FUNC\_I2S0\_OUT\_D3    | I2S0串行输出数据接口3   |
| FUNC\_I2S1\_MCLK       | I2S1主时钟（系统时钟）  |
| FUNC\_I2S1\_SCLK       | I2S1串行时钟（位时钟）  |
| FUNC\_I2S1\_WS         | I2S1帧时钟              |
| FUNC\_I2S1\_IN\_D0     | I2S1串行输入数据接口0   |
| FUNC\_I2S1\_IN\_D1     | I2S1串行输入数据接口1   |
| FUNC\_I2S1\_IN\_D2     | I2S1串行输入数据接口2   |
| FUNC\_I2S1\_IN\_D3     | I2S1串行输入数据接口3   |
| FUNC\_I2S1\_OUT\_D0    | I2S1串行输出数据接口0   |
| FUNC\_I2S1\_OUT\_D1    | I2S1串行输出数据接口1   |
| FUNC\_I2S1\_OUT\_D2    | I2S1串行输出数据接口2   |
| FUNC\_I2S1\_OUT\_D3    | I2S1串行输出数据接口3   |
| FUNC\_I2S2\_MCLK       | I2S2主时钟（系统时钟）  |
| FUNC\_I2S2\_SCLK       | I2S2串行时钟（位时钟）  |
| FUNC\_I2S2\_WS         | I2S2帧时钟              |
| FUNC\_I2S2\_IN\_D0     | I2S2串行输入数据接口0   |
| FUNC\_I2S2\_IN\_D1     | I2S2串行输入数据接口1   |
| FUNC\_I2S2\_IN\_D2     | I2S2串行输入数据接口2   |
| FUNC\_I2S2\_IN\_D3     | I2S2串行输入数据接口3   |
| FUNC\_I2S2\_OUT\_D0    | I2S2串行输出数据接口0   |
| FUNC\_I2S2\_OUT\_D1    | I2S2串行输出数据接口1   |
| FUNC\_I2S2\_OUT\_D2    | I2S2串行输出数据接口2   |
| FUNC\_I2S2\_OUT\_D3    | I2S2串行输出数据接口3   |
| FUNC\_RESV0            | 保留功能                |
| FUNC\_RESV1            | 保留功能                |
| FUNC\_RESV2            | 保留功能                |
| FUNC\_RESV3            | 保留功能                |
| FUNC\_RESV4            | 保留功能                |
| FUNC\_RESV5            | 保留功能                |
| FUNC\_I2C0\_SCLK       | I2C0串行时钟            |
| FUNC\_I2C0\_SDA        | I2C0串行数据接口        |
| FUNC\_I2C1\_SCLK       | I2C1串行时钟            |
| FUNC\_I2C1\_SDA        | I2C1串行数据接口        |
| FUNC\_I2C2\_SCLK       | I2C2串行时钟            |
| FUNC\_I2C2\_SDA        | I2C2串行数据接口        |
| FUNC\_CMOS\_XCLK       | DVP系统时钟             |
| FUNC\_CMOS\_RST        | DVP系统复位信号         |
| FUNC\_CMOS\_PWDN       | DVP使能信号             |
| FUNC\_CMOS\_VSYNC      | DVP场同步               |
| FUNC\_CMOS\_HREF       | DVP行参考信号           |
| FUNC\_CMOS\_PCLK       | 像素时钟                |
| FUNC\_CMOS\_D0         | 像素数据0               |
| FUNC\_CMOS\_D1         | 像素数据1               |
| FUNC\_CMOS\_D2         | 像素数据2               |
| FUNC\_CMOS\_D3         | 像素数据3               |
| FUNC\_CMOS\_D4         | 像素数据4               |
| FUNC\_CMOS\_D5         | 像素数据5               |
| FUNC\_CMOS\_D6         | 像素数据6               |
| FUNC\_CMOS\_D7         | 像素数据7               |
| FUNC\_SCCB\_SCLK       | SCCB时钟                |
| FUNC\_SCCB\_SDA        | SCCB串行数据信号        |
| FUNC\_UART1\_CTS       | UART1清除发送信号       |
| FUNC\_UART1\_DSR       | UART1数据设备准备信号   |
| FUNC\_UART1\_DCD       | UART1数据载波检测       |
| FUNC\_UART1\_RI        | UART1振铃指示           |
| FUNC\_UART1\_SIR\_IN   | UART1串行红外输入信号   |
| FUNC\_UART1\_DTR       | UART1数据终端准备信号   |
| FUNC\_UART1\_RTS       | UART1发送请求信号       |
| FUNC\_UART1\_OUT2      | UART1用户指定输出信号2  |
| FUNC\_UART1\_OUT1      | UART1用户指定输出信号1  |
| FUNC\_UART1\_SIR\_OUT  | UART1串行红外输出信号   |
| FUNC\_UART1\_BAUD      | UART1时钟               |
| FUNC\_UART1\_RE        | UART1接收使能           |
| FUNC\_UART1\_DE        | UART1发送使能           |
| FUNC\_UART1\_RS485\_EN | UART1使能RS485          |
| FUNC\_UART2\_CTS       | UART2清除发送信号       |
| FUNC\_UART2\_DSR       | UART2数据设备准备信号   |
| FUNC\_UART2\_DCD       | UART2数据载波检测       |
| FUNC\_UART2\_RI        | UART2振铃指示           |
| FUNC\_UART2\_SIR\_IN   | UART2串行红外输入信号   |
| FUNC\_UART2\_DTR       | UART2数据终端准备信号   |
| FUNC\_UART2\_RTS       | UART2发送请求信号       |
| FUNC\_UART2\_OUT2      | UART2用户指定输出信号2  |
| FUNC\_UART2\_OUT1      | UART2用户指定输出信号1  |
| FUNC\_UART2\_SIR\_OUT  | UART2串行红外输出信号   |
| FUNC\_UART2\_BAUD      | UART2时钟               |
| FUNC\_UART2\_RE        | UART2接收使能           |
| FUNC\_UART2\_DE        | UART2发送使能           |
| FUNC\_UART2\_RS485\_EN | UART2使能RS485          |
| FUNC\_UART3\_CTS       | 清除发送信号            |
| FUNC\_UART3\_DSR       | 数据设备准备信号        |
| FUNC\_UART3\_DCD       | UART3数据载波检测       |
| FUNC\_UART3\_RI        | UART3振铃指示           |
| FUNC\_UART3\_SIR\_IN   | UART3串行红外输入信号   |
| FUNC\_UART3\_DTR       | UART3数据终端准备信号   |
| FUNC\_UART3\_RTS       | UART3发送请求信号       |
| FUNC\_UART3\_OUT2      | UART3用户指定输出信号2  |
| FUNC\_UART3\_OUT1      | UART3用户指定输出信号1  |
| FUNC\_UART3\_SIR\_OUT  | UART3串行红外输出信号   |
| FUNC\_UART3\_BAUD      | UART3时钟               |
| FUNC\_UART3\_RE        | UART3接收使能           |
| FUNC\_UART3\_DE        | UART3发送使能           |
| FUNC\_UART3\_RS485\_EN | UART3使能RS485          |
| FUNC\_TIMER0\_TOGGLE1  | TIMER0输出信号1         |
| FUNC\_TIMER0\_TOGGLE2  | TIMER0输出信号2         |
| FUNC\_TIMER0\_TOGGLE3  | TIMER0输出信号3         |
| FUNC\_TIMER0\_TOGGLE4  | TIMER0输出信号4         |
| FUNC\_TIMER1\_TOGGLE1  | TIMER1输出信号1         |
| FUNC\_TIMER1\_TOGGLE2  | TIMER1输出信号2         |
| FUNC\_TIMER1\_TOGGLE3  | TIMER1输出信号3         |
| FUNC\_TIMER1\_TOGGLE4  | TIMER1输出信号4         |
| FUNC\_TIMER2\_TOGGLE1  | TIMER2输出信号1         |
| FUNC\_TIMER2\_TOGGLE2  | TIMER2输出信号2         |
| FUNC\_TIMER2\_TOGGLE3  | TIMER2输出信号3         |
| FUNC\_TIMER2\_TOGGLE4  | TIMER2输出信号4         |
| FUNC\_CLK\_SPI2        | SPI2时钟                |
| FUNC\_CLK\_I2C2        | I2C2时钟                |
| FUNC\_INTERNAL0        | 内部功能0               |
| FUNC\_INTERNAL1        | 内部功能1               |
| FUNC\_INTERNAL2        | 内部功能2               |
| FUNC\_INTERNAL3        | 内部功能3               |
| FUNC\_INTERNAL4        | 内部功能4               |
| FUNC\_INTERNAL5        | 内部功能5               |
| FUNC\_INTERNAL6        | 内部功能6               |
| FUNC\_INTERNAL7        | 内部功能7               |
| FUNC\_INTERNAL8        | 内部功能8               |
| FUNC\_INTERNAL9        | 内部功能9               |
| FUNC\_INTERNAL10       | 内部功能10              |
| FUNC\_INTERNAL11       | 内部功能11              |
| FUNC\_INTERNAL12       | 内部功能12              |
| FUNC\_INTERNAL13       | 内部功能13              |
| FUNC\_INTERNAL14       | 内部功能14              |
| FUNC\_INTERNAL15       | 内部功能15              |
| FUNC\_INTERNAL16       | 内部功能16              |
| FUNC\_INTERNAL17       | 内部功能17              |
| FUNC\_CONSTANT         | 常量                    |
| FUNC\_INTERNAL18       | 内部功能18              |
| FUNC\_DEBUG0           | 调试功能0               |
| FUNC\_DEBUG1           | 调试功能1               |
| FUNC\_DEBUG2           | 调试功能2               |
| FUNC\_DEBUG3           | 调试功能3               |
| FUNC\_DEBUG4           | 调试功能4               |
| FUNC\_DEBUG5           | 调试功能5               |
| FUNC\_DEBUG6           | 调试功能6               |
| FUNC\_DEBUG7           | 调试功能7               |
| FUNC\_DEBUG8           | 调试功能8               |
| FUNC\_DEBUG9           | 调试功能9               |
| FUNC\_DEBUG10          | 调试功能10              |
| FUNC\_DEBUG11          | 调试功能11              |
| FUNC\_DEBUG12          | 调试功能12              |
| FUNC\_DEBUG13          | 调试功能13              |
| FUNC\_DEBUG14          | 调试功能14              |
| FUNC\_DEBUG15          | 调试功能15              |
| FUNC\_DEBUG16          | 调试功能16              |
| FUNC\_DEBUG17          | 调试功能17              |
| FUNC\_DEBUG18          | 调试功能18              |
| FUNC\_DEBUG19          | 调试功能19              |
| FUNC\_DEBUG20          | 调试功能20              |
| FUNC\_DEBUG21          | 调试功能21              |
| FUNC\_DEBUG22          | 调试功能22              |
| FUNC\_DEBUG23          | 调试功能23              |
| FUNC\_DEBUG24          | 调试功能24              |
| FUNC\_DEBUG25          | 调试功能25              |
| FUNC\_DEBUG26          | 调试功能26              |
| FUNC\_DEBUG27          | 调试功能27              |
| FUNC\_DEBUG28          | 调试功能28              |
| FUNC\_DEBUG29          | 调试功能29              |
| FUNC\_DEBUG30          | 调试功能30              |
| FUNC\_DEBUG31          | 调试功能31              |

### fpioa\_cfg\_item\_t

#### 描述

FPIOA 管脚配置。

#### 定义

```c
typedef struct _fpioa_cfg_item
{
    int number;
    fpioa_function_t function;
} fpioa_cfg_item_t;
```

#### 成员

| 成员名称 |   描述   |
| :------- | :------- |
| number   | 管脚编号 |
| function | 功能编号 |

### fpioa\_cfg\_t

#### 描述

FPIOA 配置。

#### 定义

```c
typedef struct _fpioa_cfg
{
    uint32_t version;
    uint32_t functions_count;
    fpioa_cfg_item_t functions[];
} fpioa_cfg_t;
```

#### 成员

|    成员名称     |                  描述                  |
| :-------------- | :------------------------------------- |
| version         | 配置版本，必须设为 FPIOA\_CFG\_VERSION |
| functions_count | 功能配置数量                           |
| functions       | 功能配置列表                           |

### sysctl\_power\_bank\_t

#### 描述

电源域编号。

#### 定义

```c
typedef enum _sysctl_power_bank
{
    SYSCTL_POWER_BANK0,
    SYSCTL_POWER_BANK1,
    SYSCTL_POWER_BANK2,
    SYSCTL_POWER_BANK3,
    SYSCTL_POWER_BANK4,
    SYSCTL_POWER_BANK5,
    SYSCTL_POWER_BANK6,
    SYSCTL_POWER_BANK7,
    SYSCTL_POWER_BANK_MAX,
} sysctl_power_bank_t;
```

#### 成员

|       成员名称       |          描述          |
| :------------------- | :--------------------- |
| SYSCTL\_POWER\_BANK0 | 电源域0，控制IO0-IO5   |
| SYSCTL\_POWER\_BANK1 | 电源域0，控制IO6-IO11  |
| SYSCTL\_POWER\_BANK2 | 电源域0，控制IO12-IO17 |
| SYSCTL\_POWER\_BANK3 | 电源域0，控制IO18-IO23 |
| SYSCTL\_POWER\_BANK4 | 电源域0，控制IO24-IO29 |
| SYSCTL\_POWER\_BANK5 | 电源域0，控制IO30-IO35 |
| SYSCTL\_POWER\_BANK6 | 电源域0，控制IO36-IO41 |
| SYSCTL\_POWER\_BANK7 | 电源域0，控制IO42-IO47 |

### sysctl\_io\_power\_mode\_t

#### 描述

IO 输出电压值。

#### 定义

```c
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### 成员

|      成员名称      |    描述    |
| :----------------- | :--------- |
| SYSCTL\_POWER\_V33 | 设置为3.3V |
| SYSCTL\_POWER\_V18 | 设置为1.8V |

### power\_bank\_item\_t

#### 描述

单个电源域配置。

#### 定义

```c
typedef struct _power_bank_item
{
    sysctl_power_bank_t power_bank;
    sysctl_io_power_mode_t io_power_mode;
} power_bank_item_t;
```

#### 成员

|   成员名称    |     描述      |
| :------------ | :------------ |
| power_bank    | 电源域编号    |
| io_power_mode | IO 输出电压值 |

### power\_bank\_cfg\_t

#### 描述

电源域配置。

#### 定义

```c
typedef struct _power_bank_cfg
{
    uint32_t version;
    uint32_t power_banks_count;
    power_bank_item_t power_banks[];
} power_bank_cfg_t;
```

#### 成员

|     成员名称      |                  描述                  |
| :---------------- | :------------------------------------- |
| version           | 配置版本，必须设为 FPIOA\_CFG\_VERSION |
| power_banks_count | 电源域配置数量                         |
| power_banks       | 电源域配置列表                         |

### pin\_cfg\_t

#### 描述

管脚配置。

#### 定义

```c
typedef struct _pin_cfg
{
    uint32_t version;
    bool set_spi0_dvp_data;
} pin_cfg_t;
```

#### 成员

|     成员名称      |                              描述                               |
| :---------------- | :-------------------------------------------------------------- |
| version           | 配置版本，必须设为 FPIOA\_CFG\_VERSION                          |
| set_spi0_dvp_data | 是否设置 SPI0_D0-D7 与 DVP_D0-D7 为 SPI0数据输出与 DVP 数据输入 |

### 举例

```c
/* 配置 IO6、IO7 的功能分别为 GPIOHS0 和 GPIOHS1 */
const fpioa_cfg_t g_fpioa_cfg =
{
    .version = FPIOA_CFG_VERSION,
    .functions_count = 2,
    .functions =
    {
        { .number = 6, .function = FUNC_GPIOHS0 },
        { .number = 7, .function = FUNC_GPIOHS1 }
    }
};
```