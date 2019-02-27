# 可编程中断控制器 (PIC)

## Overview

可以将任一外部中断源单独分配到每个 CPU 的外部中断上。这提供了强大的灵活性，能适应不同的应用需求。

## Features

PIC 模块具有以下功能: 

- 启用或禁用中断
- 设置中断处理程序
- 配置中断优先级

## API

Corresponding header file `hal.h`

Provide the following interfaces

- [pic\_set\_irq\_enable](#picsetirqenable)
- [pic\_set\_irq\_handler](#picsetirqhandler)
- [pic\_set\_irq\_priority](#picsetirqpriority)

### pic\_set\_irq\_enable

#### Description

设置 IRQ 是否启用。

#### Function prototype

```c
void pic_set_irq_enable(uint32_t irq, bool enable);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| irq         | IRQ 编号       | Input      |
| enable      | 是否启用        | Input      |

#### Return value

None.

### pic\_set\_irq\_handler

#### Description

设置 IRQ Handler。

#### Function prototype

```c
void pic_set_irq_handler(uint32_t irq, pic_irq_handler_t handler, void *userdata);
```

#### Parameter

| Parameter name     |   Description         |  Input or output  |
| ----------- | -------------- | --------- |
| irq         | IRQ 编号       | Input      |
| handler     | Handler        | Input      |
| userdata    | Handler user data | Input      |

#### Return value

None.

### pic\_set\_irq\_priority

#### Description

设置 IRQ 优先级。

#### Function prototype

```c
void pic_set_irq_priority(uint32_t irq, uint32_t priority);
```

#### Parameter

| Parameter name  |   Description         |  Input or output  |
| -------- | -------------- | --------- |
| irq      | IRQ 编号       | Input      |
| priority | 优先级         | Input      |

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

| Parameter name    |   Description         |  Input or output  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | Input      |