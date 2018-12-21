# 系统控制

## 概述

系统控制模块提供对操作系统的配置功能。

## 功能描述

系统控制模块具有以下功能：

- 设置 CPU 频率
- 安装自定义驱动

## API 参考

对应的头文件 `hal.h`

为用户提供以下接口：

- [system\_set\_cpu\_frequency](#systemsetcpufrequency)
- [system\_install\_custom\_driver](#systeminstallcustomdriver)

### system\_set\_cpu\_frequency

#### 描述

设置 CPU 频率。

#### 函数原型

```c
uint32_t system_set_cpu_frequency(uint32_t frequency);
```

#### 参数

| 参数名称     |   描述           |  输入输出  |
| ----------- | ---------------- | --------- |
| frequency   | 要设置的频率（Hz） | 输入      |

#### 返回值

设置后的实际频率（Hz）。

### system\_install\_custom\_driver

#### 描述

安装自定义驱动。

#### 函数原型

```c
void system_install_custom_driver(const char *name, const custom_driver_t *driver);
```

#### 参数

| 参数名称     |   描述             |  输入输出  |
| ----------- | ------------------ | --------- |
| name        | 指定访问该设备的路径 | 输入      |
| driver      | 自定义驱动实现      | 输入      |

#### 返回值

无。

### 举例

```c
/* 设置 CPU 频率为 400MHz */
system_set_cpu_frequency(400000000);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [driver\_base\_t](#driverbaset)：驱动实现基类。
- [custom\_driver\_t](#customdrivert)：自定义驱动实现。

### driver\_base\_t

#### 描述

驱动实现基类。

#### 定义

```c
typedef struct _driver_base
{
    void *userdata;
    void (*install)(void *userdata);
    int (*open)(void *userdata);
    void (*close)(void *userdata);
} driver_base_t;
```

#### 成员

| 成员名称   | 描述        |
| --------- | ----------- |
| userdata  | 用户数据     |
| install   | 安装时被调用 |
| open      | 打开时被调用 |
| close     | 关闭时被调用 |

### custom\_driver\_t

#### 描述

自定义驱动实现。

#### 定义

```c
typedef struct _custom_driver
{
    driver_base_t base;
    int (*io_control)(uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len, void *userdata);
} custom_driver_t;
```

#### 成员

| 成员名称     | 描述               |
| ----------- | ------------------ |
| base        | 驱动实现基类        |
| io\_control | 收到控制信息时被调用 |