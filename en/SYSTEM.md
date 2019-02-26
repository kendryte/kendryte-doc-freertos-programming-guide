# 系统控制

## Overview

系统控制模块提供对操作系统的配置功能。

## Features

系统控制模块具有以下功能：

- 设置 CPU 频率
- 安装自定义驱动

## API

对应的头文件 `hal.h`

为用户提供以下接口：

- [system\_set\_cpu\_frequency](#systemsetcpufrequency)
- [system\_install\_custom\_driver](#systeminstallcustomdriver)

### system\_set\_cpu\_frequency

#### Description

设置 CPU 频率。

#### Function prototype

```c
uint32_t system_set_cpu_frequency(uint32_t frequency);
```

#### Parameter

| Parameter name     |   Description           |  Input or output  |
| ----------- | ---------------- | --------- |
| frequency   | 要设置的频率（Hz） | 输入      |

#### Return value

设置后的实际频率（Hz）。

### system\_install\_custom\_driver

#### Description

安装自定义驱动。

#### Function prototype

```c
void system_install_custom_driver(const char *name, const custom_driver_t *driver);
```

#### Parameter

| Parameter name     |   Description             |  Input or output  |
| ----------- | ------------------ | --------- |
| name        | 指定访问该设备的路径 | 输入      |
| driver      | 自定义驱动实现      | 输入      |

#### Return value

None.

### Example

```c
/* 设置 CPU 频率为 400MHz */
system_set_cpu_frequency(400000000);
```

## Data type

相关数据类型、数据结构定义如下：

- [driver\_base\_t](#driverbaset)：驱动实现基类。
- [custom\_driver\_t](#customdrivert)：自定义驱动实现。

### driver\_base\_t

#### Description

驱动实现基类。

#### Type definition

```c
typedef struct _driver_base
{
    void *userdata;
    void (*install)(void *userdata);
    int (*open)(void *userdata);
    void (*close)(void *userdata);
} driver_base_t;
```

#### Enumeration element

| 成员名称   | Description        |
| --------- | ----------- |
| userdata  | 用户数据     |
| install   | 安装时被调用 |
| open      | 打开时被调用 |
| close     | 关闭时被调用 |

### custom\_driver\_t

#### Description

自定义驱动实现。

#### Type definition

```c
typedef struct _custom_driver
{
    driver_base_t base;
    int (*io_control)(uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len, void *userdata);
} custom_driver_t;
```

#### Enumeration element

| 成员名称     | Description               |
| ----------- | ------------------ |
| base        | 驱动实现基类        |
| io\_control | 收到控制信息时被调用 |