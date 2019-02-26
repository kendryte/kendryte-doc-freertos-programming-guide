# 快速傅立叶变换加速器 (FFT)

## Overview

FFT 模块是用硬件的方式来实现 FFT 的基 2 时分运算加速。

## Features

目前该模块可以支持64点、128点、256点以及512点的 FFT 以及 IFFT。在 FFT 内部有两块大小为 512 * 32 bit 的 SRAM，在配置完成后 FFT 会向 DMA 发送 TX 请求，将 DMA 送来的送据放到其中的一块 SRAM 中去，直到满足当前 FFT 运算所需要的数据量并开始 FFT 运算，蝶形运算单元从包含有有效数据的 SRAM 中读出数据，运算结束后将数据写到另外一块 SRAM 中去，下次蝶形运算再从刚写入的 SRAM 中读出数据，运算结束后并写入另外一块 SRAM，如此反复交替进行直到完成整个 FFT 运算。

## API

对应的头文件 `fft.h`

为用户提供以下接口：

- [fft\_complex\_uint16](#fftcomplexuint16)

### fft\_complex\_uint16

#### Description

FFT 运算。

#### Function prototype

```c
void fft_complex_uint16(uint16_t shift, fft_direction_t direction, const uint64_t *input, size_t point_num, uint64_t *output);
```

#### Parameter

| Parameter name     |   Description                     |  Input or output  |
| --------   | ---------------             | ----     |
| shift    | FFT模块16位寄存器导致数据溢出(-32768~32767)，FFT变换有9层，shift决定哪一层需要移位操作(如0x1ff表示9层都做移位操作；0x03表示第第一层与第二层做移位操作)，防止溢出。如果移位了，则变换后的幅值不是正常FFT变换的幅值，对应关系可以参考fft_test测试demo程序。包含了求解频率点、相位、幅值的示例| Input |
| direction | FFT 正变换或是逆变换              | Input |
| input | Input的数据序列，格式为 RIRI.., 实部与虚部的精度都为 16 bit | Input|
| point_num | 待运算的数据点数，只能为 512/256/128/64 | Input |
| output | 运算后结果。格式为 RIRI.. ,实部与虚部的精度都为 16 bit | Output |

### Example

```c
#define FFT_N               512U
#define FFT_FORWARD_SHIFT   0x0U
#define FFT_BACKWARD_SHIFT  0x1ffU
#define PI                  3.14159265358979323846
for (i = 0; i < FFT_N; i++)
{
    tempf1[0] = 0.3 * cosf(2 * PI * i / FFT_N + PI / 3) * 256;
    tempf1[1] = 0.1 * cosf(16 * 2 * PI * i / FFT_N - PI / 9) * 256;
    tempf1[2] = 0.5 * cosf((19 * 2 * PI * i / FFT_N) + PI / 6) * 256;
    data_hard[i].real = (int16_t)(tempf1[0] + tempf1[1] + tempf1[2] + 10);
    data_hard[i].imag = (int16_t)0;
}
for (int i = 0; i < FFT_N / 2; ++i)
{
    input_data = (fft_data_t *)&buffer_input[i];
    input_data->R1 = data_hard[2 * i].real;
    input_data->I1 = data_hard[2 * i].imag;
    input_data->R2 = data_hard[2 * i + 1].real;
    input_data->I2 = data_hard[2 * i + 1].imag;
}
fft_complex_uint16(FFT_FORWARD_SHIFT, FFT_DIR_FORWARD, buffer_input, FFT_N, buffer_output);
for (i = 0; i < FFT_N / 2; i++)
{
    output_data = (fft_data_t*)&buffer_output[i];
    data_hard[2 * i].imag = output_data->I1 ;
    data_hard[2 * i].real = output_data->R1 ;
    data_hard[2 * i + 1].imag = output_data->I2 ;
    data_hard[2 * i + 1].real = output_data->R2 ;
}
for (int i = 0; i < FFT_N / 2; ++i)
{
    input_data = (fft_data_t *)&buffer_input[i];
    input_data->R1 = data_hard[2 * i].real;
    input_data->I1 = data_hard[2 * i].imag;
    input_data->R2 = data_hard[2 * i + 1].real;
    input_data->I2 = data_hard[2 * i + 1].imag;
}
fft_complex_uint16(FFT_BACKWARD_SHIFT, FFT_DIR_BACKWARD, buffer_input, FFT_N, buffer_output);
for (i = 0; i < FFT_N / 2; i++)
{
    output_data = (fft_data_t*)&buffer_output[i];
    data_hard[2 * i].imag = output_data->I1 ;
    data_hard[2 * i].real = output_data->R1 ;
    data_hard[2 * i + 1].imag = output_data->I2 ;
    data_hard[2 * i + 1].real = output_data->R2 ;
}
```

## Data type

The relevant data types and data structures are defined as follows:

- [fft\_data\_t](#fftdatat)：FFT 运算传入的数据格式。
- [fft\_direction\_t](#fftdirectiont)：FFT 运算模式。

### fft\_data\_t

#### Description

FFT运算传入的数据格式。

#### Type definition

```c
typedef struct tag_fft_data
{
    int16_t I1;
    int16_t R1;
    int16_t I2;
    int16_t R2;
} fft_data_t;
```

#### Enumeration element

| Element name | Description |
| ----- | --- |
| I1 | 第一个数据的虚部  |
| R1 | 第一个数据的实部  |
| I2 | 第二个数据的虚部  |
| R2 | 第二个数据的实部  |

### fft\_direction\_t

#### Description

FFT运算模式

#### Type definition

```c
typedef enum tag_fft_direction
{
    FFT_DIR_BACKWARD,
    FFT_DIR_FORWARD,
    FFT_DIR_MAX,
} fft_direction_t;
```

#### Enumeration element

| Element name | Description |
| ----- | --- |
| FFT\_DIR\_BACKWARD | FFT 逆变换 |
| FFT\_DIR\_FORWARD  | FFT 正变换 |