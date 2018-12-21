# 直接存储访问 (DMA)

## 概述

直接存储访问 (Direct Memory Access, DMA) 用于在外设与存储器之间以及存储器与存储器之间提供高速数据传输。可以在无需任何 CPU 操作的情况下通过 DMA 快速移动数据，从而提高了CPU 的效率。

## 功能描述

DMA 模块具有以下功能：

- 自动选择一路空闲的 DMA 通道用于传输
- 根据源地址和目标地址自动选择软件或硬件握手协议
- 支持 1、2、4、8 字节的元素大小，源和目标大小不必一致
- 异步或同步传输功能
- 循环传输功能，常用于刷新屏幕或音频录放等场景

## API 参考

对应的头文件 `hal.h`

为用户提供以下接口：

- [dma\_open\_free](#dmaopenfree)
- [dma\_close](#dmaclose)
- [dma\_set\_request\_source](#dmasetrequestsource)
- [dma\_transmit\_async](#dmatransmitasync)
- [dma\_transmit](#dmatransmit)
- [dma\_loop\_async](#dmaloopasync)

### dma\_open\_free

#### 描述

打开一个可用的 DMA 设备。

#### 函数原型

```c
handle_t dma_open_free();
```

#### 返回值

DMA 设备句柄。

### dma\_close

#### 描述

关闭 DMA 设备。

#### 函数原型

```c
void dma_close(handle_t file);
```

#### 参数

| 参数名称     |   描述         |  输入输出  |
| ----------- | -------------- | --------- |
| file        | DMA 设备句柄    | 输入      |

#### 返回值

无。

### dma\_set\_request\_source

#### 描述

设置 DMA 请求源。

#### 函数原型

```c
void dma_set_request_source(handle_t file, uint32_t request);
```

#### 参数

| 参数名称  |   描述         |  输入输出  |
| -------- | -------------- | --------- |
| file     | DMA 设备句柄    | 输入      |
| request  | 请求源编号      | 输入      |

#### 返回值

无。

### dma\_transmit\_async

#### 描述

进行 DMA 异步传输。

#### 函数原型

```c
void dma_transmit_async(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, SemaphoreHandle_t completion_event);
```

#### 参数

| 参数名称           |   描述         |  输入输出  |
| ----------------- | -------------- | --------- |
| file              | DMA 设备句柄    | 输入      |
| src               | 源地址          | 输入      |
| dest              | 目标地址        | 输出      |
| src\_inc          | 源地址是否自增   | 输入      |
| dest\_inc         | 目标地址是否自增 | 输入      |
| element\_size     | 元素大小（字节） | 输入      |
| count             | 元素数量        | 输入      |
| burst\_size       | 突发传输数量    | 输入      |
| completion\_event | 传输完成事件    | 输入      |

#### 返回值

无。

### dma\_transmit

#### 描述

进行 DMA 同步传输。

#### 函数原型

```c
void dma_transmit(handle_t file, const volatile void *src, volatile void *dest, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size);
```

#### 参数

| 参数名称          |   描述         |  输入输出  |
| ---------------- | -------------- | --------- |
| file             | DMA 设备句柄    | 输入      |
| src              | 源地址          | 输入      |
| dest             | 目标地址        | 输出      |
| src\_inc         | 源地址是否自增   | 输入      |
| dest\_inc        | 目标地址是否自增 | 输入      |
| element\_size    | 元素大小（字节） | 输入      |
| count            | 元素数量        | 输入      |
| burst\_size      | 突发传输数量    | 输入      |

#### 返回值

无。

### dma\_loop\_async

#### 描述

进行 DMA 异步循环传输。

#### 函数原型

```c
void dma_loop_async(handle_t file, const volatile void **srcs, size_t src_num, volatile void **dests, size_t dest_num, int src_inc, int dest_inc, size_t element_size, size_t count, size_t burst_size, dma_stage_completion_handler_t stage_completion_handler, void *stage_completion_handler_data, SemaphoreHandle_t completion_event, int *stop_signal);
```

#### 参数

| 参数名称                         |   描述                 |  输入输出  |
| ------------------------------- | ---------------------- | --------- |
| file                            | DMA 设备句柄            | 输入      |
| srcs                            | 源地址列表              | 输入      |
| src\_num                        | 源地址数量              | 输入      |
| dests                           | 目标地址列表            | 输出      |
| dest\_num                       | 目标地址数量            | 输入      |
| src\_inc                        | 源地址是否自增          | 输入      |
| dest\_inc                       | 目标地址是否自增        | 输入      |
| element\_size                   | 元素大小（字节）        | 输入      |
| count                           | 元素数量                | 输入      |
| burst\_size                     | 突发传输数量            | 输入      |
| stage\_completion\_handler      | 阶段完成处理程序        | 输入      |
| stage\_completion\_handler_data | 阶段完成处理程序用户数据 | 输入      |
| completion\_event               | 传输完成事件            | 输入      |
| stop\_signal                    | 停止信号                | 输入      |

**注：** 阶段完成是指单次源到目标 count 个元素的传输完成。

#### 返回值

无。

### 举例

```c
int src[256] = { [0 ... 255] = 1 };
int dest[256];
handle_t dma = dma_open_free();
dma_transmit(dma, src, dest, true, true, sizeof(int), 256, 4);
assert(dest[0] == src[0]);
dma_close(dma);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [dma\_stage\_completion\_handler\_t](#dmastagecompletionhandlert)：DMA 阶段完成处理程序。

### dma\_stage\_completion\_handler\_t

#### 描述

DMA 阶段完成处理程序。

#### 定义

```c
typedef void (*dma_stage_completion_handler_t)(void *userdata);
```

#### 参数

| 参数名称    |   描述         |  输入输出  |
| ---------- | -------------- | --------- |
| userdata   | 用户数据        | 输入      |