# Driver Development Kit

## 概述

Driver Development Kit（驱动开发服务）为外设驱动开发者提供高效、安全、丰富的扩展外设驱动开发解决方案 ArkTS-API 和 C-API，支持外设驱动开发者为消费者带来外设即插即用的极致体验。

## 核心能力

### 使用场景

1. **专业专用办公外设驱动开发**：银行柜台、企业办公、医疗检测等领域，如高拍仪、身份证扫描仪、指纹识别仪、血氧血糖监测设备
2. **非标外设扩展增强能力开放**：厂商私有非标 HID 外设增强能力开放，如手写板快捷键定制、压感/绘图区域设置、鼠标灯光效果设置、DPI 及 X/Y 轴等高阶能力设置

### 亮点特征

- 支持开发者开发外设配件的高阶功能
- 扩展驱动框架支持扩展外设驱动生命周期管理
- 面向扩展设备应用提供扩展外设查询绑定能力接口

### 基本概念

- **扩展外设驱动客户端**：查询驱动并绑定驱动，自定义驱动与设备之间的通信方式及数据处理方式（带 UI 界面基础驱动）
- **扩展外设驱动**：基于 DDK 能力开发的专业专用扩展外设驱动或扩展外设增强驱动（无 UI 界面基础驱动）
- **扩展外设管理服务**：扩展设备管理，驱动包全生命周期管理
- **非标外设**：采用非标准协议通信（厂商自定义协议）的外设

### 驱动应用规格

- 驱动应用基于 DriverExtensionAbility 开发
- 安装时安装到所有用户环境，卸载时所有用户环境同时卸载
- DriverExtensionAbility 中仅支持访问 DDK API，不支持访问其他 ArkTS API（安全管控）

## npm 包名

`@kit.DriverDevelopmentKit`

## 关键 API

| API | 说明 |
|---|---|
| `@ohos.driver.deviceManager` | 扩展外设管理（ArkTS） |
| USB DDK (C/C++) | USB 设备驱动开发 |
| HID DDK (C/C++) | HID 设备驱动开发 |
| USB Serial DDK (C/C++) | USB 串口驱动开发 |
| SCSI Peripheral DDK (C/C++) | SCSI 外设驱动开发 |
| `DriverExtensionAbility` | 驱动扩展能力生命周期管理 |

## 权限要求

| API 类型 | DDK 类型 | 权限名称 |
|---|---|---|
| ArkTS-API | 不涉及 | `ohos.permission.ACCESS_EXTENSIONAL_DEVICE_DRIVER` |
| C-API | UsbDdk | `ohos.permission.ACCESS_DDK_USB` |
| C-API | HidDdk | `ohos.permission.ACCESS_DDK_HID` |
| C-API | USBSerialDDK | `ohos.permission.ACCESS_DDK_USB_SERIAL` |
| C-API | ScsiPeripheralDDK | `ohos.permission.ACCESS_DDK_SCSI_PERIPHERAL` |

## 约束与限制

- 不支持模拟器
- DriverExtensionAbility 中受限访问 ArkTS API，仅支持 DDK API

## 关联模块

| 名称 | 作用 |
|---|---|
| PerformanceAnalysisKit | 引入 hilog 用于日志打印 |
| BasicServicesKit | 引入 BusinessError 用于捕获错误信息 |
| IPCKit | 引入 rpc 用于驱动与客户端 IPC 通信 |
| AbilityKit | 引入 Want 用于生命周期管理 |

## 官方链接

- [Driver Development Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/driverdevelopment-overview)
- [环境准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/environmental-preparation)
- [开发无 UI 界面基础驱动](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/driverextensionability)
- [开发带 UI 界面基础驱动](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/externaldevice-guidelines)
