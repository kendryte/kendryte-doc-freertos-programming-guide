# 脈衝寬度調製器 (PWM)

## 概述

PWM 用於控制脈衝輸出的占空比。

## 功能描述

PWM 模組具有以下功能：

- 配置 PWM 輸出頻率
- 配置 PWM 每個腳位的輸出占空比

## API 參考

對應的頭文件 `devices.h`

為用戶提供以下介面：

- [pwm\_get\_pin\_count](#pwmgetpincount)
- [pwm\_set\_frequency](#pwmsetfrequency)
- [pwm\_set\_active\_duty\_cycle\_percentage](#pwmsetactivedutycyclepercentage)
- [pwm\_set\_enable](#pwmsetenable)

### pwm\_get\_pin\_count

#### 描述

獲取 PWM 腳位數量。

#### 函數原型

```c
uint32_t pwm_get_pin_count(handle_t file);
```

#### 參數

| 參數名稱     |   描述         |  輸入輸出  |
| ----------- | -------------- | --------- |
| file        | PWM 裝置句柄    | 輸入      |

#### 返回值

PWM 腳位數量。

### pwm\_set\_frequency

#### 描述

設置 PWM 頻率。

#### 函數原型

```c
double pwm_set_frequency(handle_t file, double frequency);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | PWM 裝置句柄    | 輸入      |
| frequency  | 期望的頻率（Hz） | 輸入      |

#### 返回值

設置後實際的頻率（Hz）。

### pwm\_set\_active\_duty\_cycle\_percentage

#### 描述

設置 PWM 腳位占空比。

#### 函數原型

```c
double pwm_set_active_duty_cycle_percentage(handle_t file, uint32_t pin, double duty_cycle_percentage);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | PWM 裝置句柄    | 輸入      |
| pin        | 腳位編號        | 輸入      |
| duty\_cycle\_percentage  | 期望的占空比 | 輸入      |

#### 返回值

設置後實際的占空比。

### pwm\_set\_enable

#### 描述

設置 PWM 腳位是否啟用。

#### 函數原型

```c
void pwm_set_enable(handle_t file, uint32_t pin, bool enable);
```

#### 參數

| 參數名稱    |   描述         |  輸入輸出  |
| ---------- | -------------- | --------- |
| file       | PWM 裝置句柄    | 輸入      |
| pin        | 腳位編號        | 輸入      |
| enable     | 是否啟用        | 輸入      |

#### 返回值

設置後實際的占空比。

### 舉例

```c
/* pwm0 pin0 輸出 200KHZ 占空比為 0.5 的方波 */
handle_t pwm = io_open("/dev/pwm0");
pwm_set_frequency(pwm, 200000);
pwm_set_active_duty_cycle_percentage(pwm, 0, 0.5);
pwm_set_enable(pwm, 0, true);
```