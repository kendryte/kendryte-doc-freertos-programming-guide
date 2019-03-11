# 高級加密加速器 (AES)

## 概述

AES 模組是用硬體的方式來實現 AES 的時分運算加速。

## 功能描述

K210 內置 AES(高級加密加速器)，相對於軟體可以極大的提高 AES 運算速度。AES 加速器支持多種加密/解密模式(ECB,CBC,GCM), 多種長度的 KEY(128,192,256)的運算。

## API參考

對應的頭文件 `aes.h`

為用戶提供以下介面：

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

AES-ECB-128加密運算，當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
| ------:      |:-----                         | ----  |
|input\_key    |AES-ECB-128加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_ecb128\_hard\_decrypt

#### 描述

AES-ECB-128解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-128解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-128待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-128解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_encrypt

#### 描述

AES-ECB-192加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-192加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_ecb192\_hard\_decrypt

#### 描述

AES-ECB-192解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  -----       | -----                         |  ----  |
|input\_key    |AES-ECB-192解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-192待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-192解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_encrypt

#### 描述

AES-ECB-256加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256加密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待加密的明文資料           | 輸入 |
|input\_len   |AES-ECB-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_ecb256\_hard\_decrypt

#### 描述

AES-ECB-256解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256解密的密鑰                | 輸入 |
|input\_data   |AES-ECB-256待解密的密文資料           | 輸入 |
|input\_len   |AES-ECB-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-ECB-256解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_encrypt

#### 描述

AES-CBC-128加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-128加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-128待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc128\_hard\_decrypt

#### 描述

AES-CBC-128解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context    |AES-CBC-128解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-128待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-128待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-128解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_encrypt

#### 描述

AES-CBC-192加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-192待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc192\_hard\_decrypt

#### 描述

AES-CBC-192解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-192待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-192待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-192解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_encrypt

#### 描述

AES-CBC-256加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256加密計算的結構體，包含加密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待加密的明文資料           | 輸入 |
|input\_len   |AES-CBC-256待加密明文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_cbc256\_hard\_decrypt

#### 描述

AES-CBC-256解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256解密計算的結構體，包含解密密鑰與偏移向量| 輸入 |
|input\_data   |AES-CBC-256待解密的密文資料           | 輸入 |
|input\_len   |AES-CBC-256待解密密文資料的長度        | 輸入 |
|output\_data  |AES-CBC-256解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為16bytes的整數倍| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_encrypt

#### 描述

AES-GCM-128加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-128加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-128待加密明文資料的長度      | 輸入 |
|output\_data  |AES-GCM-128加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-128加密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm128\_hard\_decrypt

#### 描述

AES-GCM-128解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context    |AES-GCM-128解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-128待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-128待解密密文資料的長度。    | 輸入 |
|output\_data  |AES-GCM-128解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-128解密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_encrypt

#### 描述

AES-GCM-192加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-192加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-192待加密明文資料的長度。| 輸入 |
|output\_data  |AES-GCM-192加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-192加密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm192\_hard\_decrypt

#### 描述

AES-GCM-192解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-192解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-192待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-192待解密密文資料的長度。| 輸入 |
|output\_data  |AES-GCM-192解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-192解密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_encrypt

#### 描述

AES-GCM-256加密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱      |  描述                          |輸入輸出|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-256加密計算的結構體，包含加密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待加密的明文資料           | 輸入 |
|input\_len   |AES-GCM-256待加密明文資料的長度。| 輸入 |
|output\_data  |AES-GCM-256加密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-256加密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### aes\_gcm256\_hard\_decrypt

#### 描述

AES-GCM-256解密運算。當加密資料量小於等於896bytes時會使用cpu來傳輸資料，大於896bytes時，會使用dma來傳輸資料，從而提高計算的效率。

#### 函數原型

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### 參數

| 參數名稱    |  描述                          |輸入輸出|
|  ------   | -----                         |  ----  |
|context |AES-GCM-256解密計算的結構體，包含解密密鑰/偏移向量/aad/aad長度| 輸入 |
|input\_data   |AES-GCM-256待解密的密文資料           | 輸入 |
|input\_len   |AES-GCM-256待解密密文資料的長度。| 輸入 |
|output\_data  |AES-GCM-256解密運算後的結果存放在這個buffer。<br/>這個buffer大小需要至少為4bytes的整數倍，<br/>因為DMA的傳輸資料的最小粒度為4bytes。| 輸出 |
|gcm\_tag  |AES-GCM-256解密運算後的tag存放在這個buffer。<br/>這個buffer的大小需要保證為16bytes| 輸出 |

#### 返回值

無。

### 舉例

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [aes\_cipher\_mode\_t](#aesciphermodet)：AES 加密/解密的方式。

### aes\_cipher\_mode\_t

#### 描述

AES加密/解密的方式。

#### 定義

```c
typedef enum _aes_cipher_mode
{
    AES_ECB = 0,
    AES_CBC = 1,
    AES_GCM = 2,
    AES_CIPHER_MAX
} aes_cipher_mode_t;
```

#### 成員

| 成員名稱 | 描述 |
| :----- | :--- |
| AES\_ECB | ECB 加密/解密 |
| AES\_CBC | CBC 加密/解密 |
| AES\_GCM | GCM 加密/解密 |