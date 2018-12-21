# 看门狗定时器 (WDT)

## 概述

WDT 提供系统出错或无响应时的恢复功能。

## 功能描述

WDT 模块具有以下功能：

- 配置超时时间
- 手动重启计时
- 配置为超时后复位或进入中断
- 进入中断后清除中断可取消复位，否则等待第二次超时后复位

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

- [wdt\_set\_response\_mode](#wdtsetresponsemode)
- [wdt\_set\_timeout](#wdtsettimeout)
- [wdt\_set\_on\_timeout](#wdtsetontimeout)
- [wdt\_restart\_counter](#wdtrestartcounter)
- [wdt\_set\_enable](#wdtsetenable)

### wdt\_set\_response\_mode

#### 描述

设置 WDT 响应模式。

#### 函数原型

```c
void wdt_set_response_mode(handle_t file, wdt_response_mode_t mode);
```

#### 参数

| 参数名称     |   描述         |  输入输出  |
| ----------- | -------------- | --------- |
| file        | WDT 设备句柄    | 输入      |
| mode        | 响应模式        | 输入      |

#### 返回值

无。

### wdt\_set\_timeout

#### 描述

设置 WDT 超时时间。

#### 函数原型

```c
size_t wdt_set_timeout(handle_t file, size_t nanoseconds);
```

#### 参数

| 参数名称     |   描述               |  输入输出  |
| ----------- | -------------------- | --------- |
| file        | WDT 设备句柄          | 输入      |
| nanoseconds | 期望的超时时间（纳秒） | 输入      |

#### 返回值

设置后实际的超时时间（纳秒）。

### wdt\_set\_on\_timeout

#### 描述

设置 WDT 超时处理程序。

#### 函数原型

```c
void wdt_set_on_timeout(handle_t file, wdt_on_timeout_t handler, void *userdata);
```

#### 参数

| 参数名称  |   描述         |  输入输出  |
| -------- | -------------- | --------- |
| file     | WDT 设备句柄    | 输入      |
| handler  | 处理程序        | 输入      |
| userdata | 处理程序用户数据 | 输入      |

#### 返回值

无。

### wdt\_restart\_counter

#### 描述

使 WDT 重新开始计数。

#### 函数原型

```c
void wdt_restart_counter(handle_t file);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | WDT 设备句柄    | 输入      |

#### 返回值

无。

### wdt\_set\_enable

#### 描述

设置 WDT 是否启用。

#### 函数原型

```c
void wdt_set_enable(handle_t file, bool enable);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | WDT 设备句柄    | 输入      |
| enable     | 是否启用        | 输入      |

#### 返回值

无。

### 举例

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

## 数据类型

相关数据类型、数据结构定义如下：

- [wdt\_response\_mode\_t](#wdtresponsemodet)：WDT 响应模式。
- [wdt\_on\_timeout\_t](#wdtontimeoutt)：WDT 超时处理程序。

### wdt\_response\_mode\_t

#### 描述

WDT 响应模式。

#### 定义

```c
typedef enum _wdt_response_mode
{
    WDT_RESP_RESET,
    WDT_RESP_INTERRUPT
} wdt_response_mode_t;
```

#### 成员

| 成员名称             | 描述           |
| -------------------- | ------------- |
| WDT\_RESP\_RESET     | 超时后复位系统 |
| WDT\_RESP\_INTERRUPT | 超时后进入中断，再次超时复位系统 |

### wdt\_on\_timeout\_t

#### 描述

WDT 超时处理程序。

#### 定义

```c
typedef int (*wdt_on_timeout_t)(void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |

#### 返回值

| 返回值 |  描述   |
| ----- | ------- |
| 0     | 不清除中断，系统将复位 |
| 1     | 清除中断，系统不复位   |