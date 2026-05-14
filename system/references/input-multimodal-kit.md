# Input Kit + Multimodal Awareness Kit

本文件汇总多模输入服务与多模态融合感知服务。

---

## 一、Input Kit（多模输入服务）

### 概述

Input Kit 为多种输入设备提供服务，如触控板、触摸屏、鼠标、键盘等。通过对这些输入设备上报驱动事件的归一化处理，确保不同输入设备与用户交互体验统一和流畅。除基础输入事件服务外，还提供获取输入设备列表、改变鼠标光标样式等功能和接口。

### 核心能力

- 多输入设备驱动事件归一化处理
- 输入事件管理、接收、预处理、分发
- 获取输入设备列表
- 改变鼠标光标样式
- 触摸事件、按键事件、鼠标事件分发

### npm 包名

`@kit.InputKit`

### 关键 API

| API | 说明 |
|---|---|
| `@ohos.multimodalInput.inputDevice` | 输入设备管理 |
| `@ohos.multimodalInput.inputEventClient` | 输入事件注入 |
| `@ohos.multimodalInput.inputMonitor` | 输入事件监听 |
| `@ohos.multimodalInput.pointer` | 鼠标光标样式管理 |
| `@ohos.multimodalInput.keyEvent` | 按键事件 |
| `@ohos.multimodalInput.touchEvent` | 触摸事件 |
| `@ohos.multimodalInput.mouseEvent` | 鼠标事件 |

### 权限要求

具体权限请参考各开发指导文档。

### 官方链接

- [Input Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/input-overview)
- [输入设备开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputdevice-guidelines)

---

## 二、Multimodal Awareness Kit（多模态融合感知服务）

### 概述

多模态融合感知利用设备上的多种传感器数据（如加速度计和陀螺仪等），来识别活动、状态和姿态等信息，例如判断设备是否处于静止状态。

### 核心能力

- 基于多传感器数据融合的设备状态识别
- 活动识别（静止、步行、跑步等）
- 设备姿态感知
- 实时设备状态结果上报

### npm 包名

`@kit.MultimodalAwarenessKit`

### 关键 API

| API | 说明 |
|---|---|
| Stationary API | 设备静止状态识别与订阅 |

### 权限要求

使用多模态融合感知需要申请相关权限，设备需支持对应能力所需的传感器。

### 约束与限制

- 需要用户进行相关权限申请
- 设备需支持对应传感器
- 应用需在业务场景主动发起订阅，业务结束时主动取消订阅

### 官方链接

- [Multimodal Awareness Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/multimodalawareness-kit-intro)
- [Stationary 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/stationary-guidelines)
