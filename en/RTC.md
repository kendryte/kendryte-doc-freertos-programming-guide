# RTC

## Overview

The Real Time Clock (RTC) is a unit for timing and has a timing function after
the set time.

**Note** The RTC unit is only used when PLL0 is enabled and the CPU frequency is greater than 30MHz.

## Features

The RTC unit has the following features:

- Get current date and time
- Set the current date and time
- Set timing interrupt
- Set alarm interrupt

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [rtc\_get\_datetime](#rtcgetdatetime)
- [rtc\_set\_datetime](#rtcsetdatetime)

### rtc\_get\_datetime

#### Description

Get the RTC date and time.

#### Function prototype

```c
void rtc_get_datetime(handle_t file, struct tm *datetime);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | RTC device handle | Input           |
| datetime       | Date time         | Output          |

#### Return value

None.

### rtc\_set\_datetime

#### Description

Set the RTC date and time.

#### Function prototype

```c
void rtc_set_datetime(handle_t file, const struct tm *datetime);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | RTC device handle | Input           |
| datetime       | Date time         | Input           |

#### Return value

None.

### Example

```c
/* Set the date and time, then read the date and time */
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