# 看门狗定时器 (WDT)

## Overview

WDT 提供系统出错或无响应时的恢复功能。

## Features

WDT 模块具有以下功能：

- 配置超时时间
- 手动重启计时
- 配置为超时后复位或进入中断
- 进入中断后清除中断可取消复位，否则等待第二次超时后复位

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [wdt\_set\_response\_mode](#wdtsetresponsemode)
- [wdt\_set\_timeout](#wdtsettimeout)
- [wdt\_set\_on\_timeout](#wdtsetontimeout)
- [wdt\_restart\_counter](#wdtrestartcounter)
- [wdt\_set\_enable](#wdtsetenable)

### wdt\_set\_response\_mode

#### Description

设置 WDT 响应模式。

#### Function prototype

```c
void wdt_set_response_mode(handle_t file, wdt_response_mode_t mode);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| file        | WDT device handle    | Input      |
| mode        | 响应模式        | Input      |

#### Return value

None.

### wdt\_set\_timeout

#### Description

设置 WDT 超时时间。

#### Function prototype

```c
size_t wdt_set_timeout(handle_t file, size_t nanoseconds);
```

#### Parameter

| Parameter name     |   Description               |  Input or output  |
| ----------- | -------------------- | --------- |
| file        | WDT device handle          | Input      |
| nanoseconds | 期望的超时时间（纳秒） | Input      |

#### Return value

设置后实际的超时时间（纳秒）。

### wdt\_set\_on\_timeout

#### Description

设置 WDT 超时处理程序。

#### Function prototype

```c
void wdt_set_on_timeout(handle_t file, wdt_on_timeout_t handler, void *userdata);
```

#### Parameter

| Parameter name  |   Description         |  Input or output  |
| -------- | -------------- | --------- |
| file     | WDT device handle    | Input      |
| handler  | 处理程序        | Input      |
| userdata | 处理程序用户数据 | Input      |

#### Return value

None.

### wdt\_restart\_counter

#### Description

使 WDT 重新开始计数。

#### Function prototype

```c
void wdt_restart_counter(handle_t file);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | WDT device handle    | Input      |

#### Return value

None.

### wdt\_set\_enable

#### Description

设置 WDT 是否启用。

#### Function prototype

```c
void wdt_set_enable(handle_t file, bool enable);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | WDT device handle    | Input      |
| enable     | 是否启用        | Input      |

#### Return value

None.

### Example

```c
/* 2 秒后进入看门狗中断函数打印 Timeout，再过 2 秒复位 */
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

## Data type

The relevant data types and data structures are defined as follows:

- [wdt\_response\_mode\_t](#wdtresponsemodet)：WDT 响应模式。
- [wdt\_on\_timeout\_t](#wdtontimeoutt)：WDT 超时处理程序。

### wdt\_response\_mode\_t

#### Description

WDT 响应模式。

#### Type definition

```c
typedef enum _wdt_response_mode
{
    WDT_RESP_RESET,
    WDT_RESP_INTERRUPT
} wdt_response_mode_t;
```

#### Enumeration element

| Element name             | Description           |
| -------------------- | ------------- |
| WDT\_RESP\_RESET     | 超时后复位系统 |
| WDT\_RESP\_INTERRUPT | 超时后进入中断，再次超时复位系统 |

### wdt\_on\_timeout\_t

#### Description

WDT 超时处理程序。

#### Type definition

```c
typedef int (*wdt_on_timeout_t)(void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | Input      |

#### Return value

| 返回值 |  Description   |
| ----- | ------- |
| 0     | 不清除中断，系统将复位 |
| 1     | 清除中断，系统不复位   |