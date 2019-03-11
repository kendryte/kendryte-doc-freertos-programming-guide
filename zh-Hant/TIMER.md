# 定時器 (TIMER)

## 概述

TIMER 提供高精度定時功能。

## 功能描述

TIMER 模組具有以下功能：

- 啟用或禁用定時器
- 配置定時器觸發間隔
- 配置定時器觸發處理程序

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [timer\_set\_interval](#timersetinterval)
- [timer\_set\_on\_tick](#timersetontick)
- [timer\_set\_enable](#timersetenable)

### timer\_set\_interval

#### 描述

設置 TIMER 觸發間隔。

#### 函數原型

```c
size_t timer_set_interval(handle_t file, size_t nanoseconds);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| file        | TIMER 裝置句柄  | 輸入      |
| nanoseconds | 間隔（納秒）    | 輸入       |

#### 返回值

實際的觸發間隔（納秒）。

### timer\_set\_on\_tick

#### 描述

設置 TIMER 觸發時的處理程序。

#### 函數原型

```c
void timer_set_on_tick(handle_t file, timer_on_tick_t on_tick, void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | TIMER 裝置句柄  | 輸入      |
| on_tick    | 處理程序        | 輸入      |
| userdata   | 處理程序用戶資料 | 輸入      |

#### 返回值

無。

### timer\_set\_enable

#### 描述

設置 TIMER 是否啟用。

#### 函數原型

```c
void timer_set_enable(handle_t file, bool enable);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | TIMER 裝置句柄 | 輸入      |
| enable     | 是否啟用        | 輸入      |

#### 返回值

無。

### 舉例

```c
/* 定時器0  定時 1 秒列印 Time OK! */
void on_tick(void *unused)
{
    printf("Time OK!\n");
}

handle_t timer = io_open("/dev/timer0");

timer_set_interval(timer, 1e9);
timer_set_on_tick(timer, on_tick, NULL);
timer_set_enable(timer, true);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [timer\_on\_tick\_t](#timerontickt)：TIMER 觸發時的處理程序。

### timer\_on\_tick\_t

#### 描述

TIMER 觸發時的處理程序。

#### 定義

```c
typedef void (*timer_on_tick_t)(void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| userdata   | 用戶資料        | 輸入      |