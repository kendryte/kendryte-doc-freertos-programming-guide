# 看門狗定時器 (WDT)

## 概述

WDT 提供系統出錯或無響應時的恢復功能。

## 功能描述

WDT 模組具有以下功能：

- 配置超時時間
- 手動重啟計時
- 配置為超時後複位或進入中斷
- 進入中斷後清除中斷可取消複位，否則等待第二次超時後複位

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [wdt\_set\_response\_mode](#wdtsetresponsemode)
- [wdt\_set\_timeout](#wdtsettimeout)
- [wdt\_set\_on\_timeout](#wdtsetontimeout)
- [wdt\_restart\_counter](#wdtrestartcounter)
- [wdt\_set\_enable](#wdtsetenable)

### wdt\_set\_response\_mode

#### 描述

設置 WDT 響應模式。

#### 函數原型

```c
void wdt_set_response_mode(handle_t file, wdt_response_mode_t mode);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| file        | WDT 裝置句柄    | 輸入      |
| mode        | 響應模式        | 輸入      |

#### 返回值

無。

### wdt\_set\_timeout

#### 描述

設置 WDT 超時時間。

#### 函數原型

```c
size_t wdt_set_timeout(handle_t file, size_t nanoseconds);
```

#### 參數

| 參數名稱     |   描述               |  輸入輸出  |
| ----------- | -------------------- | --------- |
| file        | WDT 裝置句柄          | 輸入      |
| nanoseconds | 期望的超時時間（納秒） | 輸入      |

#### 返回值

設置後實際的超時時間（納秒）。

### wdt\_set\_on\_timeout

#### 描述

設置 WDT 超時處理程序。

#### 函數原型

```c
void wdt_set_on_timeout(handle_t file, wdt_on_timeout_t handler, void *userdata);
```

#### 參數

| 參數名稱  |   描述         |  輸入輸出  |
| -------- | -------------- | --------- |
| file     | WDT 裝置句柄    | 輸入      |
| handler  | 處理程序        | 輸入      |
| userdata | 處理程序用戶資料 | 輸入      |

#### 返回值

無。

### wdt\_restart\_counter

#### 描述

使 WDT 重新開始計數。

#### 函數原型

```c
void wdt_restart_counter(handle_t file);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | WDT 裝置句柄    | 輸入      |

#### 返回值

無。

### wdt\_set\_enable

#### 描述

設置 WDT 是否啟用。

#### 函數原型

```c
void wdt_set_enable(handle_t file, bool enable);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | WDT 裝置句柄    | 輸入      |
| enable     | 是否啟用        | 輸入      |

#### 返回值

無。

### 舉例

```c
/* 2 秒後進入看門狗中斷函數列印 Timeout，再過 2 秒複位 */
void on_timeout(void *unused)
{
    printf("Timeout\n");
}

handle_t wdt = io_open("/dev/wdt0");

wdt_set_response_mode(wdt, WDT_RESP_INTERRUPT);
wdt_set_timeout(wdt, 2e9);
wdt_set_on_timeout(wdt, on_timeout, NULL);
wdt_set_enable(wdt, true);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [wdt\_response\_mode\_t](#wdtresponsemodet)：WDT 響應模式。
- [wdt\_on\_timeout\_t](#wdtontimeoutt)：WDT 超時處理程序。

### wdt\_response\_mode\_t

#### 描述

WDT 響應模式。

#### 定義

```c
typedef enum _wdt_response_mode
{
    WDT_RESP_RESET,
    WDT_RESP_INTERRUPT
} wdt_response_mode_t;
```

#### 成員

| 成員名稱             | 描述           |
| -------------------- | ------------- |
| WDT\_RESP\_RESET     | 超時後複位系統 |
| WDT\_RESP\_INTERRUPT | 超時後進入中斷，再次超時複位系統 |

### wdt\_on\_timeout\_t

#### 描述

WDT 超時處理程序。

#### 定義

```c
typedef int (*wdt_on_timeout_t)(void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| userdata   | 用戶資料        | 輸入      |

#### 返回值

| 返回值 |  描述   |
| ----- | ------- |
| 0     | 不清除中斷，系統將複位 |
| 1     | 清除中斷，系統不複位   |