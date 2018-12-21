# 定时器 (TIMER)

## 概述

TIMER 提供高精度定时功能。

## 功能描述

TIMER 模块具有以下功能：

- 启用或禁用定时器
- 配置定时器触发间隔
- 配置定时器触发处理程序

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

- [timer\_set\_interval](#timersetinterval)
- [timer\_set\_on\_tick](#timersetontick)
- [timer\_set\_enable](#timersetenable)

### timer\_set\_interval

#### 描述

设置 TIMER 触发间隔。

#### 函数原型

```c
size_t timer_set_interval(handle_t file, size_t nanoseconds);
```

#### 参数

| 参数名称     |   描述         |  输入输出  |
| ----------- | -------------- | --------- |
| file        | TIMER 设备句柄  | 输入      |
| nanoseconds | 间隔（纳秒）    | 输入       |

#### 返回值

实际的触发间隔（纳秒）。

### timer\_set\_on\_tick

#### 描述

设置 TIMER 触发时的处理程序。

#### 函数原型

```c
void timer_set_on_tick(handle_t file, timer_on_tick_t on_tick, void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | TIMER 设备句柄  | 输入      |
| on_tick    | 处理程序        | 输入      |
| userdata   | 处理程序用户数据 | 输入      |

#### 返回值

无。

### timer\_set\_enable

#### 描述

设置 TIMER 是否启用。

#### 函数原型

```c
void timer_set_enable(handle_t file, bool enable);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | TIMER 设备句柄 | 输入      |
| enable     | 是否启用        | 输入      |

#### 返回值

无。

### 举例

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

## 数据类型

相关数据类型、数据结构定义如下：

- [timer\_on\_tick\_t](#timerontickt)：TIMER 触发时的处理程序。

### timer\_on\_tick\_t

#### 描述

TIMER 触发时的处理程序。

#### 定义

```c
typedef void (*timer_on_tick_t)(void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |