# 集成電路內置音頻匯流排 (I2S)

## 概述

I2S 標準匯流排定義了三種信號：時脈信號 BCK、聲道選擇信號 WS 和串列資料信號 SD。一個基本的I2S 資料匯流排有一個主機和一個從機。主機和從機的角色在通信過程中保持不變。I2S 模組包含獨立的發送和接收聲道，能夠保證優良的通信性能。

## 功能描述

I2S 模組具有以下功能：

- 根據音頻格式自動配置裝置（支持 16、24、32 位深，44100 採樣率，1 - 4 聲道）
- 可配置為播放或錄音模式
- 自動管理音頻緩衝區

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [i2s\_config\_as\_render](#i2sconfigasrender)
- [i2s\_config\_as\_capture](#i2sconfigascapture)
- [i2s\_get\_buffer](#i2sgetbuffer)
- [i2s\_release\_buffer](#i2sreleasebuffer)
- [i2s\_start](#i2sstart)
- [i2s\_stop](#i2sstop)

### i2s\_config\_as\_render

#### 描述

配置 I2S 控制器為輸出模式。

#### 函數原型

```c
void i2s_config_as_render(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### 參數

| 參數名稱          |   描述             |  輸入輸出  |
| ---------------- | ------------------ | --------- |
| file             | I2S 控制器句柄      | 輸入      |
| format           | 音頻格式            | 輸入      |
| delay\_ms        | 緩衝區長度          | 輸入      |
| align\_mode      | 對齊模式            | 輸入      |
| channels\_mask   | 通道掩碼            | 輸入      |

#### 返回值

無。

### i2s\_config\_as\_capture

#### 描述

配置 I2S 控制器為捕獲模式。

#### 函數原型

```c
void i2s_config_as_capture(handle_t file, const audio_format_t *format, size_t delay_ms, i2s_align_mode_t align_mode, size_t channels_mask);
```

#### 參數

| 參數名稱          |   描述             |  輸入輸出  |
| ---------------- | ------------------ | --------- |
| file             | I2S 控制器句柄      | 輸入      |
| format           | 音頻格式            | 輸入      |
| delay\_ms        | 緩衝區長度          | 輸入      |
| align\_mode      | 對齊模式            | 輸入      |
| channels\_mask   | 通道掩碼            | 輸入      |

#### 返回值

無。

### i2s\_get\_buffer

#### 描述

獲取音頻緩衝區。

#### 函數原型

```c
void i2s_get_buffer(handle_t file, uint8_t **buffer, size_t *frames);
```

#### 參數

| 參數名稱    |   描述        |  輸入輸出  |
| ---------- | ------------- | --------- |
| file       | I2S 控制器句柄 | 輸入       |
| buffer     | 緩衝區         | 輸出       |
| frames     | 緩衝區幀數     | 輸出       |

#### 返回值

無。

### i2s\_release\_buffer

#### 描述

釋放音頻緩衝區。

#### 函數原型

```c
void i2s_release_buffer(handle_t file, size_t frames);
```

#### 參數

| 參數名稱    |   描述               |  輸入輸出  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | 輸入       |
| frames     | 確認已讀取或寫入的幀數 | 輸入       |

#### 返回值

無。

### i2s\_start

#### 描述

開始播放或錄音。

#### 函數原型

```c
void i2s_start(handle_t file);
```

#### 參數

| 參數名稱    |   描述               |  輸入輸出  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | 輸入       |

#### 返回值

無。

### i2s\_stop

#### 描述

停止播放或錄音。

#### 函數原型

```c
void i2s_stop(handle_t file);
```

#### 參數

| 參數名稱    |   描述               |  輸入輸出  |
| ---------- | -------------------- | --------- |
| file       | I2S 控制器句柄        | 輸入       |

#### 返回值

無。

### 舉例

```c
/* 循環播放 PCM 音頻 */
handle_t i2s = io_open("/dev/i2s0");
audio_format_t audio_fmt = { .type = AUDIO_FMT_PCM, .bits_per_sample = 16, .sample_rate = 44100, .channels = 2 };
i2s_config_as_render(i2s, &audio_fmt, 100, I2S_AM_RIGHT, 0b11);
i2s_start(i2s);

while (1)
{
    uint8_t *buffer;
    size_t frames;
    i2s_get_buffer(i2s, &buffer, &frames);
    memcpy(buffer, pcm, 4 * frames);
    i2s_release_buffer(i2s, frames);
    pcm += frames;
    if (pcm >= pcm_end)
        pcm = pcm_start;
}
```

## 資料類型

相關資料類型、資料結構定義如下：

- [audio\_format\_type\_t](#audioformattypet)：音頻格式類型。
- [audio\_format\_t](#[audioformatt)：音頻格式。
- [i2s\_align\_mode\_t](#i2salignmodet)：I2S 對齊模式。

### audio\_format\_type\_t

#### 描述

音頻格式類型。

#### 定義

```c
typedef enum _audio_format_type
{
    AUDIO_FMT_PCM
} audio_format_type_t;
```

#### 成員

| 成員名稱            | 描述        |
| ------------------ | ----------- |
| AUDIO\_FMT\_PCM    | PCM         |

### audio\_format\_t

#### 描述

音頻格式。

#### 定義

```c
typedef struct _audio_format
{
    audio_format_type_t type;
    uint32_t bits_per_sample;
    uint32_t sample_rate;
    uint32_t channels;
} audio_format_t;
```

#### 成員

| 成員名稱           | 描述          |
| ----------------- | ------------- |
| type              | 音頻格式類型   |
| bits\_per\_sample | 採樣深度       |
| sample\_rate      | 採樣率         |
| channels          | 聲道數         |

### i2s\_align\_mode\_t

#### 描述

I2S 對齊模式。

#### 定義

```c
typedef enum _i2s_align_mode
{
    I2S_AM_STANDARD,
    I2S_AM_RIGHT,
    I2S_AM_LEFT
} i2s_align_mode_t;
```

#### 成員

| 成員名稱           | 描述        |
| ----------------- | ----------- |
| I2S\_AM\_STANDARD | 標準模式     |
| I2S\_AM\_RIGHT    | 右對齊       |
| I2S\_AM\_LEFT     | 左對齊       |