# I/O configuration

## Overview

The I/O configuration includes FPIOA and power domain configuration.

FPIOA (Field Programmable I/O Array) allows the user to map 256 internal functions to 48 free I/Os on the chip.

## Features

- Support for I/O's programmable function selection
- 8 driving capability options for I/O output support
- Support I/O internal pull-up resistor selection
- Support I/O internal pull-down resistor selection
- Internal Schmitt trigger settings that support I/O input
- Slew control for I/O output support
- Support level setting of internal input logic
- Support for configuring power domains

## Data type

Corresponding header file `pin_cfg.h`

The relevant data types and data structures are defined as follows:

- [fpioa\_function\_t](#fpioafunctiont): The function number of the pin.
- [fpioa\_cfg\_item\_t](#fpioacfgitemt): FPIOA pin configuration.
- [fpioa\_cfg\_t](#fpioacfgt): FPIOA configuration.
- [sysctl\_power\_bank\_t](#sysctlpowerbankt): Power domain number.
- [sysctl\_io\_power\_mode\_t](#sysctlpowerbankt): IO output voltage selection.
- [power\_bank\_item\_t](#powerbankitemt): Single power domain configuration.
- [power\_bank\_cfg\_t](#powerbankcfgt): Power domain configuration.
- [pin\_cfg\_t](#pincfgt): Pin configuration.

### fpioa\_function\_t

#### Description

The function number of the pin.

#### Type definition

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

#### Enumeration element

|      Element name      |           Description           |
| :--------------------- | :------------------------------ |
| FUNC\_JTAG\_TCLK       | JTAG Test Clock                 |
| FUNC\_JTAG\_TDI        | JTAG Test Data In               |
| FUNC\_JTAG\_TMS        | JTAG Test Mode Select           |
| FUNC\_JTAG\_TDO        | JTAG Test Data Out              |
| FUNC\_SPI0\_D0         | SPI0 Data 0                     |
| FUNC\_SPI0\_D1         | SPI0 Data 1                     |
| FUNC\_SPI0\_D2         | SPI0 Data 2                     |
| FUNC\_SPI0\_D3         | SPI0 Data 3                     |
| FUNC\_SPI0\_D4         | SPI0 Data 4                     |
| FUNC\_SPI0\_D5         | SPI0 Data 5                     |
| FUNC\_SPI0\_D6         | SPI0 Data 6                     |
| FUNC\_SPI0\_D7         | SPI0 Data 7                     |
| FUNC\_SPI0\_SS0        | SPI0 Chip Select 0              |
| FUNC\_SPI0\_SS1        | SPI0 Chip Select 1              |
| FUNC\_SPI0\_SS2        | SPI0 Chip Select 2              |
| FUNC\_SPI0\_SS3        | SPI0 Chip Select 3              |
| FUNC\_SPI0\_ARB        | SPI0 Arbitration                |
| FUNC\_SPI0\_SCLK       | SPI0 Serial Clock               |
| FUNC\_UARTHS\_RX       | UART High speed Receiver        |
| FUNC\_UARTHS\_TX       | UART High speed Transmitter     |
| FUNC\_RESV6            | Clock Input 1                   |
| FUNC\_RESV7            | Clock Input 2                   |
| FUNC\_CLK\_SPI1        | Clock SPI1                      |
| FUNC\_CLK\_I2C1        | Clock I2C1                      |
| FUNC\_GPIOHS0          | GPIO High speed 0               |
| FUNC\_GPIOHS1          | GPIO High speed 1               |
| FUNC\_GPIOHS2          | GPIO High speed 2               |
| FUNC\_GPIOHS3          | GPIO High speed 3               |
| FUNC\_GPIOHS4          | GPIO High speed 4               |
| FUNC\_GPIOHS5          | GPIO High speed 5               |
| FUNC\_GPIOHS6          | GPIO High speed 6               |
| FUNC\_GPIOHS7          | GPIO High speed 7               |
| FUNC\_GPIOHS8          | GPIO High speed 8               |
| FUNC\_GPIOHS9          | GPIO High speed 9               |
| FUNC\_GPIOHS10         | GPIO High speed 10              |
| FUNC\_GPIOHS11         | GPIO High speed 11              |
| FUNC\_GPIOHS12         | GPIO High speed 12              |
| FUNC\_GPIOHS13         | GPIO High speed 13              |
| FUNC\_GPIOHS14         | GPIO High speed 14              |
| FUNC\_GPIOHS15         | GPIO High speed 15              |
| FUNC\_GPIOHS16         | GPIO High speed 16              |
| FUNC\_GPIOHS17         | GPIO High speed 17              |
| FUNC\_GPIOHS18         | GPIO High speed 18              |
| FUNC\_GPIOHS19         | GPIO High speed 19              |
| FUNC\_GPIOHS20         | GPIO High speed 20              |
| FUNC\_GPIOHS21         | GPIO High speed 21              |
| FUNC\_GPIOHS22         | GPIO High speed 22              |
| FUNC\_GPIOHS23         | GPIO High speed 23              |
| FUNC\_GPIOHS24         | GPIO High speed 24              |
| FUNC\_GPIOHS25         | GPIO High speed 25              |
| FUNC\_GPIOHS26         | GPIO High speed 26              |
| FUNC\_GPIOHS27         | GPIO High speed 27              |
| FUNC\_GPIOHS28         | GPIO High speed 28              |
| FUNC\_GPIOHS29         | GPIO High speed 29              |
| FUNC\_GPIOHS30         | GPIO High speed 30              |
| FUNC\_GPIOHS31         | GPIO High speed 31              |
| FUNC\_GPIO0            | GPIO pin 0                      |
| FUNC\_GPIO1            | GPIO pin 1                      |
| FUNC\_GPIO2            | GPIO pin 2                      |
| FUNC\_GPIO3            | GPIO pin 3                      |
| FUNC\_GPIO4            | GPIO pin 4                      |
| FUNC\_GPIO5            | GPIO pin 5                      |
| FUNC\_GPIO6            | GPIO pin 6                      |
| FUNC\_GPIO7            | GPIO pin 7                      |
| FUNC\_UART1\_RX        | UART1 Receiver                  |
| FUNC\_UART1\_TX        | UART1 Transmitter               |
| FUNC\_UART2\_RX        | UART2 Receiver                  |
| FUNC\_UART2\_TX        | UART2 Transmitter               |
| FUNC\_UART3\_RX        | UART3 Receiver                  |
| FUNC\_UART3\_TX        | UART3 Transmitter               |
| FUNC\_SPI1\_D0         | SPI1 Data 0                     |
| FUNC\_SPI1\_D1         | SPI1 Data 1                     |
| FUNC\_SPI1\_D2         | SPI1 Data 2                     |
| FUNC\_SPI1\_D3         | SPI1 Data 3                     |
| FUNC\_SPI1\_D4         | SPI1 Data 4                     |
| FUNC\_SPI1\_D5         | SPI1 Data 5                     |
| FUNC\_SPI1\_D6         | SPI1 Data 6                     |
| FUNC\_SPI1\_D7         | SPI1 Data 7                     |
| FUNC\_SPI1\_SS0        | SPI1 Chip Select 0              |
| FUNC\_SPI1\_SS1        | SPI1 Chip Select 1              |
| FUNC\_SPI1\_SS2        | SPI1 Chip Select 2              |
| FUNC\_SPI1\_SS3        | SPI1 Chip Select 3              |
| FUNC\_SPI1\_ARB        | SPI1 Arbitration                |
| FUNC\_SPI1\_SCLK       | SPI1 Serial Clock               |
| FUNC\_SPI\_SLAVE\_D0   | SPI Slave Data 0                |
| FUNC\_SPI\_SLAVE\_SS   | SPI Slave Select                |
| FUNC\_SPI\_SLAVE\_SCLK | SPI Slave Serial Clock          |
| FUNC\_I2S0\_MCLK       | I2S0 Master Clock               |
| FUNC\_I2S0\_SCLK       | I2S0 Serial Clock(BCLK)         |
| FUNC\_I2S0\_WS         | I2S0 Word Select(LRCLK)         |
| FUNC\_I2S0\_IN\_D0     | I2S0 Serial Data Input 0        |
| FUNC\_I2S0\_IN\_D1     | I2S0 Serial Data Input 1        |
| FUNC\_I2S0\_IN\_D2     | I2S0 Serial Data Input 2        |
| FUNC\_I2S0\_IN\_D3     | I2S0 Serial Data Input 3        |
| FUNC\_I2S0\_OUT\_D0    | I2S0 Serial Data Output 0       |
| FUNC\_I2S0\_OUT\_D1    | I2S0 Serial Data Output 1       |
| FUNC\_I2S0\_OUT\_D2    | I2S0 Serial Data Output 2       |
| FUNC\_I2S0\_OUT\_D3    | I2S0 Serial Data Output 3       |
| FUNC\_I2S1\_MCLK       | I2S1 Master Clock               |
| FUNC\_I2S1\_SCLK       | I2S1 Serial Clock(BCLK)         |
| FUNC\_I2S1\_WS         | I2S1 Word Select(LRCLK)         |
| FUNC\_I2S1\_IN\_D0     | I2S1 Serial Data Input 0        |
| FUNC\_I2S1\_IN\_D1     | I2S1 Serial Data Input 1        |
| FUNC\_I2S1\_IN\_D2     | I2S1 Serial Data Input 2        |
| FUNC\_I2S1\_IN\_D3     | I2S1 Serial Data Input 3        |
| FUNC\_I2S1\_OUT\_D0    | I2S1 Serial Data Output 0       |
| FUNC\_I2S1\_OUT\_D1    | I2S1 Serial Data Output 1       |
| FUNC\_I2S1\_OUT\_D2    | I2S1 Serial Data Output 2       |
| FUNC\_I2S1\_OUT\_D3    | I2S1 Serial Data Output 3       |
| FUNC\_I2S2\_MCLK       | I2S2 Master Clock               |
| FUNC\_I2S2\_SCLK       | I2S2 Serial Clock(BCLK)         |
| FUNC\_I2S2\_WS         | I2S2 Word Select(LRCLK)         |
| FUNC\_I2S2\_IN\_D0     | I2S2 Serial Data Input 0        |
| FUNC\_I2S2\_IN\_D1     | I2S2 Serial Data Input 1        |
| FUNC\_I2S2\_IN\_D2     | I2S2 Serial Data Input 2        |
| FUNC\_I2S2\_IN\_D3     | I2S2 Serial Data Input 3        |
| FUNC\_I2S2\_OUT\_D0    | I2S2 Serial Data Output 0       |
| FUNC\_I2S2\_OUT\_D1    | I2S2 Serial Data Output 1       |
| FUNC\_I2S2\_OUT\_D2    | I2S2 Serial Data Output 2       |
| FUNC\_I2S2\_OUT\_D3    | I2S2 Serial Data Output 3       |
| FUNC\_RESV0            | Reserved function               |
| FUNC\_RESV1            | Reserved function               |
| FUNC\_RESV2            | Reserved function               |
| FUNC\_RESV3            | Reserved function               |
| FUNC\_RESV4            | Reserved function               |
| FUNC\_RESV5            | Reserved function               |
| FUNC\_I2C0\_SCLK       | I2C0 Serial Clock               |
| FUNC\_I2C0\_SDA        | I2C0 Serial Data                |
| FUNC\_I2C1\_SCLK       | I2C1 Serial Clock               |
| FUNC\_I2C1\_SDA        | I2C1 Serial Data                |
| FUNC\_I2C2\_SCLK       | I2C2 Serial Clock               |
| FUNC\_I2C2\_SDA        | I2C2 Serial Data                |
| FUNC\_CMOS\_XCLK       | DVP System Clock                |
| FUNC\_CMOS\_RST        | DVP System Reset                |
| FUNC\_CMOS\_PWDN       | DVP Power Down Mode             |
| FUNC\_CMOS\_VSYNC      | DVP Vertical Sync               |
| FUNC\_CMOS\_HREF       | DVP Horizontal Reference output |
| FUNC\_CMOS\_PCLK       | Pixel Clock                     |
| FUNC\_CMOS\_D0         | Data Bit 0                      |
| FUNC\_CMOS\_D1         | Data Bit 1                      |
| FUNC\_CMOS\_D2         | Data Bit 2                      |
| FUNC\_CMOS\_D3         | Data Bit 3                      |
| FUNC\_CMOS\_D4         | Data Bit 4                      |
| FUNC\_CMOS\_D5         | Data Bit 5                      |
| FUNC\_CMOS\_D6         | Data Bit 6                      |
| FUNC\_CMOS\_D7         | Data Bit 7                      |
| FUNC\_SCCB\_SCLK       | SCCB Serial Clock               |
| FUNC\_SCCB\_SDA        | SCCB Serial Data                |
| FUNC\_UART1\_CTS       | UART1 Clear To Send             |
| FUNC\_UART1\_DSR       | UART1 Data Set Ready            |
| FUNC\_UART1\_DCD       | UART1 Data Carrier Detect       |
| FUNC\_UART1\_RI        | UART1 Ring Indicator            |
| FUNC\_UART1\_SIR\_IN   | UART1 Serial Infrared Input     |
| FUNC\_UART1\_DTR       | UART1 Data Terminal Ready       |
| FUNC\_UART1\_RTS       | UART1 Request To Send           |
| FUNC\_UART1\_OUT2      | UART1 User-designated Output 2  |
| FUNC\_UART1\_OUT1      | UART1 User-designated Output 1  |
| FUNC\_UART1\_SIR\_OUT  | UART1 Serial Infrared Output    |
| FUNC\_UART1\_BAUD      | UART1 Transmit Clock Output     |
| FUNC\_UART1\_RE        | UART1 Receiver Output Enable    |
| FUNC\_UART1\_DE        | UART1 Driver Output Enable      |
| FUNC\_UART1\_RS485\_EN | UART1 RS485 Enable              |
| FUNC\_UART2\_CTS       | UART2 Clear To Send             |
| FUNC\_UART2\_DSR       | UART2 Data Set Ready            |
| FUNC\_UART2\_DCD       | UART2 Data Carrier Detect       |
| FUNC\_UART2\_RI        | UART2 Ring Indicator            |
| FUNC\_UART2\_SIR\_IN   | UART2 Serial Infrared Input     |
| FUNC\_UART2\_DTR       | UART2 Data Terminal Ready       |
| FUNC\_UART2\_RTS       | UART2 Request To Send           |
| FUNC\_UART2\_OUT2      | UART2 User-designated Output 2  |
| FUNC\_UART2\_OUT1      | UART2 User-designated Output 1  |
| FUNC\_UART2\_SIR\_OUT  | UART2 Serial Infrared Output    |
| FUNC\_UART2\_BAUD      | UART2 Transmit Clock Output     |
| FUNC\_UART2\_RE        | UART2 Receiver Output Enable    |
| FUNC\_UART2\_DE        | UART2 Driver Output Enable      |
| FUNC\_UART2\_RS485\_EN | UART2 RS485 Enable              |
| FUNC\_UART3\_CTS       | UART3 Clear To Send             |
| FUNC\_UART3\_DSR       | UART3 Data Set Ready            |
| FUNC\_UART3\_DCD       | UART3 Data Carrier Detect       |
| FUNC\_UART3\_RI        | UART3 Ring Indicator            |
| FUNC\_UART3\_SIR\_IN   | UART3 Serial Infrared Input     |
| FUNC\_UART3\_DTR       | UART3 Data Terminal Ready       |
| FUNC\_UART3\_RTS       | UART3 Request To Send           |
| FUNC\_UART3\_OUT2      | UART3 User-designated Output 2  |
| FUNC\_UART3\_OUT1      | UART3 User-designated Output 1  |
| FUNC\_UART3\_SIR\_OUT  | UART3 Serial Infrared Output    |
| FUNC\_UART3\_BAUD      | UART3 Transmit Clock Output     |
| FUNC\_UART3\_RE        | UART3 Receiver Output Enable    |
| FUNC\_UART3\_DE        | UART3 Driver Output Enable      |
| FUNC\_UART3\_RS485\_EN | UART3 RS485 Enable              |
| FUNC\_TIMER0\_TOGGLE1  | TIMER0 Toggle Output 1          |
| FUNC\_TIMER0\_TOGGLE2  | TIMER0 Toggle Output 2          |
| FUNC\_TIMER0\_TOGGLE3  | TIMER0 Toggle Output 3          |
| FUNC\_TIMER0\_TOGGLE4  | TIMER0 Toggle Output 4          |
| FUNC\_TIMER1\_TOGGLE1  | TIMER1 Toggle Output 1          |
| FUNC\_TIMER1\_TOGGLE2  | TIMER1 Toggle Output 2          |
| FUNC\_TIMER1\_TOGGLE3  | TIMER1 Toggle Output 3          |
| FUNC\_TIMER1\_TOGGLE4  | TIMER1 Toggle Output 4          |
| FUNC\_TIMER2\_TOGGLE1  | TIMER2 Toggle Output 1          |
| FUNC\_TIMER2\_TOGGLE2  | TIMER2 Toggle Output 2          |
| FUNC\_TIMER2\_TOGGLE3  | TIMER2 Toggle Output 3          |
| FUNC\_TIMER2\_TOGGLE4  | TIMER2 Toggle Output 4          |
| FUNC\_CLK\_SPI2        | Clock SPI2                      |
| FUNC\_CLK\_I2C2        | Clock I2C2                      |
| FUNC\_INTERNAL0        | Internal function 0             |
| FUNC\_INTERNAL1        | Internal function 1             |
| FUNC\_INTERNAL2        | Internal function 2             |
| FUNC\_INTERNAL3        | Internal function 3             |
| FUNC\_INTERNAL4        | Internal function 4             |
| FUNC\_INTERNAL5        | Internal function 5             |
| FUNC\_INTERNAL6        | Internal function 6             |
| FUNC\_INTERNAL7        | Internal function 7             |
| FUNC\_INTERNAL8        | Internal function 8             |
| FUNC\_INTERNAL9        | Internal function 9             |
| FUNC\_INTERNAL10       | Internal function 10            |
| FUNC\_INTERNAL11       | Internal function 11            |
| FUNC\_INTERNAL12       | Internal function 12            |
| FUNC\_INTERNAL13       | Internal function 13            |
| FUNC\_INTERNAL14       | Internal function 14            |
| FUNC\_INTERNAL15       | Internal function 15            |
| FUNC\_INTERNAL16       | Internal function 16            |
| FUNC\_INTERNAL17       | Internal function 17            |
| FUNC\_CONSTANT         | Constant function               |
| FUNC\_INTERNAL18       | Internal function 18            |
| FUNC\_DEBUG0           | Debug function 0                |
| FUNC\_DEBUG1           | Debug function 1                |
| FUNC\_DEBUG2           | Debug function 2                |
| FUNC\_DEBUG3           | Debug function 3                |
| FUNC\_DEBUG4           | Debug function 4                |
| FUNC\_DEBUG5           | Debug function 5                |
| FUNC\_DEBUG6           | Debug function 6                |
| FUNC\_DEBUG7           | Debug function 7                |
| FUNC\_DEBUG8           | Debug function 8                |
| FUNC\_DEBUG9           | Debug function 9                |
| FUNC\_DEBUG10          | Debug function 10               |
| FUNC\_DEBUG11          | Debug function 11               |
| FUNC\_DEBUG12          | Debug function 12               |
| FUNC\_DEBUG13          | Debug function 13               |
| FUNC\_DEBUG14          | Debug function 14               |
| FUNC\_DEBUG15          | Debug function 15               |
| FUNC\_DEBUG16          | Debug function 16               |
| FUNC\_DEBUG17          | Debug function 17               |
| FUNC\_DEBUG18          | Debug function 18               |
| FUNC\_DEBUG19          | Debug function 19               |
| FUNC\_DEBUG20          | Debug function 20               |
| FUNC\_DEBUG21          | Debug function 21               |
| FUNC\_DEBUG22          | Debug function 22               |
| FUNC\_DEBUG23          | Debug function 23               |
| FUNC\_DEBUG24          | Debug function 24               |
| FUNC\_DEBUG25          | Debug function 25               |
| FUNC\_DEBUG26          | Debug function 26               |
| FUNC\_DEBUG27          | Debug function 27               |
| FUNC\_DEBUG28          | Debug function 28               |
| FUNC\_DEBUG29          | Debug function 29               |
| FUNC\_DEBUG30          | Debug function 30               |
| FUNC\_DEBUG31          | Debug function 31               |

### fpioa\_cfg\_item\_t

#### Description

FPIOA pin configuration.

#### Type definition

```c
typedef struct _fpioa_cfg_item
{
    int number;
    fpioa_function_t function;
} fpioa_cfg_item_t;
```

#### Enumeration element

| Element name |   Description   |
| :----------- | :-------------- |
| number       | Pin number      |
| function     | Function number |

### fpioa\_cfg\_t

#### Description

FPIOA configuration.

#### Type definition

```c
typedef struct _fpioa_cfg
{
    uint32_t version;
    uint32_t functions_count;
    fpioa_cfg_item_t functions[];
} fpioa_cfg_t;
```

#### Enumeration element

|  Element name   |                        Description                        |
| :-------------- | :-------------------------------------------------------- |
| version         | Configuration version, must be set to FPIOA\_CFG\_VERSION |
| functions_count | Number of function configurations                         |
| functions       | Function configurations list                              |

### sysctl\_power\_bank\_t

#### Description

Power domain number.

#### Type definition

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

#### Enumeration element

|     Element name     |            Description            |
| :------------------- | :-------------------------------- |
| SYSCTL\_POWER\_BANK0 | Power domain 0, control IO0-IO5   |
| SYSCTL\_POWER\_BANK1 | Power domain 0, control IO6-IO11  |
| SYSCTL\_POWER\_BANK2 | Power domain 0, control IO12-IO17 |
| SYSCTL\_POWER\_BANK3 | Power domain 0, control IO18-IO23 |
| SYSCTL\_POWER\_BANK4 | Power domain 0, control IO24-IO29 |
| SYSCTL\_POWER\_BANK5 | Power domain 0, control IO30-IO35 |
| SYSCTL\_POWER\_BANK6 | Power domain 0, control IO36-IO41 |
| SYSCTL\_POWER\_BANK7 | Power domain 0, control IO42-IO47 |

### sysctl\_io\_power\_mode\_t

#### Description

I/O output voltage selection。

#### Type definition

```c
typedef enum _sysctl_io_power_mode
{
    SYSCTL_POWER_V33,
    SYSCTL_POWER_V18
} sysctl_io_power_mode_t;
```

#### Enumeration element

|    Element name    | Description |
| :----------------- | :---------- |
| SYSCTL\_POWER\_V33 | Set to 3.3V |
| SYSCTL\_POWER\_V18 | Set to 1.8V |

### power\_bank\_item\_t

#### Description

Single power domain configuration.

#### Type definition

```c
typedef struct _power_bank_item
{
    sysctl_power_bank_t power_bank;
    sysctl_io_power_mode_t io_power_mode;
} power_bank_item_t;
```

#### Enumeration element

| Element name  |         Description          |
| :------------ | :--------------------------- |
| power_bank    | Power domain number          |
| io_power_mode | I/O output voltage selection |

### power\_bank\_cfg\_t

#### Description

Power domain configuration.

#### Type definition

```c
typedef struct _power_bank_cfg
{
    uint32_t version;
    uint32_t power_banks_count;
    power_bank_item_t power_banks[];
} power_bank_cfg_t;
```

#### Enumeration element

|   Element name    |                        Description                        |
| :---------------- | :-------------------------------------------------------- |
| version           | Configuration version, must be set to FPIOA\_CFG\_VERSION |
| power_banks_count | Number of power domain configurations                     |
| power_banks       | Power domain configuration list                           |

### pin\_cfg\_t

#### Description

Pin configuration.

#### Type definition

```c
typedef struct _pin_cfg
{
    uint32_t version;
    bool set_spi0_dvp_data;
} pin_cfg_t;
```

#### Enumeration element

|   Element name    |                                   Description                                   |
| :---------------- | :------------------------------------------------------------------------------ |
| version           | Configuration version, must be set to FPIOA\_CFG\_VERSION                       |
| set_spi0_dvp_data | Whether to set SPI0_D0-D7 and DVP_D0-D7 for SPI0 data output and DVP data input |

### Example

```c
/* Configuration IO6, IO7 functions to GPIOHS0 and GPIOHS1 */
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
