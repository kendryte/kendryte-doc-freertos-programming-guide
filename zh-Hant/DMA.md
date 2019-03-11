# 直接存儲訪問 (DMA)

## 概述

直接存儲訪問 (Direct Memory Access, DMA) 用於在外部裝置與記憶體之間以及記憶體與記憶體之間提供高速資料傳輸。可以在無需任何 CPU 操作的情況下通過 DMA 快速移動資料，從而提高了CPU 的效率。

## 功能描述

DMA 模組具有以下功能：

- 自動選擇一路空閑的 DMA 通道用於傳輸
- 根據源地址和目標地址自動選擇軟體或硬體握手協議
- 支持 1、2、4、8 位元組的元素大小，源和目標大小不必一致
- 非同步或同步傳輸功能
- 循環傳輸功能，常用於刷新屏幕或音頻錄放等場景

## API 參考

對應的頭文件 `hal.h`

為用戶提供以下介面：

- [dma\_open\_free](#dmaopenfree)
- [dma\_close](#dmaclose)
- [dma\_set\_request\_source](#dmasetrequestsource)
- [dma\_transmit\_async](#dmatransmitasync)
- [dma\_transmit](#dmatransmit)
- [dma\_loop\_async](#dmaloopasync)

### dma\_open\_free

#### 描述

打開一個可用的 DMA 裝置。

#### 函數原型

```c
handle_t dma_open_free();
```

#### 返回值

DMA 裝置句柄。

### dma\_close

#### 描述

關閉 DMA 裝置。

#### 函數原型

```c
void dma_close(handle_t file);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| file        | DMA 裝置句柄    | 輸入      |

#### 返回值

無。

### dma\_set\_request\_source

#### 描述

設置 DMA 請求源。

#### 函數原型

```c
void dma_set_request_source(handle_t file, uint32_t request);
```

#### 參數

| 參數名稱  |   描述         |  輸入輸出  |
| -------- | -------------- | --------- |
| file     | DMA 裝置句柄    | 輸入      |
| request  | 請求源編號      | 輸入      |

#### 返回值

無。

### dma\_transmit\_async

#### 描述

進行 DMA 非同步傳輸。

#### 函數原型

```c
void dma_transmit_async(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, SemaphoreHandle_t completion_event);
```

#### 參數

| 參數名稱           |   描述         |  輸入輸出  |
| ----------------- | -------------- | --------- |
| file              | DMA 裝置句柄    | 輸入      |
| src               | 源地址          | 輸入      |
| dest              | 目標地址        | 輸出      |
| src\_inc          | 源地址是否自增   | 輸入      |
| dest\_inc         | 目標地址是否自增 | 輸入      |
| element\_size     | 元素大小（位元組） | 輸入      |
| count             | 元素數量        | 輸入      |
| burst\_size       | 突發傳輸數量    | 輸入      |
| completion\_event | 傳輸完成事件    | 輸入      |

#### 返回值

無。

### dma\_transmit

#### 描述

進行 DMA 同步傳輸。

#### 函數原型

```c
void dma_transmit(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size);
```

#### 參數

| 參數名稱          |   描述         |  輸入輸出  |
| ---------------- | -------------- | --------- |
| file             | DMA 裝置句柄    | 輸入      |
| src              | 源地址          | 輸入      |
| dest             | 目標地址        | 輸出      |
| src\_inc         | 源地址是否自增   | 輸入      |
| dest\_inc        | 目標地址是否自增 | 輸入      |
| element\_size    | 元素大小（位元組） | 輸入      |
| count            | 元素數量        | 輸入      |
| burst\_size      | 突發傳輸數量    | 輸入      |

#### 返回值

無。

### dma\_loop\_async

#### 描述

進行 DMA 非同步循環傳輸。

#### 函數原型

```c
void dma_loop_async(handle_t file, const volatile void **srcs, size_t src_num, volatile void **dests, size_t dest_num, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, dma_stage_completion_handler_t stage_completion_handler, void *stage_completion_handler_data, SemaphoreHandle_t completion_event, int *stop_signal);
```

#### 參數

| 參數名稱                         |   描述                 |  輸入輸出  |
| ------------------------------- | ---------------------- | --------- |
| file                            | DMA 裝置句柄            | 輸入      |
| srcs                            | 源地址列表              | 輸入      |
| src\_num                        | 源地址數量              | 輸入      |
| dests                           | 目標地址列表            | 輸出      |
| dest\_num                       | 目標地址數量            | 輸入      |
| src\_inc                        | 源地址是否自增          | 輸入      |
| dest\_inc                       | 目標地址是否自增        | 輸入      |
| element\_size                   | 元素大小（位元組）        | 輸入      |
| count                           | 元素數量                | 輸入      |
| burst\_size                     | 突發傳輸數量            | 輸入      |
| stage\_completion\_handler      | 階段完成處理程序        | 輸入      |
| stage\_completion\_handler_data | 階段完成處理程序用戶資料 | 輸入      |
| completion\_event               | 傳輸完成事件            | 輸入      |
| stop\_signal                    | 停止信號                | 輸入      |

**註：** 階段完成是指單次源到目標 count 個元素的傳輸完成。

#### 返回值

無。

### 舉例

```c
int src[256] = { [0 ... 255] = 1 };
int dest[256];
handle_t dma = dma_open_free();
dma_transmit(dma, src, dest, true, true, sizeof(int), 256, 4);
assert(dest[0] == src[0]);
dma_close(dma);
```

## 資料類型

相關資料類型、資料結構定義如下：

- [dma\_stage\_completion\_handler\_t](#dmastagecompletionhandlert)：DMA 階段完成處理程序。

### dma\_stage\_completion\_handler\_t

#### 描述

DMA 階段完成處理程序。

#### 定義

```c
typedef void (*dma_stage_completion_handler_t)(void *userdata);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| userdata   | 用戶資料        | 輸入      |