# 实时时钟 (RTC)

## Overview

RTC 是用来计时的单元，在设置时间后具备计时功能。

## Features

RTC 模块具有以下功能：

- 获取当前日期时刻
- 设置当前日期时刻

## API

对应的头文件 `devices.h`

为用户提供以下接口：

- [rtc\_get\_datetime](#rtcgetdatetime)
- [rtc\_set\_datetime](#rtcsetdatetime)

### rtc\_get\_datetime

#### Description

获取 RTC 日期时刻。

#### Function prototype

```c
void rtc_get_datetime(handle_t file, struct tm *datetime);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| file        | RTC 设备句柄    | 输入      |
| datetime    | 日期时刻        | 输出      |

#### Return value

None.

### rtc\_set\_datetime

#### Description

设置 RTC 日期时刻。

#### Function prototype

```c
void rtc_set_datetime(handle_t file, const struct tm *datetime);
```

#### Parameter

| Parameter name     |   Description           |  Input or output  |
| ----------- | ---------------- | --------- |
| file        | RTC 设备句柄      | 输入      |
| datetime    | 日期时刻          | 输入      |

#### Return value

None.

### Example

```c
/* 设置日期时间，然后读取日期时间 */
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