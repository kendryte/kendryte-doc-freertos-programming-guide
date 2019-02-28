# PIC

## Overview

Programmable Interrupt Controller (PIC).

Any external interrupt source can be individually assigned to an external interrupt on each CPU. This provides great flexibility to adapt to different application needs.

## Features

The PIC module has the following features:

- Enable or disable interrupts
- Set the interrupt handler
- Configure interrupt priority

## API

Corresponding header file `hal.h`

Provide the following interfaces

- [pic\_set\_irq\_enable](#picsetirqenable)
- [pic\_set\_irq\_handler](#picsetirqhandler)
- [pic\_set\_irq\_priority](#picsetirqpriority)

### pic\_set\_irq\_enable

#### Description

Set whether IRQ is enabled.

#### Function prototype

```c
void pic_set_irq_enable(uint32_t irq, bool enable);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| irq            | IRQ number        | Input           |
| enable         | Whether to enable | Input           |

#### Return value

None.

### pic\_set\_irq\_handler

#### Description

Set the IRQ Handler.

#### Function prototype

```c
void pic_set_irq_handler(uint32_t irq, pic_irq_handler_t handler, void *userdata);
```

#### Parameter

| Parameter name |    Description    | Input or output |
| -------------- | ----------------- | --------------- |
| irq            | IRQ number        | Input           |
| handler        | Handler           | Input           |
| userdata       | Handler user data | Input           |

#### Return value

None.

### pic\_set\_irq\_priority

#### Description

Set the IRQ priority.

#### Function prototype

```c
void pic_set_irq_priority(uint32_t irq, uint32_t priority);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| irq            | IRQ number  | Input           |
| priority       | Priority    | Input           |

#### Return value

None.

## Data type

The relevant data types and data structures are defined as follows:

- [pic\_irq\_handler\_t](#picirqhandlert): IRQ Handler。

### pic\_irq\_handler\_t

#### Description

IRQ Handler。

#### Type definition

```c
typedef void (*pic_irq_handler_t)(void *userdata);
```

#### Parameter

| Parameter name | Description | Input or output |
| -------------- | ----------- | --------------- |
| userdata       | User data   | Input           |