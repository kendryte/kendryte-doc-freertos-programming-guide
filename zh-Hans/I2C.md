# 集成电路内置总线 (I²C)

## 概述

I²C 总线用于和多个外部设备进行通信。多个外部设备可以共用一个 I²C 总线。

## 功能描述

I²C 模块具有以下功能：

- 独立的 I²C 设备封装外设相关参数
- 自动处理多设备总线争用
- 支持从模式

## API 参考

对应的头文件 `devices.h`

为用户提供以下接口：

- [i2c\_get\_device](#i2cgetdevice)
- [i2c\_dev\_set\_clock\_rate](#i2cdevsetclockrate)
- [i2c\_dev\_transfer\_sequential](#i2cdevtransfersequential)
- [i2c\_config\_as\_slave](#i2cconfigasslave)
- [i2c\_slave\_set\_clock\_rate](#i2cslavesetclockrate)

### i2c\_get\_device

#### 描述

注册并打开一个 I²C 设备。

#### 函数原型

```c
handle_t i2c_get_device(handle_t file, const char *name, uint32_t slave_address, uint32_t address_width);
```

#### 参数

| 参数名称          |   描述             |  输入输出  |
| ---------------- | ------------------ | --------- |
| file             | I²C 控制器句柄      | 输入      |
| name             | 指定访问该设备的路径 | 输入      |
| slave\_address   | 从设备地址          | 输入      |
| address\_width   | 从设备地址宽度      | 输入      |

#### 返回值

I²C 设备句柄。

### i2c\_dev\_set\_clock\_rate

#### 描述

配置 I²C 设备的时钟速率。

#### 函数原型

```c
double i2c_dev_set_clock_rate(handle_t file, double clock_rate);
```

#### 参数

| 参数名称          |   描述        |  输入输出  |
| ---------------- | ------------- | --------- |
| file             | I²C 设备句柄   | 输入       |
| clock\_rate      | 期望的时钟速率 | 输入       |

#### 返回值

设置后的实际速率。

### i2c\_dev\_transfer\_sequential

#### 描述

对 I²C 设备先读后写。

#### 函数原型

```c
int i2c_dev_transfer_sequential(handle_t file, const uint8_t *write_buffer, size_t write_len, uint8_t *read_buffer, size_t read_len);
```

#### 参数

| 参数名称       |   描述         |  输入输出  |
| ------------- | -------------- | --------- |
| file          | I²C 设备句柄    | 输入      |
| write\_buffer | 源缓冲区        | 输入      |
| write\_len    | 要写入的字节数   | 输入      |
| read\_buffer  | 目标缓冲区      | 输出      |
| read\_len     | 最多读取的字节数 | 输入      |

#### 返回值

实际读取的字节数。

### i2c\_config\_as\_slave

#### 描述

配置 I²C 控制器为从模式。

#### 函数原型

```c
void i2c_config_as_slave(handle_t file, uint32_t slave_address, uint32_t address_width, i2c_slave_handler_t *handler);
```

#### 参数

| 参数名称          |   描述        |  输入输出  |
| ---------------- | ------------- | --------- |
| file             | I²C 控制器句柄 | 输入       |
| slave\_address   | 从设备地址     | 输入       |
| address\_width   | 从设备地址宽度 | 输入       |
| handler          | 从设备处理程序 | 输入       |

#### 返回值

无。

### spi\_dev\_set\_clock\_rate

#### 描述

配置 I²C 从模式的时钟速率。

#### 函数原型

```c
double i2c_slave_set_clock_rate(handle_t file, double clock_rate);
```

#### 参数

| 参数名称          |   描述        |  输入输出  |
| ---------------- | ------------- | --------- |
| file             | I²C 控制器句柄 | 输入       |
| clock\_rate      | 期望的时钟速率 | 输入       |

#### 返回值

设置后的实际速率。

### 举例

```c
handle_t i2c = io_open("/dev/i2c0");
/* i2c外设地址是0x32, 7位地址，速率200K */
handle_t dev0 = i2c_get_device(i2c, "/dev/i2c0/dev0", 0x32, 7);
i2c_dev_set_clock_rate(dev0, 200000);

uint8_t reg = 0;
uint8_t data_buf[2] = { 0x00,0x01 };
data_buf[0] = reg;
/* 向0寄存器写0x01 */
io_write(dev0, data_buf, 2);
/* 从0寄存器读取1字节数据 */
i2c_dev_transfer_sequential(dev0, &reg, 1, data_buf, 1);
```

## 数据类型

相关数据类型、数据结构定义如下：

- [i2c\_event\_t](#i2ceventt)：I²C 事件。
- [i2c\_slave\_handler\_t](#i2cslavehandlert)：I²C 从设备处理程序。

### i2c\_event\_t

#### 描述

I²C 事件。

#### 定义

```c
typedef enum _i2c_event
{
    I2C_EV_START,
    I2C_EV_RESTART,
    I2C_EV_STOP
} i2c_event_t;
```

#### 成员

| 成员名称            | 描述             |
| ------------------ | ---------------- |
| I2C\_EV\_START     | 收到 Start 信号   |
| I2C\_EV\_RESTART   | 收到 Restart 信号 |
| I2C\_EV\_STOP      | 收到 Stop 信号    |

### i2c\_slave\_handler\_t

#### 描述

I²C 从设备处理程序。

#### 定义

```c
typedef struct _i2c_slave_handler
{
    void (*on_receive)(uint32_t data);
    uint32_t (*on_transmit)();
    void (*on_event)(i2c_event_t event);
} i2c_slave_handler_t;
```

#### 成员

| 成员名称          | 描述               |
| ---------------- | ------------------ |
| on\_receive      | 收到数据时被调用     |
| on\_transmit     | 需要发送数据时被调用 |
| on\_event        | 发生事件时被调用     |