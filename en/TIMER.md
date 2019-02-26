# 定时器 (TIMER)

## Overview

TIMER 提供高精度定时功能。

## Features

TIMER 模块具有以下功能：

- 启用或禁用定时器
- 配置定时器触发间隔
- 配置定时器触发处理程序

## API

对应的头文件 `devices.h`

为用户提供以下接口：

- [timer\_set\_interval](#timersetinterval)
- [timer\_set\_on\_tick](#timersetontick)
- [timer\_set\_enable](#timersetenable)

### timer\_set\_interval

#### Description

设置 TIMER 触发间隔。

#### Function prototype

```c
size_t timer_set_interval(handle_t file, size_t nanoseconds);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| file        | TIMER 设备句柄  | 输入      |
| nanoseconds | 间隔（纳秒）    | 输入       |

#### Return value

实际的触发间隔（纳秒）。

### timer\_set\_on\_tick

#### Description

设置 TIMER 触发时的处理程序。

#### Function prototype

```c
void timer_set_on_tick(handle_t file, timer_on_tick_t on_tick, void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | TIMER 设备句柄  | 输入      |
| on_tick    | 处理程序        | 输入      |
| userdata   | 处理程序用户数据 | 输入      |

#### Return value

None.

### timer\_set\_enable

#### Description

设置 TIMER 是否启用。

#### Function prototype

```c
void timer_set_enable(handle_t file, bool enable);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | TIMER 设备句柄 | 输入      |
| enable     | 是否启用        | 输入      |

#### Return value

None.

### Example

```c
/* 定时器0  定时 1 秒打印 Time OK! */
void on_tick(void *unused)
{
    printf("Time OK!\n");
}

handle_t timer = io_open("/dev/timer0");

timer_set_interval(timer, 1e9);
timer_set_on_tick(timer, on_tick, NULL);
timer_set_enable(timer, true);
```

## Data type

相关数据类型、数据结构定义如下：

- [timer\_on\_tick\_t](#timerontickt)：TIMER 触发时的处理程序。

### timer\_on\_tick\_t

#### Description

TIMER 触发时的处理程序。

#### Type definition

```c
typedef void (*timer_on_tick_t)(void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |