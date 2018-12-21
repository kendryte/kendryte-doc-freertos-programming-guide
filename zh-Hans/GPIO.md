# 通用输入/输出 (GPIO)

## 概述

芯片有 32 个高速 GPIO 和 8 个通用 GPIO。

## 功能描述

GPIO 模块具有以下功能：

- 可配置上下拉驱动模式
- 支持上升沿、下降沿和双沿触发

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

- [gpio\_get\_pin\_count](#gpiogetpincount)
- [gpio\_set\_drive\_mode](#gpiosetdrivemode)
- [gpio\_set\_pin\_edge](#gpiosetpinedge)
- [gpio\_set\_on_\changed](#gpiosetonchanged)
- [gpio\_get\_pin\_value](#gpiogetpinvalue)
- [gpio\_set\_pin\_value](#gpiosetpinvalue)

### gpio\_get\_pin\_count

#### 描述

获取 GPIO 管脚数量。

#### 函数原型

```c
uint32_t gpio_get_pin_count(handle_t file);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |

#### 返回值

管脚数量。

### gpio\_set\_drive\_mode

#### 描述

设置 GPIO 管脚驱动模式。

#### 函数原型

```c
void gpio_set_drive_mode(handle_t file, uint32_t pin, gpio_drive_mode_t mode);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |
| pin        | 管脚编号        | 输入      |
| mode       | 驱动模式        | 输入      |

#### 返回值

无。

### gpio\_set\_pin\_edge

#### 描述

设置 GPIO 管脚边沿触发模式。

**注：**`/dev/gpio1` 暂不支持。

#### 函数原型

```c
void gpio_set_pin_edge(handle_t file, uint32_t pin, gpio_pin_edge_t edge);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |
| pin        | 管脚编号        | 输入      |
| edge       | 边沿触发模式    | 输入      |

#### 返回值

无。

### gpio\_set\_on\_changed

#### 描述

设置 GPIO 管脚边沿触发处理程序。

**注：**`/dev/gpio1` 暂不支持。

#### 函数原型

```c
void gpio_set_on_changed(handle_t file, uint32_t pin, gpio_on_changed_t callback, void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |
| pin        | 管脚编号        | 输入      |
| callback   | 处理程序        | 输入      |
| userdata   | 处理程序用户数据 | 输入      |

#### 返回值

无。

### gpio\_get\_pin\_value

#### 描述

获取 GPIO 管脚的值。

#### 函数原型

```c
gpio_pin_value_t gpio_get_pin_value(handle_t file, uint32_t pin);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |
| pin        | 管脚编号        | 输入      |

#### 返回值

GPIO 管脚的值。

### gpio\_set\_pin\_value

#### 描述

设置 GPIO 管脚的值。

#### 函数原型

```c
void gpio_set_pin_value(handle_t file, uint32_t pin, gpio_pin_value_t value);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | 输入      |
| pin        | 管脚编号        | 输入      |
| value      | 要设置的值      | 输入      |

#### 返回值

无。

### 举例

```c
handle_t gpio = io_open("/dev/gpio0");

gpio_set_drive_mode(gpio, 0, GPIO_DM_OUTPUT);
gpio_set_pin_value(gpio, 0, GPIO_PV_LOW);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [gpio\_drive\_mode\_t](#gpiodrivemodet)：GPIO 驱动模式。
- [gpio\_pin\_edge\_t](#gpiopinedget)：GPIO 边沿触发模式。
- [gpio\_pin\_value\_t](#gpiopinvaluet)：GPIO 值。
- [gpio\_on\_changed\_t](#gpioonchangedt)：GPIO 边沿触发处理程序。

### gpio\_drive\_mode\_t

#### 描述

GPIO 驱动模式。

#### 定义

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT
} gpio_drive_mode_t;
```

#### 成员

| 成员名称                     | 描述        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | 输入        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | 输入下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | 输入上拉     |
| GPIO\_DM\_OUTPUT            | 输出         |

### gpio\_pin\_edge\_t

#### 描述

GPIO 边沿触发模式。

#### 定义

```c
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH
} gpio_pin_edge_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不触发      |
| GPIO\_PE\_FALLING  | 下降沿触发  |
| GPIO\_PE\_RISING   | 上升沿触发  |
| GPIO\_PE\_BOTH     | 双沿触发    |

### gpio\_pin\_value\_t

#### 描述

GPIO 值。

#### 定义

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### 成员

| 成员名称            | 描述        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |

### gpio\_on_changed\_t

#### 描述

GPIO 边沿触发处理程序。

#### 定义

```c
typedef void (*gpio_on_changed_t)(uint32_t pin, void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| pin        | 管脚编号        | 输入      |
| userdata   | 用户数据        | 输入      |