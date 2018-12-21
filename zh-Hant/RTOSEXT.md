# FreeRTOS 扩展

## 概述

FreeRTOS 是一个轻量级的实时操作系统。本 SDK 在其基础上新增了一些适用于 K210 的功能。

## 功能描述

FreeRTOS 扩展模块具有以下功能：

- 获取当前任务所在的逻辑处理器 Id
- 在指定逻辑处理器创建任务

K210 包含 2 个逻辑处理器，Id 分别为 0 和 1。

## API 参考

对应的头文件 `task.h`

为用户提供以下接口：

- [uxTaskGetProcessorId](#uxtaskgetprocessorid)
- [xTaskCreateAtProcessor](#xtaskcreateatprocessor)

### uxTaskGetProcessorId

#### 描述

获取当前逻辑处理器 Id。

#### 函数原型

```c
UBaseType_t uxTaskGetProcessorId(void);
```

#### 返回值

当前逻辑处理器 Id。

### xTaskCreateAtProcessor

#### 描述

在指定逻辑处理器创建任务。

#### 函数原型

```c
BaseType_t xTaskCreateAtProcessor(UBaseType_t uxProcessor, TaskFunction_t pxTaskCode, const char * const pcName, const configSTACK_DEPTH_TYPE usStackDepth, void * const pvParameters, UBaseType_t uxPriority, TaskHandle_t * const pxCreatedTask);
```

#### 参数

| 参数名称       |   描述       |  输入输出  |
| ------------- | ------------ | --------- |
| uxProcessor   | 逻辑处理器 Id | 输入      |
| pxTaskCode    | 任务入口点    | 输入      |
| pcName        | 任务名称      | 输入      |
| usStackDepth  | 栈空间        | 输入      |
| pvParameters  | 参数          | 输入      |
| uxPriority    | 优先级        | 输入      |
| pxCreatedTask | 创建的任务句柄 | 输入      |

#### 返回值

| 返回值  |  描述   |
| ------ | ------- |
| pdPASS | 成功 |
| 其他   | 失败 |