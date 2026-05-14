# Service Collaboration Kit

## 概述

Service Collaboration Kit（协同服务）提供了同账号下多端设备协同的能力。核心场景为跨设备互通——Tablet、PC/2in1 或 Phone 可调用远端设备的相机、扫描和图库功能，实现跨设备拍照、文档扫描、图片/视频选择等操作，拍摄结果自动回传至本端应用。

## 核心能力

### 跨设备互通（ArkTS）

基于分布式协同框架，提供两个核心 UI 组件：

- **createCollaborationServiceMenuItems**（设备列表组件）：展示附近可用远端设备，用户选择后发起跨端请求
- **CollaborationServiceStateDialog**（状态弹窗组件）：实时显示远端设备拍摄状态（拍摄中、导入中、协同失败等）

支持的能力类型：

| 能力 | 说明 |
|---|---|
| 跨端拍照 | 本端应用调用远端 Phone/Tablet 相机拍照，照片回传至本端 |
| 跨端文档扫描 | 本端应用调用远端设备扫描能力 |
| 跨端图库选择 | 本端应用调用远端设备图库（图片和视频）选择器 |
| 跨端视频选择 | API 6.0.0(20) 及之后版本支持视频选择器 |
| 跨端图片和视频选择 | API 6.0.0(20) 及之后版本支持图片和视频选择器 |

### 跨设备互通（NDK）

提供 C/C++ 接口，适用于 Native 层跨设备互通场景。

## 设备调用策略

| 版本 | 调用策略 |
|---|---|
| API 6.0.0(20) 之前 | PC/2in1 可调用 Tablet 和 Phone；Tablet 可调用 Phone |
| API 6.1.0(23) 及之后 | TV、Phone、Tablet、PC/2in1 可调用具备相应能力的远端 Phone、Tablet、PC/2in1 |

## npm 包名

`@kit.ServiceCollaborationKit`

## 关键 API

| API | 说明 |
|---|---|
| `createCollaborationServiceMenuItems` | 创建跨端设备列表菜单组件 |
| `CollaborationServiceStateDialog` | 远端设备状态弹窗组件 |
| 跨设备互通 NDK 接口 | C/C++ 层跨设备互通能力 |

## 权限要求

无额外权限要求，但需满足以下前提条件：

- 双端设备登录同一华为账号
- 双端设备打开 WLAN 和蓝牙开关
- 本端为 HarmonyOS NEXT 及以上版本的 Tablet 或 PC/2in1
- 远端为具备相机能力的 HarmonyOS NEXT 及以上版本的 Phone 或 Tablet

## 约束与限制

- 支持设备：Phone、Tablet、PC/2in1、TV
- 暂不支持模拟器
- API 6.1.0(23) 之前版本，仅 PC/2in1 和 Tablet 可正常调用跨设备互通接口

## 官方链接

- [Service Collaboration Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/servicecollaborationkit-introduction)
- [跨设备互通特性简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/servicecollaboration-service-overview)
- [跨设备互通开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/servicecollaboration-dev-guides)
- [跨设备互通 NDK 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/servicecollaboration-servicendk-guide)
