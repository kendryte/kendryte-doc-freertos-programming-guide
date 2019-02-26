# 脉冲宽度调制器 (PWM)

## Overview

PWM 用于控制脉冲输出的占空比。

## Features

PWM 模块具有以下功能：

- 配置 PWM Output频率
- 配置 PWM 每个管脚的Output占空比

## API

对应的头文件 `devices.h`

为用户提供以下接口：

- [pwm\_get\_pin\_count](#pwmgetpincount)
- [pwm\_set\_frequency](#pwmsetfrequency)
- [pwm\_set\_active\_duty\_cycle\_percentage](#pwmsetactivedutycyclepercentage)
- [pwm\_set\_enable](#pwmsetenable)

### pwm\_get\_pin\_count

#### Description

获取 PWM 管脚数量。

#### Function prototype

```c
uint32_t pwm_get_pin_count(handle_t file);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| file        | PWM 设备句柄    | Input      |

#### Return value

PWM 管脚数量。

### pwm\_set\_frequency

#### Description

设置 PWM 频率。

#### Function prototype

```c
double pwm_set_frequency(handle_t file, double frequency);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | PWM 设备句柄    | Input      |
| frequency  | 期望的频率（Hz） | Input      |

#### Return value

设置后实际的频率（Hz）。

### pwm\_set\_active\_duty\_cycle\_percentage

#### Description

设置 PWM 管脚占空比。

#### Function prototype

```c
double pwm_set_active_duty_cycle_percentage(handle_t file, uint32_t pin, double duty_cycle_percentage);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | PWM 设备句柄    | Input      |
| pin        | 管脚编号        | Input      |
| duty\_cycle\_percentage  | 期望的占空比 | Input      |

#### Return value

设置后实际的占空比。

### pwm\_set\_enable

#### Description

设置 PWM 管脚是否启用。

#### Function prototype

```c
void pwm_set_enable(handle_t file, uint32_t pin, bool enable);
```

#### Parameter

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| file       | PWM 设备句柄    | Input      |
| pin        | 管脚编号        | Input      |
| enable     | 是否启用        | Input      |

#### Return value

设置后实际的占空比。

### Example

```c
/* pwm0 pin0 Output 200KHZ 占空比为 0.5 的方波 */
handle_t pwm = io_open("/dev/pwm0");
pwm_set_frequency(pwm, 200000);
pwm_set_active_duty_cycle_percentage(pwm, 0, 0.5);
pwm_set_enable(pwm, 0, true);
```