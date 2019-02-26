# Advanced Encryption Standard acceleration engine(AES)

## Overview

The AES module uses hardware to implement AES operation acceleration.

## Features

K210 have a built-in AES(Advanced Encryption Standard acceleration engine).
Compared with software, it can greatly improve the speed of AES operation.
The AES accelerator supports multiple encryption/decryption modes (ECB, CBC, GCM)
and multiple length of KEY (128, 192, 256).

## API

Corresponding header file `aes.h`

Provide the following interfaces

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

#### Description

AES-ECB-128 encryption operation, when the amount of encrypted data is less than or equal to 896 bytes, it will use the CPU to transmit data. When it is greater than 896 bytes, it will use DMA to transmit data, thus improving the calculation efficiency.

#### Function prototype

```c
void aes_ecb128_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
| ------:      |:-----                         | ----  |
|input\_key    |AES-ECB-128 encryption key                | Input |
|input\_data   |AES-ECB-128 plaintext data to be encrypted           | Input |
|input\_len   |AES-ECB-128 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-ECB-128 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_ecb128\_hard\_decrypt

#### Description

AES-ECB-128 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_ecb128_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-128 decryption key                | Input |
|input\_data   |AES-ECB-128 ciphertext data to be decrypted           | Input |
|input\_len   |AES-ECB-128 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-ECB-128 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_ecb192\_hard\_encrypt

#### Description

AES-ECB-192 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_ecb192_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-192 encryption key                | Input |
|input\_data   |AES-ECB-192 plaintext data to be encrypted           | Input |
|input\_len   |AES-ECB-192 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-ECB-192 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_ecb192\_hard\_decrypt

#### Description

AES-ECB-192 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_ecb192_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  -----       | -----                         |  ----  |
|input\_key    |AES-ECB-192 decryption key                | Input |
|input\_data   |AES-ECB-192 ciphertext data to be decrypted           | Input |
|input\_len   |AES-ECB-192 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-ECB-192 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_ecb256\_hard\_encrypt

#### Description

AES-ECB-256 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_ecb256_hard_encrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256 encryption key                | Input |
|input\_data   |AES-ECB-256 plaintext data to be encrypted           | Input |
|input\_len   |AES-ECB-256 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-ECB-256 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_ecb256\_hard\_decrypt

#### Description

AES-ECB-256 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_ecb256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|input\_key    |AES-ECB-256 decryption key                | Input |
|input\_data   |AES-ECB-256 ciphertext data to be decrypted           | Input |
|input\_len   |AES-ECB-256 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-ECB-256 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc128\_hard\_encrypt

#### Description

AES-CBC-128 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc128_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-128 encryption operation structure containing encryption key and offset vector| Input |
|input\_data   |AES-CBC-128 plaintext data to be encrypted           | Input |
|input\_len   |AES-CBC-128 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-CBC-128 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc128\_hard\_decrypt

#### Description

AES-CBC-128 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc128_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context    |AES-CBC-128 decryption operation structure, including decryption key and offset vector| Input |
|input\_data   |AES-CBC-128 ciphertext data to be decrypted           | Input |
|input\_len   |AES-CBC-128 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-CBC-128 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc192\_hard\_encrypt

#### Description

AES-CBC-192 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc192_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192 encryption operation structure containing encryption key and offset vector| Input |
|input\_data   |AES-CBC-192 plaintext data to be encrypted           | Input |
|input\_len   |AES-CBC-192 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-CBC-192 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc192\_hard\_decrypt

#### Description

AES-CBC-192 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc192_hard_decrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-192 decryption operation structure, including decryption key and offset vector| Input |
|input\_data   |AES-CBC-192 ciphertext data to be decrypted           | Input |
|input\_len   |AES-CBC-192 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-CBC-192 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc256\_hard\_encrypt

#### Description

AES-CBC-256 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc256_hard_encrypt(cbc_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256 encryption operation structure containing encryption key and offset vector| Input |
|input\_data   |AES-CBC-256 plaintext data to be encrypted           | Input |
|input\_len   |AES-CBC-256 length of plaintext data to be encrypted        | Input |
|output\_data  |The result of the AES-CBC-256 encryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_cbc256\_hard\_decrypt

#### Description

AES-CBC-256 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_cbc256_hard_decrypt(uint8_t *input_key, uint8_t *input_data, size_t input_len, uint8_t *output_data)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-CBC-256 decryption operation structure, including decryption key and offset vector| Input |
|input\_data   |AES-CBC-256 ciphertext data to be decrypted           | Input |
|input\_len   |AES-CBC-256 length of ciphertext data to be decrypted        | Input |
|output\_data  |The result of the AES-CBC-256 decryption operation is stored in this buffer.<br/>This buffer size needs to be at least an integer multiple of 16bytes.| Output |

#### Return value

None.

### aes\_gcm128\_hard\_encrypt

#### Description

AES-GCM-128 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm128_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |AES-GCM-128加密计算的结构体, including the encryption key / offset vector / aad / aad length| Input |
|input\_data   |AES-GCM-128 plaintext data to be encrypted           | Input |
|input\_len   |AES-GCM-128 length of plaintext data to be encrypted      | Input |
|output\_data  |The result of the AES-GCM-128 encryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-128 encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### aes\_gcm128\_hard\_decrypt

#### Description

AES-GCM-128 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm128_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context    |The structure of the AES-GCM-128 decryption operation, including the decryption key/offset vector/aad/aad length| Input |
|input\_data   |AES-GCM-128 ciphertext data to be decrypted           | Input |
|input\_len   |AES-GCM-128 length of ciphertext data to be decrypted。    | Input |
|output\_data  |The result of the AES-GCM-128 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-128 decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### aes\_gcm192\_hard\_encrypt

#### Description

AES-GCM-192 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm192_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |The structure of the AES-GCM-192 encryption operation, including the encryption key / offset vector / aad / aad length| Input |
|input\_data   |AES-GCM-192 plaintext data to be encrypted           | Input |
|input\_len   |AES-GCM-192 length of plaintext data to be encrypted。| Input |
|output\_data  |The result of the AES-GCM-192 encryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-192 encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### aes\_gcm192\_hard\_decrypt

#### Description

AES-GCM-192 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm192_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |The structure of the AES-GCM-192 decryption operation, including the decryption key/offset vector/aad/aad length| Input |
|input\_data   |AES-GCM-192 ciphertext data to be decrypted           | Input |
|input\_len   |AES-GCM-192 length of ciphertext data to be decrypted。| Input |
|output\_data  |The result of the AES-GCM-192 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-192 decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### aes\_gcm256\_hard\_encrypt

#### Description

AES-GCM-256 encryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm256_hard_encrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name      |  Description                          |Input or output|
|  ------       | -----                         |  ----  |
|context      |The structure of the AES-GCM-256 encryption operation, including the encryption key / offset vector / aad / aad length| Input |
|input\_data   |AES-GCM-256 plaintext data to be encrypted           | Input |
|input\_len   |AES-GCM-256 length of plaintext data to be encrypted。| Input |
|output\_data  |The result of the AES-GCM-256 encryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-256 encryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### aes\_gcm256\_hard\_decrypt

#### Description

AES-GCM-256 decryption operation. When the amount of encrypted data is less than or equal to 896 bytes, cpu is used to transmit data. When it is greater than 896 bytes, dma is used to transmit data, thereby improving the efficiency of calculation.

#### Function prototype

```c
void aes_gcm256_hard_decrypt(gcm_context_t *context, uint8_t *input_data, size_t input_len, uint8_t *output_data, uint8_t *gcm_tag)
```

#### Parameter

| Parameter name    |  Description                          |Input or output|
|  ------   | -----                         |  ----  |
|context |The structure of the AES-GCM-256 decryption operation, including the decryption key/offset vector/aad/aad length| Input |
|input\_data   |AES-GCM-256 ciphertext data to be decrypted           | Input |
|input\_len   |AES-GCM-256 length of ciphertext data to be decrypted。| Input |
|output\_data  |The result of the AES-GCM-256 decryption operation is stored in this buffer.<br/>Since the minimum granularity of DMA handling data is 4bytes,<br/>Therefore, you need to ensure that the buffer size is at least an integer multiple of 4 bytes.| Output |
|gcm\_tag  |The tag after the AES-GCM-256 decryption operation is stored in this buffer.<br/>This buffer size needs to be determined to be 16bytes| Output |

#### Return value

None.

### Example

```c
cbc_context_t cbc_context;
cbc_context.input_key = cbc_key;
cbc_context.iv = cbc_iv;
aes_cbc128_hard_encrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
memcpy(aes_input_data, aes_output_data, 16L);
aes_cbc128_hard_decrypt(&cbc_context, aes_input_data, 16L, aes_output_data);
```

## Data type

The relevant data types and data structures are defined as follows:

- [aes\_cipher\_mode\_t](#aesciphermodet)：AES encryption and decryption mode

### aes\_cipher\_mode\_t

#### Description

AES encryption and decryption mode

#### Type definition

```c
typedef enum _aes_cipher_mode
{
    AES_ECB = 0,
    AES_CBC = 1,
    AES_GCM = 2,
    AES_CIPHER_MAX
} aes_cipher_mode_t;
```

#### Enumeration element

| Element name |          Description          |
| :----------- | :---------------------------- |
| AES\_ECB     | ECB encryption and decryption |
| AES\_CBC     | CBC encryption and decryption |
| AES\_GCM     | GCM encryption and decryption |