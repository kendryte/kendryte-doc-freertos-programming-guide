# WDT

## Overview

A watchdog timer (WDT) is a hardware timer that automatically generates a system reset if the main program neglects to periodically service it.

## Features

The WDT module has the following features:

- Configure timeout
- Manually set the restart time
- Configure to reset or enter interrupt after timeout
- Clear the interrupt after entering the interrupt to cancel the reset, otherwise wait for the second timeout after reset

## API

Corresponding header file `devices.h`

Provide the following interfaces

- [wdt\_set\_response\_mode](#wdtsetresponsemode)
- [wdt\_set\_timeout](#wdtsettimeout)
- [wdt\_set\_on\_timeout](#wdtsetontimeout)
- [wdt\_restart\_counter](#wdtrestartcounter)
- [wdt\_set\_enable](#wdtsetenable)

### wdt\_set\_response\_mode

#### Description

Set the WDT response mode.

#### Function prototype

```c
void wdt_set_response_mode(handle_t file, wdt_response_mode_t mode);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | WDT device handle | Input           |
| mode           | Response mode     | Input           |

#### Return value

None.

### wdt\_set\_timeout

#### Description

Set the WDT timeout period.

#### Function prototype

```c
size_t wdt_set_timeout(handle_t file, size_t nanoseconds);
```

#### Parameter

| Parameter name |          Description           | Input or output |
| -------------- | ------------------------------ | --------------- |
| file           | WDT device handle              | Input           |
| nanoseconds    | Expected timeout (nanoseconds) | Input           |

#### Return value

The actual timeout (nanoseconds) after setting.

### wdt\_set\_on\_timeout

#### Description

Set the WDT timeout handler.

#### Function prototype

```c
void wdt_set_on_timeout(handle_t file, wdt_on_timeout_t handler, void *userdata);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | WDT device handle | Input           |
| handler        | Handler           | Input           |
| userdata       | Handler user data | Input           |

#### Return value

None.

### wdt\_restart\_counter

#### Description

Let the WDT restart counting.

#### Function prototype

```c
void wdt_restart_counter(handle_t file);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | WDT device handle | Input           |

#### Return value

None.

### wdt\_set\_enable

#### Description

Set whether WDT is enabled.

#### Function prototype

```c
void wdt_set_enable(handle_t file, bool enable);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| file           | WDT device handle | Input           |
| enable         | Whether to enable | Input           |

#### Return value

None.

### Example

```c
/*
 * After 2 seconds, enter the watchdog interrupt function to print Hello_world,
 * and then reset after 2 seconds.
 */
void on_timeout(void *unused)
{
    printf("Timeout\n");
}

handle_t wdt = io_open("/dev/wdt0");

wdt_set_response_mode(wdt, WDT_RESP_INTERRUPT);
wdt_set_timeout(wdt, 2e9);
wdt_set_on_timeout(wdt, on_timeout, NULL);
wdt_set_enable(wdt, true);
```

## Data type

The relevant data types and data structures are defined as follows:

- [wdt\_response\_mode\_t](#wdtresponsemodet): WDT Response mode.
- [wdt\_on\_timeout\_t](#wdtontimeoutt): WDT timeout handler.

### wdt\_response\_mode\_t

#### Description

WDT Response mode.

#### Type definition

```c
typedef enum _wdt_response_mode
{
    WDT_RESP_RESET,
    WDT_RESP_INTERRUPT
} wdt_response_mode_t;
```

#### Enumeration element

|     Element name     |                                Description                                |
| -------------------- | ------------------------------------------------------------------------- |
| WDT\_RESP\_RESET     | Reset system after timeout                                                |
| WDT\_RESP\_INTERRUPT | Enter the interrupt after timeout, reset the system if it times out again |

### wdt\_on\_timeout\_t

#### Description

WDT timeout handler.

#### Type definition

```c
typedef int (*wdt_on_timeout_t)(void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| userdata       | User data   | Input           |

#### Return value

| Return value |                      Description                       |
| ------------ | ------------------------------------------------------ |
| 0            | The interrupt is not cleared and the system will reset |
| 1            | Clear interrupt, system does not reset                 |
