# 可编程中断控制器 (PIC)

## 概述

可以将任一外部中断源单独分配到每个 CPU 的外部中断上。这提供了强大的灵活性，能适应不同的应用需求。

## 功能描述

PIC 模块具有以下功能：

- 启用或禁用中断
- 设置中断处理程序
- 配置中断优先级

## API 参考

对应的头文件 `hal.h`

为用户提供以下接口：

- [pic\_set\_irq\_enable](#picsetirqenable)
- [pic\_set\_irq\_handler](#picsetirqhandler)
- [pic\_set\_irq\_priority](#picsetirqpriority)

### pic\_set\_irq\_enable

#### 描述

设置 IRQ 是否启用。

#### 函数原型

```c
void pic_set_irq_enable(uint32_t irq, bool enable);
```

#### 参数

| 参数名称     |   描述         |  输入输出  |
| ----------- | -------------- | --------- |
| irq         | IRQ 编号       | 输入      |
| enable      | 是否启用        | 输入      |

#### 返回值

无。

### pic\_set\_irq\_handler

#### 描述

设置 IRQ 处理程序。

#### 函数原型

```c
void pic_set_irq_handler(uint32_t irq, pic_irq_handler_t handler, void *userdata);
```

#### 参数

| 参数名称     |   描述         |  输入输出  |
| ----------- | -------------- | --------- |
| irq         | IRQ 编号       | 输入      |
| handler     | 处理程序        | 输入      |
| userdata    | 处理程序用户数据 | 输入      |

#### 返回值

无。

### pic\_set\_irq\_priority

#### 描述

设置 IRQ 优先级。

#### 函数原型

```c
void pic_set_irq_priority(uint32_t irq, uint32_t priority);
```

#### 参数

| 参数名称  |   描述         |  输入输出  |
| -------- | -------------- | --------- |
| irq      | IRQ 编号       | 输入      |
| priority | 优先级         | 输入      |

#### 返回值

无。

## 数据类型

相关数据类型、数据结构定义如下：

- [pic\_irq\_handler\_t](#picirqhandlert)：IRQ 处理程序。

### pic\_irq\_handler\_t

#### 描述

IRQ 处理程序。

#### 定义

```c
typedef void (*pic_irq_handler_t)(void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |