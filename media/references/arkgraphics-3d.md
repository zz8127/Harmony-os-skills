# 图形3D Kit 合集

## ArkGraphics 3D — 方舟3D图形

### 概述

ArkGraphics 3D 基于轻量级 3D 引擎及渲染管线为开发者提供基础 3D 场景绘制能力，支持自定义场景模式和自动场景模式。自定义场景模式为核心能力，支持自行构建和管理 Scene、Camera、Light 等节点；自动场景模式可直接加载 glTF 模型，由框架自动创建基础相机、光源及交互控制。

- npm 包名：`@kit.ArkGraphics3D`
- 模拟器：未明确说明

### 核心能力

| 能力 | 说明 |
|---|---|
| glTF 模型加载 | 加载并解析标准 glTF 模型（.gltf / .glb），异步接口完成加载及渲染 |
| 自定义灯光/相机/节点 | 自定义场景灯光、渲染视角，动态调整场景树结构及节点属性 |
| 资源创建 | 创建图片（Image）、材质（Material）、环境（Environment）及自定义着色器（Shader） |
| 动画控制 | 控制动画开始、暂停、结束、播放到指定位置，提供动画回调 |
| 后处理 | ToneMapping 等基础 3D 渲染后处理能力 |

### 关键 API

| API | 说明 |
|---|---|
| `@ohos.graphics.scene` | ArkGraphics 3D 主模块，场景加载与渲染入口 |
| `Scene` | 场景管理，加载模型、创建节点、管理资源 |
| `SceneNode` | 节点管理，操作场景树中的各类节点 |
| `SceneResource` | 资源管理，管理图片、材质、环境、着色器等资源 |
| `ScenePostProcessSettings` | 后处理管理，ToneMapping 等后处理控制 |

### 框架原理

- 图形后端：GPU 硬件驱动接口（OpenGL ES / Vulkan）
- 引擎层：Ark Graphics Platform（AGP）渲染引擎，ECS 架构设计
- 接口层：基于 NAPI 暴露 3D 渲染接口

### 约束限制

需硬件设备支持 OpenGL ES 3.2 以上或 Vulkan 1.0 以上的 GPU 驱动。

### 权限要求

无特殊权限要求。

### 官方链接

- [ArkGraphics 3D 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-overview)
- [ArkGraphics 3D 场景搭建及管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-scene)
- [ArkGraphics 3D 场景动画控制及管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics3d-animation)

---

## Spatial Recon Kit — 空间建模服务

### 概述

Spatial Recon Kit 集成了 3DGS（3D Gaussian Splatting）模型的渲染、运算等能力，便于用户对三维模型实现自定义操作。是 ArkGraphics 3D 模块的扩展，需与 ArkGraphics 3D 联合使用。

- npm 包名：`@kit.SpatialReconKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 3DGS 模型加载 | 加载不同格式的三维模型（MP4、PLY、GLB） |
| 滤镜 | 对渲染图像进行风格化处理 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone、Tablet、PC/2in1、TV |

### 关键 API

| API | 说明 |
|---|---|
| `SpatialRecon` | 空间建模核心模块 |
| `spatial_recon_interface.h` | C/C++ 接口头文件 |

### 权限要求

详情请参考官方文档。

### 官方链接

- [Spatial Recon Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/spatial-recon-introduction)
- [重建三维场景 C/C++](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/spatial-recon-c-spatial-recon-pipeline)

---

## Graphics Accelerate Kit — 图形加速服务

### 概述

Graphics Accelerate Kit 是集成了先进图形渲染加速和资源管理优化的综合解决方案，通过软硬件协同优化，全面提升图形处理相关应用的性能和用户体验。已构建三大核心服务：游戏渲染加速、游戏资源加速、游戏启动加速。

- npm 包名：`@kit.GraphicsAccelerateKit`
- 模拟器：暂不支持

### 核心能力

| 服务 | 功能模块 | 说明 |
|---|---|---|
| 游戏渲染加速 | 超帧 | 利用 MEMC 技术在真实渲染帧间插入预测帧，提升帧率降低功耗 |
| 游戏渲染加速 | ABR | 自适应稳态渲染，感知游戏/设备状态动态调整分辨率，稳定帧率降低功耗 |
| 游戏渲染加速 | OpenGTX | LTPO 方案自适应调整帧率/SOC/DDR 频率，降低负载和功耗 |
| 游戏资源加速 | 资源包后台下载 | 静默下载资源文件，减少启动等待时间，即开即玩 |
| 游戏启动加速 | 秒级启动 | 退出时制作内存镜像，下次冷启动加载镜像实现秒开 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 游戏渲染加速支持设备 | Phone、Tablet、TV |
| 游戏资源加速支持设备 | Phone、Tablet |
| 游戏启动加速支持设备 | Phone、Tablet、PC/2in1 |

### 关键 API

| API | 说明 |
|---|---|
| `GraphicsAccelerate` | 图形加速主模块 |
| `frame_generation_base.h` | 超帧相关接口 |

### 权限要求

详情请参考官方文档。

### 官方链接

- [Graphics Accelerate Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-accelerate-introduction)
- [游戏渲染加速服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-accelerate-rendering)
- [超帧](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-accelerate-fg)
- [ABR](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-accelerate-abr)
- [OpenGTX](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-accelerate-opengtx)

---

## XEngine Kit — GPU加速引擎服务

### 概述

XEngine Kit 提供基于马良 GPU 的性能提升方案，包括超分、自适应 VRS、Subpass Shading、光线追踪技术（反射、阴影、环境光遮蔽、全局光照）和高性能着色器等，通过图形算法及软硬件优化实现更高画质、更高性能、更低功耗。

- npm 包名：`@kit.XEngineKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 空域 GPU 超分 | 基于单帧图像的空域超采样，开销最低 |
| 空域 AI 超分 | GPU/NPU 协同空域超采样，效果更好 |
| 时域 AI 超分 | GPU/NPU 协同时域超采样，抗锯齿效果明显，画质更优，倍率更高 |
| 自适应 VRS | 合理分配画面计算资源，视觉无损降低渲染频次，提高渲染性能 |
| Subpass Shading | 降低 TBDR/Forward+ 管线带宽开销，提升性能 |
| 光线追踪（反射/阴影/AO） | 开箱即用的光追渲染技术，较少光线数达成较高画质 |
| 全局光照（DDGI/NNGI） | DDGI 轻量级配合端云渲染，NNGI 提供移动端更好动态 GI 画质 |
| 高性能 GPU 排序 | 降低排序时延，提升性能 |

### 关键 API

| API | 说明 |
|---|---|
| `HMS_XEG_GetString` | OpenGL ES 扩展特性查询 |
| `HMS_XEG_EnumerateDeviceExtensionProperties` | Vulkan 扩展特性查询 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| Syscap 要求 | 需查询 SystemCapability.Graphic.XEngine |
| 支持设备 | Phone、Tablet、PC/2in1、TV |
| GPU 要求 | 仅马良 GPU 芯片设备支持，不同设备特性范围有差异 |

### 权限要求

无特殊权限要求，但需查询设备 Syscap 支持情况。

### 官方链接

- [XEngine Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xengine-kit-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xengine-kit-preparations)
- [空域GPU超分](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xengine-kit-gpu-spatial-upscaling)
- [空域AI超分](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xengine-kit-ai-spatial-upscaling)
- [自适应VRS](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/xengine-kit-adaptive-vrs)
