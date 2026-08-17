# AR Engine（AREngine）

## 概述

AR Engine（AR 引擎服务）是用于在 HarmonyOS 上构建增强现实应用的引擎，提供运动跟踪、环境跟踪等空间计算能力，实现虚拟世界与现实世界的融合。主要能力覆盖：运动跟踪与平面识别、平面语义及物体语义、环境 Mesh 识别、深度估计、图像跟踪、高精几何重建、人脸识别与跟踪（FaceAR）、人体骨骼点识别与跟踪（BodyAR）。

- npm 包名：`@kit.AREngine`（官方实际包名，导入 `arEngine`、`ARView`、`arViewController`）
- 配套依赖：通常联合 `@kit.ArkGraphics3D`（渲染）、`@kit.BasicServicesKit`（BusinessError）
- 模拟器：不支持

```
import { arEngine, ARView, arViewController } from '@kit.AREngine';
import { Scene, Node, ... } from '@kit.ArkGraphics3D';
```

## 核心能力

### ARView / arViewController 基础会话管理

- `ARView`：AR 渲染组件，接收 `ARViewContext` 用于显示相机预览流与 3D 场景。
- `arViewController.ARViewContext`：AR 会话上下文，管理 AR Engine 系统状态，生命周期：`init()` → `pause()` / `resume()` → `destroy()`。
- `arViewController.ARViewCallback`：会话回调，含 `onFrameUpdate`（帧更新）、`onAnchorAdd` / `onAnchorUpdate`（锚点变化）。
- 会话配置（`ARViewContext.config`）：`type`（ARType）、`planeFindingMode`、`powerMode`、`focusMode`、`cameraLensFacing`、`multiFaceMode` 等。
- 特性检查：`arViewController.isARTypeSupported(arEngine.ARFeatureType.XXX)` 查询设备是否支持指定 AR 特性。

### FaceAR：人脸识别与跟踪（API 23 新增）

- 人脸识别与实时跟踪，支持多人脸（`ARMultiFaceMode.MULTIFACE_ENABLE`），前置相机（`ARCameraLensFacing.FRONT`）。
- 几何数据：`ARFace.getGeometry()` 返回 `ARGeometry`，提供 84 个人脸拓扑点（`getVertices()` / `getIndices()`）。
- 微表情捕捉：`ARFace.getBlendShapes()` 返回 `ARBlendShapes`，提供 64 种表情参数（覆盖眼、眉、眼球、嘴、舌等主要脸部器官），支持 `getData()` / `getTypes()` / `count`。

### BodyAR：人体骨骼关键点识别（API 23 新增）

- 人体骨骼点识别与实时跟踪，获取环境中人体骨骼关键点信息，用于虚拟形象驱动、运动检测等场景。

### 3D 空间重建会话管理

- 实时 3D 环境重建与 3DGS 场景建模。
- 提供重建任务控制、进度查询、模型导出能力。
- 高精几何重建包含稠密点云绘制、体积测量、空间识别三大能力。

### 营销组件

- AR 营销互动能力，支持营销场景的 AR 展示与交互。

### 外部相机传感器支持

- 支持接入外部相机传感器数据，扩展 AR 能力在更多硬件形态上的适用范围。

### 3D 高斯模型加载

- 支持 3DGS（3D Gaussian Splatting）模型加载，可与 Spatial Recon Kit 的 3DGS 渲染运算能力配合。

### C/C++ 接口

- C API 以 `HMS_AREngine_` 为前缀，头文件 `ar_engine_core.h`，链接 `libarengine_native.so`。
- 特性查询使用 `HMS_AREngine_CheckSupported`（对应 ArkTS 的 `isARTypeSupported`）。
- 人脸跟踪、人体跟踪、运动跟踪、平面识别等能力均提供 C/C++ 版本（文档页 arengine-c-face / arengine-c-body 等）。

## 关键 API

| API | 说明 |
|---|---|
| `arViewController.ARViewContext` | AR 会话上下文：init / pause / resume / destroy，管理会话状态 |
| `arViewController.ARViewCallback` | 会话回调：onFrameUpdate / onAnchorAdd / onAnchorUpdate |
| `arViewController.isARTypeSupported` | 查询设备是否支持指定 AR 特性 |
| `ARView` | AR 渲染组件，显示预览流与 3D 场景 |
| `arEngine.ARSession` | AR 会话：getFrame 获取当前帧、getAllTrackables 获取跟踪对象 |
| `arEngine.ARFace` | 人脸对象：getGeometry 人脸几何、getBlendShapes 微表情、getPose 位姿 |
| `arEngine.ARGeometry` | 人脸几何数据：getVertices 拓扑点、getIndices 索引 |
| `arEngine.ARBlendShapes` | 微表情数据：getData 表情系数、getTypes 表情类型 |
| `arEngine.ARType` | 会话类型：FACE / BODY 等 |
| `arEngine.ARFeatureType` | 特性类型：ARENGINE_FEATURE_TYPE_FACE 等 |
| `arEngine.ARCameraLensFacing` | 相机朝向：FRONT / BACK |
| `arEngine.ARMultiFaceMode` | 多人脸模式：MULTIFACE_ENABLE 等 |
| `arEngine.ARTrackable` / `ARTrackingState` | 跟踪对象与跟踪状态（TRACKING 等） |

## 权限与约束

| 项目 | 要求 |
|---|---|
| 系统能力 | 调用前需 `canIUse("SystemCapability.AREngine.Core")` 检查设备支持 |
| 设备类型 | Phone、Tablet；6.1.0(23) 起新增支持 TV；不同设备支持的特性范围有差异 |
| 特性查询 | ArkTS：`arViewController.isARTypeSupported`；C API：`HMS_AREngine_CheckSupported` |
| 地域限制 | 仅支持中国境内（香港、澳门特别行政区及中国台湾除外）接入使用 |
| 模拟器 | 不支持 |
| 免责说明 | 人脸跟踪等能力不构成产品质量保证，接入前阅读官方技术局限性及免责声明 |

坐标系说明：AR Engine 提供重力对齐世界坐标系、重力对齐北向坐标系（固定坐标系，不受设备位姿影响）、AGP 世界坐标系三种，均以相机启动时相机中心为原点。

## API 23 / 24 变更说明

| 版本 | 变更 |
|---|---|
| API 23（6.1.0） | 新增 FaceAR（人脸识别与跟踪、几何数据、微表情）、BodyAR（人体骨骼关键点识别）；新增 3D 空间重建会话管理、营销组件、外部相机传感器支持、3D 高斯模型加载；新增 TV 设备支持；多 Kit 扩展对 PC/2in1、TV 设备支持 |
| API 24（6.1.1） | 官方文档暂未列出 AR Engine 重大变更，能力与 API 23 保持一致 |

## 官方链接

- [AR Engine 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-overview)
- [AR Engine Kit 指南目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ar-engine-kit-guide)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-preparations)
- [管理 AR 会话](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arsession)
- [人脸跟踪（ArkTS）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-face)
- [人体骨骼点识别与跟踪介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-body-conversion)
- [ArkTS API 参考（arEngine）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-api-arengine)
- [C API 参考（AR Engine）](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arengine-capi-arengine)
