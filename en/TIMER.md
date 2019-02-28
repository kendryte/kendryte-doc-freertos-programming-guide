# TIMER

## Overview

The timer peripheral provides high-precision timing.
The chip has 3 timers, each with 4 channels. Can be configured as PWM, see PWM description for details.

## Features

The TIMER module has the following features:

- Enable or disable the timer
- Configure timer trigger interval
- Configure timer trigger handler

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [timer\_set\_interval](#timersetinterval)
- [timer\_set\_on\_tick](#timersetontick)
- [timer\_set\_enable](#timersetenable)

### timer\_set\_interval

#### Description

Set the timer trigger interval.

#### Function prototype

```c
size_t timer_set_interval(handle_t file, size_t nanoseconds);
```

#### Parameter

| Parameter name |      Description       | Input or output |
| -------------- | ---------------------- | --------------- |
| file           | TIMER device handle    | Input           |
| nanoseconds    | Interval (nanoseconds) | Input           |

#### Return value

Actual trigger interval (nanoseconds).

### timer\_set\_on\_tick

#### Description

Set the handler when the timer is triggered.

#### Function prototype

```c
void timer_set_on_tick(handle_t file, timer_on_tick_t on_tick, void *userdata);
```

#### Parameter

| Parameter name |     Description     | Input or output |
| -------------- | ------------------- | --------------- |
| file           | TIMER device handle | Input           |
| on_tick        | Handler             | Input           |
| userdata       | Handler user data   | Input           |

#### Return value

None.

### timer\_set\_enable

#### Description

Enable or disable the timer.

#### Function prototype

```c
void timer_set_enable(handle_t file, bool enable);
```

#### Parameter

| Parameter name |     Description     | Input or output |
| -------------- | ------------------- | --------------- |
| file           | TIMER device handle | Input           |
| enable         | Whether to enable   | Input           |

#### Return value

None.

### Example

```c
/* Timer 0 Channel 0 timed 1 second print "Time OK!" */
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

The relevant data types and data structures are defined as follows:

- [timer\_on\_tick\_t](#timerontickt): The handler when the timer is triggered.

### timer\_on\_tick\_t

#### Description

The handler when the timer is triggered.

#### Type definition

```c
typedef void (*timer_on_tick_t)(void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| userdata       | User data   | Input           |