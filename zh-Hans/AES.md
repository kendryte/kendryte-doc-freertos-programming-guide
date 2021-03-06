# 高级加密加速器 (AES)

## 概述

AES 模块是用硬件的方式来实现 AES 的时分运算加速。

## 功能描述

K210 内置 AES(高级加密加速器)，相对于软件可以极大的提高 AES 运算速度。AES 加速器支持多种加密/解密模式(ECB, CBC, GCM), 多种长度的 KEY(128,192,256)的运算。

## API参考

对应的头文件 `aes.h`

为用户提供以下接口：

- [aes\_ecb128\_hard\_encrypt](#aesecb128hardencrypt)

- [aes\_ecb128\_hard\_decrypt](#aesecb128harddecrypt)

- [aes\_ecb192\_hard\_encrypt](#aesecb192hardencrypt)

- [aes\_ecb192\_hard\_decrypt](#aesecb192harddecrypt)

- [aes\_ecb256\_hard\_encrypt](#aesecb256hardencrypt)

- [aes\_ecb256\_hard\_decrypt](#aesecb256harddecrypt)

- [aes\_cbc128\_hard\_encrypt](#aescbc128hardencrypt)

- [aes\_cbc128\_hard\_decrypt](#aescbc128harddecrypt)

- [aes\_cbc192\_hard\_encrypt](#aescbc192hardencrypt)

- [aes\_cbc192\_hard\_decrypt](#aescbc192harddecrypt)

- [aes\_cbc256\_hard\_encrypt](#aescbc256hardencrypt)

- [aes\_cbc256\_hard\_decrypt](#aescbc256harddecrypt)

- [aes\_gcm128\_hard\_encrypt](#aesgcm128hardencrypt)

- [aes\_gcm128\_hard\_decrypt](#aesgcm128harddecrypt)

- [aes\_gcm192\_hard\_encrypt](#aesgcm192hardencrypt)

- [aes\_gcm192\_hard\_decrypt](#aesgcm192harddecrypt)

- [aes\_gcm256\_hard\_encrypt](#aesgcm256hardencrypt)

- [aes\_gcm256\_hard\_decrypt](#aesgcm256harddecrypt)

### aes\_ecb128\_hard\_encrypt

#### 描述

AES-ECB-128加密运算，当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
| ------:      |:-----                         | ----  |
|input\_key    |AES-ECB-128加密的密钥                | 输入 |
|input\_data   |AES-ECB-128待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-128加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_ecb128\_hard\_decrypt

#### 描述

AES-ECB-128解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-128解密的密钥                | 输入 |
|input\_data   |AES-ECB-128待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-128解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_encrypt

#### 描述

AES-ECB-192加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-192加密的密钥                | 输入 |
|input\_data   |AES-ECB-192待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-192加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_ecb192\_hard\_decrypt

#### 描述

AES-ECB-192解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  -----       | -----                         |  ----  |
|input\_key    |AES-ECB-192解密的密钥                | 输入 |
|input\_data   |AES-ECB-192待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-192解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_encrypt

#### 描述

AES-ECB-256加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256加密的密钥                | 输入 |
|input\_data   |AES-ECB-256待加密的明文数据           | 输入 |
|input\_len   |AES-ECB-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-ECB-256加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_ecb256\_hard\_decrypt

#### 描述

AES-ECB-256解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256解密的密钥                | 输入 |
|input\_data   |AES-ECB-256待解密的密文数据           | 输入 |
|input\_len   |AES-ECB-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-ECB-256解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_encrypt

#### 描述

AES-CBC-128加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-128加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-128待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-128加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc128\_hard\_decrypt

#### 描述

AES-CBC-128解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context    |AES-CBC-128解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-128待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-128待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-128解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_encrypt

#### 描述

AES-CBC-192加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-192待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-192加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc192\_hard\_decrypt

#### 描述

AES-CBC-192解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-192待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-192待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-192解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_encrypt

#### 描述

AES-CBC-256加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256加密计算的结构体，包含加密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待加密的明文数据           | 输入 |
|input\_len   |AES-CBC-256待加密明文数据的长度        | 输入 |
|output\_data  |AES-CBC-256加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_cbc256\_hard\_decrypt

#### 描述

AES-CBC-256解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256解密计算的结构体，包含解密密钥与偏移向量| 输入 |
|input\_data   |AES-CBC-256待解密的密文数据           | 输入 |
|input\_len   |AES-CBC-256待解密密文数据的长度        | 输入 |
|output\_data  |AES-CBC-256解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为16bytes的整数倍| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_encrypt

#### 描述

AES-GCM-128加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-128加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-128待加密明文数据的长度      | 输入 |
|output\_data  |AES-GCM-128加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-128加密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm128\_hard\_decrypt

#### 描述

AES-GCM-128解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context    |AES-GCM-128解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-128待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-128待解密密文数据的长度。    | 输入 |
|output\_data  |AES-GCM-128解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-128解密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_encrypt

#### 描述

AES-GCM-192加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-192加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-192待加密明文数据的长度。| 输入 |
|output\_data  |AES-GCM-192加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-192加密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm192\_hard\_decrypt

#### 描述

AES-GCM-192解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-192解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-192待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-192待解密密文数据的长度。| 输入 |
|output\_data  |AES-GCM-192解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-192解密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_encrypt

#### 描述

AES-GCM-256加密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称      |  描述                          |输入输出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-256加密计算的结构体，包含加密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待加密的明文数据           | 输入 |
|input\_len   |AES-GCM-256待加密明文数据的长度。| 输入 |
|output\_data  |AES-GCM-256加密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-256加密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### aes\_gcm256\_hard\_decrypt

#### 描述

AES-GCM-256解密运算。当加密数据量小于等于896bytes时会使用cpu来传输数据，大于896bytes时，会使用dma来传输数据，从而提高计算的效率。

#### 函数原型

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 参数

| 参数名称    |  描述                          |输入输出|
|  ------   | -----                         |  ----  |
|context |AES-GCM-256解密计算的结构体，包含解密密钥/偏移向量/aad/aad长度| 输入 |
|input\_data   |AES-GCM-256待解密的密文数据           | 输入 |
|input\_len   |AES-GCM-256待解密密文数据的长度。| 输入 |
|output\_data  |AES-GCM-256解密运算后的结果存放在这个buffer。<br/>这个buffer大小需要至少为4bytes的整数倍，<br/>因为DMA的传输数据的最小粒度为4bytes。| 输出 |
|gcm\_tag  |AES-GCM-256解密运算后的tag存放在这个buffer。<br/>这个buffer的大小需要保证为16bytes| 输出 |

#### 返回值

无。

### 举例

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [aes\_cipher\_mode\_t](#aesciphermodet)：AES 加密/解密的方式。

### aes\_cipher\_mode\_t

#### 描述

AES加密/解密的方式。

#### 定义

```c
typedef enum _aes_cipher_mode
{
    AES_ECB = 0,
    AES_CBC = 1,
    AES_GCM = 2,
    AES_CIPHER_MAX
} aes_cipher_mode_t;
```

#### 成员

| 成员名称 | 描述 |
| :----- | :--- |
| AES\_ECB | ECB 加密/解密 |
| AES\_CBC | CBC 加密/解密 |
| AES\_GCM | GCM 加密/解密 |