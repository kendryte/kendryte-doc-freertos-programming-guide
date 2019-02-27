# FreeRTOS 扩展

## Overview

FreeRTOS 是一个轻量级的实时操作系统。本 SDK 在其基础上新增了一些适用于 K210 的功能。

## Features

FreeRTOS 扩展模块具有以下功能：

- 获取当前任务所在的逻辑处理器 Id
- 在指定逻辑处理器创建任务

K210 包含 2 个逻辑处理器，Id 分别为 0 和 1。

## API

Corresponding header file `task.h`

Provide the following interfaces

- [uxTaskGetProcessorId](#uxtaskgetprocessorid)
- [xTaskCreateAtProcessor](#xtaskcreateatprocessor)

### uxTaskGetProcessorId

#### Description

获取当前逻辑处理器 Id。

#### Function prototype

```c
UBaseType_t uxTaskGetProcessorId(void);
```

#### Return value

当前逻辑处理器 Id。

### xTaskCreateAtProcessor

#### Description

在指定逻辑处理器创建任务。

#### Function prototype

```c
BaseType_t xTaskCreateAtProcessor(UBaseType_t uxProcessor, TaskFunction_t pxTaskCode, const char * const pcName, const configSTACK_DEPTH_TYPE usStackDepth, void * const pvParameters, UBaseType_t uxPriority, TaskHandle_t * const pxCreatedTask);
```

#### Parameter

| Parameter name       |   Description       |  Input or output  |
| ------------- | ------------ | --------- |
| uxProcessor   | 逻辑处理器 Id | Input      |
| pxTaskCode    | 任务入口点    | Input      |
| pcName        | 任务名称      | Input      |
| usStackDepth  | 栈空间        | Input      |
| pvParameters  | 参数          | Input      |
| uxPriority    | 优先级        | Input      |
| pxCreatedTask | 创建的任务句柄 | Input      |

#### Return value

| 返回值  |  Description   |
| ------ | ------- |
| pdPASS | 成功 |
| 其他   | 失败 |