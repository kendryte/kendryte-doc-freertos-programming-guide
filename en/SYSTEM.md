# System control (SYSCTL)

## Overview

The system control (SYSCTL) unit can provide configuration functions for the SoC (system on chip).

## Features

The system control module has the following features:

- Set the CPU frequency
- Install custom drivers

## API

Corresponding header file `hal.h`

Provide the following interfaces

- [system\_set\_cpu\_frequency](#systemsetcpufrequency)
- [system\_install\_custom\_driver](#systeminstallcustomdriver)

### system\_set\_cpu\_frequency

#### Description

Set the CPU frequency.

#### Function prototype

```c
uint32_t system_set_cpu_frequency(uint32_t frequency);
```

#### Parameter

| Parameter name |       Description        | Input or output |
| -------------- | ------------------------ | --------------- |
| frequency      | Frequency to be set (Hz) | Input           |

#### Return value

The actual frequency (Hz) after setting.

### system\_install\_custom\_driver

#### Description

Install a custom driver.

#### Function prototype

```c
void system_install_custom_driver(const char *name, const custom_driver_t *driver);
```

#### Parameter

| Parameter name |              Description              | Input or output |
| -------------- | ------------------------------------- | --------------- |
| name           | Specify the path to access the device | Input           |
| driver         | Custom driver implementation          | Input           |

#### Return value

None.

### Example

```c
/* Set the CPU frequency to 400MHz */
system_set_cpu_frequency(400000000);
```

## Data type

The relevant data types and data structures are defined as follows:

- [driver\_base\_t](#driverbaset): The base class for the driver implementation.
- [custom\_driver\_t](#customdrivert): Custom drive implementation.

### driver\_base\_t

#### Description

The base class for the driver implementation.

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

| Element name |        Description         |
| ------------ | -------------------------- |
| userdata     | User data                  |
| install      | Called during installation |
| open         | Called when opened         |
| close        | Called when closed         |

### custom\_driver\_t

#### Description

Custom drive implementation.

#### Type definition

```c
typedef struct _custom_driver
{
    driver_base_t base;
    int (*io_control)(uint32_t control_code, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len, void *userdata);
} custom_driver_t;
```

#### Enumeration element

| Element name |                 Description                 |
| ------------ | ------------------------------------------- |
| base         | Driver implementation base class            |
| io\_control  | Called when control information is received |