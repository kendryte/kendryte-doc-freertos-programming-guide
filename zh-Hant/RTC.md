# 實時時脈 (RTC)

## 概述

RTC 是用來計時的單元，在設置時間後具備計時功能。

## 功能描述

RTC 模組具有以下功能：

- 獲取當前日期時刻
- 設置當前日期時刻

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [rtc\_get\_datetime](#rtcgetdatetime)
- [rtc\_set\_datetime](#rtcsetdatetime)

### rtc\_get\_datetime

#### 描述

獲取 RTC 日期時刻。

#### 函數原型

```c
void rtc_get_datetime(handle_t file, struct tm *datetime);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| file        | RTC 裝置句柄    | 輸入      |
| datetime    | 日期時刻        | 輸出      |

#### 返回值

無。

### rtc\_set\_datetime

#### 描述

設置 RTC 日期時刻。

#### 函數原型

```c
void rtc_set_datetime(handle_t file, const struct tm *datetime);
```

#### 參數

| 參數名稱     |   描述           |  輸入輸出  |
| ----------- | ---------------- | --------- |
| file        | RTC 裝置句柄      | 輸入      |
| datetime    | 日期時刻          | 輸入      |

#### 返回值

無。

### 舉例

```c
/* 設置日期時間，然後讀取日期時間 */
handle_t rtc = io_open("/dev/rtc0");

struct tm time =
{
    .tm_year = 2018,
    .tm_mon = 10,
    .tm_mday = 11,
    .tm_hour = 12
};
rtc_set_datetime(rtc, &time);
rtc_get_datetime(rtc, &time);
```