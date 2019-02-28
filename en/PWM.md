# PWM

## Overview

A pulse width modulator (PWM) is used to control the duty cycle of the pulse output.
It is essentially a timer, so be careful not to conflict with the timer when setting the PWM number and channel.

## Features

The PWM module has the following features:

- Configure the PWM output frequency
- Configure the output duty cycle of each pin of the PWM

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [pwm\_get\_pin\_count](#pwmgetpincount)
- [pwm\_set\_frequency](#pwmsetfrequency)
- [pwm\_set\_active\_duty\_cycle\_percentage](#pwmsetactivedutycyclepercentage)
- [pwm\_set\_enable](#pwmsetenable)

### pwm\_get\_pin\_count

#### Description

Get the number of PWM pins.

#### Function prototype

```c
uint32_t pwm_get_pin_count(handle_t file);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | PWM device handle | Input           |

#### Return value

The number of PWM pins.

### pwm\_set\_frequency

#### Description

Set the PWM frequency.

#### Function prototype

```c
double pwm_set_frequency(handle_t file, double frequency);
```

#### Parameter

| Parameter name |       Description       | Input or output |
| -------------- | ----------------------- | --------------- |
| file           | PWM device handle       | Input           |
| frequency      | Expected frequency (Hz) | Input           |

#### Return value

The actual frequency (Hz) after setting.

### pwm\_set\_active\_duty\_cycle\_percentage

#### Description

Set the PWM pin duty cycle.

#### Function prototype

```c
double pwm_set_active_duty_cycle_percentage(handle_t file, uint32_t pin, double duty_cycle_percentage);
```

#### Parameter

|     Parameter name      |     Description     | Input or output |
| ----------------------- | ------------------- | --------------- |
| file                    | PWM device handle   | Input           |
| pin                     | Pin number          | Input           |
| duty\_cycle\_percentage | Expected duty cycle | Input           |

#### Return value

The actual duty cycle after setting.

### pwm\_set\_enable

#### Description

Set whether the PWM pin is enabled.

#### Function prototype

```c
void pwm_set_enable(handle_t file, uint32_t pin, bool enable);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | PWM device handle | Input           |
| pin            | Pin number        | Input           |
| enable         | Whether to enable | Input           |

#### Return value

The actual duty cycle after setting.

### Example

```c
/* pwm0 pin0 output 200KHz square wave with duty cycle of 0.5 */
handle_t pwm = io_open("/dev/pwm0");
pwm_set_frequency(pwm, 200000);
pwm_set_active_duty_cycle_percentage(pwm, 0, 0.5);
pwm_set_enable(pwm, 0, true);
```
