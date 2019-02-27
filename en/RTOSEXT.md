# FreeRTOS Extension

## Overview

FreeRTOS is a lightweight real-time operating system. This SDK adds some features for the K210.

## Features

The FreeRTOS extension has the following features:

- Get the logical processor Id where the current task is located
- Create tasks on the specified logical processor

The K210 contains 2 logical processors with IDs of 0 and 1 respectively.

## API

Corresponding header file `task.h`

Provide the following interfaces

- [uxTaskGetProcessorId](#uxtaskgetprocessorid)
- [xTaskCreateAtProcessor](#xtaskcreateatprocessor)

### uxTaskGetProcessorId

#### Description

Get the current logical processor ID.

#### Function prototype

```c
UBaseType_t uxTaskGetProcessorId(void);
```

#### Return value

Current logical processor ID.

### xTaskCreateAtProcessor

#### Description

Create a task at the specified logical processor.

#### Function prototype

```c
BaseType_t xTaskCreateAtProcessor(UBaseType_t uxProcessor, TaskFunction_t pxTaskCode, const char * const pcName, const configSTACK_DEPTH_TYPE usStackDepth, void * const pvParameters, UBaseType_t uxPriority, TaskHandle_t * const pxCreatedTask);
```

#### Parameter

| Parameter name |     Description      | Input or output |
| -------------- | -------------------- | --------------- |
| uxProcessor    | Logical processor ID | Input           |
| pxTaskCode     | Task entry point     | Input           |
| pcName         | Task name            | Input           |
| usStackDepth   | Stack depth          | Input           |
| pvParameters   | Parameters           | Input           |
| uxPriority     | Priority             | Input           |
| pxCreatedTask  | Created task handle  | Input           |

#### Return value

| Return value | Description |
| ------ | ----------- |
| pdPASS | Success     |
| Others | Fail        |