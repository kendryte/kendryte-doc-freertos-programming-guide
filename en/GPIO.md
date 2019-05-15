# GPIO

## Overview

GPIO stands for General Purpose Input Output.
The chip has 32 high-speed GPIOs and 8 general-purpose GPIOs.

## Features

The GPIO unit has the following features:

- Configurable up and down drive mode
- Support for rising edge, falling edge and double edge trigger

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [gpio\_get\_pin\_count](#gpiogetpincount)
- [gpio\_set\_drive\_mode](#gpiosetdrivemode)
- [gpio\_set\_pin\_edge](#gpiosetpinedge)
- [gpio\_set\_on_\changed](#gpiosetonchanged)
- [gpio\_get\_pin\_value](#gpiogetpinvalue)
- [gpio\_set\_pin\_value](#gpiosetpinvalue)

### gpio\_get\_pin\_count

#### Description

Get the GPIO pin count.

#### Function prototype

```c
uint32_t gpio_get_pin_count(handle_t file);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |

#### Return value

Pin count.

### gpio\_set\_drive\_mode

#### Description

Set the GPIO pin drive mode.

#### Function prototype

```c
void gpio_set_drive_mode(handle_t file, uint32_t pin, gpio_drive_mode_t mode);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |
| pin            | Pin number             | Input           |
| mode           | Drive mode             | Input           |

#### Return value

None.

### gpio\_set\_pin\_edge

#### Description

Set the GPIO pin edge trigger mode.

**Note:**`/dev/gpio1` is not supported this function.

#### Function prototype

```c
void gpio_set_pin_edge(handle_t file, uint32_t pin, gpio_pin_edge_t edge);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |
| pin            | Pin number             | Input           |
| edge           | Edge trigger mode      | Input           |

#### Return value

None.

### gpio\_set\_on\_changed

#### Description

Set the GPIO pin edge trigger handler.

**Note:**`/dev/gpio1` is not supported this function.

#### Function prototype

```c
void gpio_set_on_changed(handle_t file, uint32_t pin, gpio_on_changed_t callback, void *userdata);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |
| pin            | Pin number             | Input           |
| callback       | Handler                | Input           |
| userdata       | Handler user data      | Input           |

#### Return value

None.

### gpio\_get\_pin\_value

#### Description

Get the value of the GPIO pin.

#### Function prototype

```c
gpio_pin_value_t gpio_get_pin_value(handle_t file, uint32_t pin);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |
| pin            | Pin number             | Input           |

#### Return value

The value of the GPIO pin.

### gpio\_set\_pin\_value

#### Description

Set the value of the GPIO pin.

#### Function prototype

```c
void gpio_set_pin_value(handle_t file, uint32_t pin, gpio_pin_value_t value);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | GPIO controller handle | Input           |
| pin            | Pin number             | Input           |
| value          | The value to set       | Input           |

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

- [gpio\_drive\_mode\_t](#gpiodrivemodet): GPIO drive mode.
- [gpio\_pin\_edge\_t](#gpiopinedget): GPIO edge trigger mode.
- [gpio\_pin\_value\_t](#gpiopinvaluet): GPIO value.
- [gpio\_on\_changed\_t](#gpioonchangedt): GPIO edge trigger handler。

### gpio\_drive\_mode\_t

#### Description

GPIO drive mode.

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

|        Element name         |   Description   |
| --------------------------- | --------------- |
| GPIO\_DM\_INPUT             | Input           |
| GPIO\_DM\_INPUT\_PULL\_DOWN | Input pull down |
| GPIO\_DM\_INPUT\_PULL\_UP   | Input pull up   |
| GPIO\_DM\_OUTPUT            | Output          |

### gpio\_pin\_edge\_t

#### Description

GPIO edge trigger mode.

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

|   Element name    |     Description      |
| ----------------- | -------------------- |
| GPIO\_PE\_NONE    | Do not trigger       |
| GPIO\_PE\_FALLING | Falling edge trigger |
| GPIO\_PE\_RISING  | Rising edge trigger  |
| GPIO\_PE\_BOTH    | Double edge trigger  |

### gpio\_pin\_value\_t

#### Description

GPIO value.

#### Type definition

```c
typedef enum _gpio_pin_value
{
    GPIO_PV_LOW,
    GPIO_PV_HIGH
} gpio_pin_value_t;
```

#### Enumeration element

|  Element name  | Description |
| -------------- | ----------- |
| GPIO\_PV\_LOW  | Low         |
| GPIO\_PV\_HIGH | High        |

### gpio\_on_changed\_t

#### Description

GPIO edge trigger handler。

#### Type definition

```c
typedef void (*gpio_on_changed_t)(uint32_t pin, void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| pin            | Pin number  | Input           |
| userdata       | User data   | Input           |