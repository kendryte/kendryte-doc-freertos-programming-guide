# 通用输入/Output (GPIO)

## Overview

芯片有 32 个高速 GPIO 和 8 个通用 GPIO。

## Features

GPIO 模块具有以下功能：

- 可配置上下拉驱动模式
- 支持上升沿、下降沿和双沿触发

## API

对应的头文件 `devices.h`

为用户提供以下接口：

- [gpio\_get\_pin\_count](#gpiogetpincount)
- [gpio\_set\_drive\_mode](#gpiosetdrivemode)
- [gpio\_set\_pin\_edge](#gpiosetpinedge)
- [gpio\_set\_on_\changed](#gpiosetonchanged)
- [gpio\_get\_pin\_value](#gpiogetpinvalue)
- [gpio\_set\_pin\_value](#gpiosetpinvalue)

### gpio\_get\_pin\_count

#### Description

获取 GPIO 管脚数量。

#### Function prototype

```c
uint32_t gpio_get_pin_count(handle_t file);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |

#### Return value

管脚数量。

### gpio\_set\_drive\_mode

#### Description

设置 GPIO 管脚驱动模式。

#### Function prototype

```c
void gpio_set_drive_mode(handle_t file, uint32_t pin, gpio_drive_mode_t mode);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |
| pin        | 管脚编号        | Input      |
| mode       | 驱动模式        | Input      |

#### Return value

None.

### gpio\_set\_pin\_edge

#### Description

设置 GPIO 管脚边沿触发模式。

**注：**`/dev/gpio1` 暂不支持。

#### Function prototype

```c
void gpio_set_pin_edge(handle_t file, uint32_t pin, gpio_pin_edge_t edge);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |
| pin        | 管脚编号        | Input      |
| edge       | 边沿触发模式    | Input      |

#### Return value

None.

### gpio\_set\_on\_changed

#### Description

设置 GPIO 管脚边沿触发处理程序。

**注：**`/dev/gpio1` 暂不支持。

#### Function prototype

```c
void gpio_set_on_changed(handle_t file, uint32_t pin, gpio_on_changed_t callback, void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |
| pin        | 管脚编号        | Input      |
| callback   | 处理程序        | Input      |
| userdata   | 处理程序用户数据 | Input      |

#### Return value

None.

### gpio\_get\_pin\_value

#### Description

获取 GPIO 管脚的值。

#### Function prototype

```c
gpio_pin_value_t gpio_get_pin_value(handle_t file, uint32_t pin);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |
| pin        | 管脚编号        | Input      |

#### Return value

GPIO 管脚的值。

### gpio\_set\_pin\_value

#### Description

设置 GPIO 管脚的值。

#### Function prototype

```c
void gpio_set_pin_value(handle_t file, uint32_t pin, gpio_pin_value_t value);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | GPIO 控制器句柄 | Input      |
| pin        | 管脚编号        | Input      |
| value      | 要设置的值      | Input      |

#### Return value

None.

### Example

```c
handle_t gpio = io_open("/dev/gpio0");

gpio_set_drive_mode(gpio, 0, GPIO_DM_OUTPUT);
gpio_set_pin_value(gpio, 0, GPIO_PV_LOW);
```

## Data type

The relevant data types and data structures are defined as follows:

- [gpio\_drive\_mode\_t](#gpiodrivemodet)：GPIO 驱动模式。
- [gpio\_pin\_edge\_t](#gpiopinedget)：GPIO 边沿触发模式。
- [gpio\_pin\_value\_t](#gpiopinvaluet)：GPIO 值。
- [gpio\_on\_changed\_t](#gpioonchangedt)：GPIO 边沿触发处理程序。

### gpio\_drive\_mode\_t

#### Description

GPIO 驱动模式。

#### Type definition

```c
typedef enum _gpio_drive_mode
{
    GPIO_DM_INPUT,
    GPIO_DM_INPUT_PULL_DOWN,
    GPIO_DM_INPUT_PULL_UP,
    GPIO_DM_OUTPUT
} gpio_drive_mode_t;
```

#### Enumeration element

| Element name                     | Description        |
| --------------------------- | ----------- |
| GPIO\_DM\_INPUT             | Input        |
| GPIO\_DM\_INPUT\_PULL\_DOWN | Input下拉     |
| GPIO\_DM\_INPUT\_PULL\_UP   | Input上拉     |
| GPIO\_DM\_OUTPUT            | Output         |

### gpio\_pin\_edge\_t

#### Description

GPIO 边沿触发模式。

#### Type definition

```c
typedef enum _gpio_pin_edge
{
    GPIO_PE_NONE,
    GPIO_PE_FALLING,
    GPIO_PE_RISING,
    GPIO_PE_BOTH
} gpio_pin_edge_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| GPIO\_PE\_NONE     | 不触发      |
| GPIO\_PE\_FALLING  | 下降沿触发  |
| GPIO\_PE\_RISING   | 上升沿触发  |
| GPIO\_PE\_BOTH     | 双沿触发    |

### gpio\_pin\_value\_t

#### Description

GPIO 值。

#### Type definition

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### Enumeration element

| Element name            | Description        |
| ------------------ | ----------- |
| GPIO\_PV\_LOW      | 低          |
| GPIO\_PV\_HIGH     | 高          |

### gpio\_on_changed\_t

#### Description

GPIO 边沿触发处理程序。

#### Type definition

```c
typedef void (*gpio_on_changed_t)(uint32_t pin, void *userdata);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| pin        | 管脚编号        | Input      |
| userdata   | 用户数据        | Input      |