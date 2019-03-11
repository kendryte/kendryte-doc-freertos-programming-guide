# 可編程中斷控制器 (PIC)

## 概述

可以將任一外部中斷源單獨分配到每個 CPU 的外部中斷上。這提供了強大的靈活性，能適應不同的應用需求。

## 功能描述

PIC 模組具有以下功能：

- 啟用或禁用中斷
- 設置中斷處理程序
- 配置中斷優先順序

## API 參考

對應的頭文件 `hal.h`

為用戶提供以下介面：

- [pic\_set\_irq\_enable](#picsetirqenable)
- [pic\_set\_irq\_handler](#picsetirqhandler)
- [pic\_set\_irq\_priority](#picsetirqpriority)

### pic\_set\_irq\_enable

#### 描述

設置 IRQ 是否啟用。

#### 函數原型

```c
void pic_set_irq_enable(uint32_t irq, bool enable);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| irq         | IRQ 編號       | 輸入      |
| enable      | 是否啟用        | 輸入      |

#### 返回值

無。

### pic\_set\_irq\_handler

#### 描述

設置 IRQ 處理程序。

#### 函數原型

```c
void pic_set_irq_handler(uint32_t irq, pic_irq_handler_t handler, void *userdata);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| irq         | IRQ 編號       | 輸入      |
| handler     | 處理程序        | 輸入      |
| userdata    | 處理程序用戶資料 | 輸入      |

#### 返回值

無。

### pic\_set\_irq\_priority

#### 描述

設置 IRQ 優先順序。

#### 函數原型

```c
void pic_set_irq_priority(uint32_t irq, uint32_t priority);
```

#### 參數

| 參數名稱  |   描述         |  輸入輸出  |
| -------- | -------------- | --------- |
| irq      | IRQ 編號       | 輸入      |
| priority | 優先順序         | 輸入      |

#### 返回值

無。

## 資料類型

相關資料類型、資料結構定義如下：

- [pic\_irq\_handler\_t](#picirqhandlert)：IRQ 處理程序。

### pic\_irq\_handler\_t

#### 描述

IRQ 處理程序。

#### 定義

```c
typedef void (*pic_irq_handler_t)(void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| userdata   | 用戶資料        | 輸入      |