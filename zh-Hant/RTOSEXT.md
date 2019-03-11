# FreeRTOS 擴展

## 概述

FreeRTOS 是一個輕量級的實時操作系統。本 SDK 在其基礎上新增了一些適用於 K210 的功能。

## 功能描述

FreeRTOS 擴展模組具有以下功能：

- 獲取當前任務所在的邏輯處理器 Id
- 在指定邏輯處理器創建任務

K210 包含 2 個邏輯處理器，Id 分別為 0 和 1。

## API 參考

對應的頭文件 `task.h`

為用戶提供以下介面：

- [uxTaskGetProcessorId](#uxtaskgetprocessorid)
- [xTaskCreateAtProcessor](#xtaskcreateatprocessor)

### uxTaskGetProcessorId

#### 描述

獲取當前邏輯處理器 Id。

#### 函數原型

```c
UBaseType_t uxTaskGetProcessorId(void);
```

#### 返回值

當前邏輯處理器 Id。

### xTaskCreateAtProcessor

#### 描述

在指定邏輯處理器創建任務。

#### 函數原型

```c
BaseType_t xTaskCreateAtProcessor(UBaseType_t uxProcessor, TaskFunction_t pxTaskCode, const char * const pcName, const configSTACK_DEPTH_TYPE usStackDepth, void * const pvParameters, UBaseType_t uxPriority, TaskHandle_t * const pxCreatedTask);
```

#### 參數

| 參數名稱       |   描述       |  輸入輸出  |
| ------------- | ------------ | --------- |
| uxProcessor   | 邏輯處理器 Id | 輸入      |
| pxTaskCode    | 任務入口點    | 輸入      |
| pcName        | 任務名稱      | 輸入      |
| usStackDepth  | 棧空間        | 輸入      |
| pvParameters  | 參數          | 輸入      |
| uxPriority    | 優先順序        | 輸入      |
| pxCreatedTask | 創建的任務句柄 | 輸入      |

#### 返回值

| 返回值  |  描述   |
| ------ | ------- |
| pdPASS | 成功 |
| 其他   | 失敗 |