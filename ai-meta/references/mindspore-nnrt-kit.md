# 推理运行时 Kit 合集

## MindSpore Lite Kit — 昇思推理框架服务

### 概述

MindSpore Lite 是 HarmonyOS 内置的轻量化 AI 引擎，面向全场景构建支持多处理器架构的开放 AI 架构，为开发者提供端到端解决方案。已在图像分类、目标识别、人脸识别、文字识别等应用中广泛使用。

- npm 包名：`@kit.MindSporeLiteKit`
- 模拟器：支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 图像分类 | 给定图像判断所属类别（猫、狗、飞机等） |
| 目标检测 | 检测摄像头输入帧中的对象并添加标签和边框 |
| 图像分割 | 检测目标在图片中的位置或像素归属 |
| 模型转换 | 支持 TensorFlow/TensorFlow Lite/Caffe/ONNX 模型转换为 .ms 格式 |
| 模型推理 | 加载 .ms 模型文件执行推理 |
| 端侧训练 | 支持端侧模型训练 |

### 亮点优势

| 优势 | 说明 |
|---|---|
| 更优性能 | 高效内核算法和汇编级优化，支持 CPU/NNRt 高性能推理 |
| 轻量化 | 超轻量方案，支持模型量化压缩 |
| 全场景支持 | 支持多种操作系统及嵌入式系统 |
| 高效部署 | 支持 MindSpore/TFLite/Caffe/ONNX 模型，统一训练和推理 IR |

### 开发流程

1. 模型转换：使用转换工具将第三方框架模型转为 .ms 格式
2. 模型部署：
   - 创建推理/训练上下文（指定硬件、线程数等）
   - 加载 .ms 模型文件
   - 设置模型输入数据
   - 执行推理/训练，读取输出

### 开发方式

| 方式 | 说明 |
|---|---|
| ArkTS API | 直接在 UI 代码中调用 MindSpore Lite ArkTS API，快速验证效果 |
| Native API | 将算法模型和 Native API 调用封装成动态库，通过 N-API 封装为 ArkTS 接口 |

### 关键 API

| API | 说明 |
|---|---|
| `@ohos.ai.mindSpore` | MindSpore Lite ArkTS 主模块 |
| MindSpore Lite Native API | C/C++ 接口，用于高性能推理场景 |
| 模型转换工具 | conveter 工具，将第三方模型转为 .ms 格式 |

### 与其他 Kit 的关系

HarmonyOS AI 开放层次（上层→底层）：

1. **MindSpore Lite Kit** — 轻量化 AI 引擎，统一推理接口 + 多后端硬件加速
2. **Neural Network Runtime Kit** — 跨芯片推理计算运行时，连通推理框架与加速芯片
3. **CANN Kit** — 海思 AI 硬件统一开放计算架构

MindSpore Lite 与 NNRt 共享 MindIR 模型图格式，无需构图即可对接，加载更高效。还支持 CPU/GPU 与 NNRt AI 加速硬件之间的模型异构推理。

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持设备 | Phone、Tablet、PC/2in1、TV |

### 权限要求

无特殊权限要求。

### 官方链接

- [MindSpore Lite Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-lite-kit-introduction)
- [使用 MindSpore Lite 进行模型转换](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-lite-converter-guidelines)
- [使用 MindSpore Lite 进行模型推理 C/C++](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-lite-guidelines)
- [使用 MindSpore Lite 进行端侧训练 C/C++](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-lite-train-guidelines)
- [ArkTS API 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-guidelines-based-js)
- [Native API 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mindspore-guidelines-based-native)

---

## Neural Network Runtime Kit — Neural Network 运行时服务

### 概述

Neural Network Runtime（NNRt）是面向 AI 领域的跨芯片推理计算运行时，作为中间桥梁连通上层 AI 推理框架和底层加速芯片，实现 AI 模型的跨芯片推理计算。主要面向 AI 推理框架开发者或希望直接使用 AI 加速硬件的应用开发者。

- npm 包名：`@kit.NeuralNetworkRuntimeKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 在线构图 | AI 推理框架将模型图转换为 NNRt 内部模型图 |
| 模型编译 | 将模型图或离线模型在 AI 硬件驱动上编译为硬件相关模型对象 |
| 模型推理 | 基于编译模型创建执行器，设置输入输出张量，在 AI 硬件上执行推理 |
| 内存管理 | 在 AI 硬件驱动上申请共享内存，实现输入输出数据"零拷贝" |
| 设备管理 | 展示 NNRt 对接的 AI 硬件信息，提供选择 AI 硬件功能 |
| 模型缓存 | 将编译模型保存为缓存，下次加载大幅提升编译速度 |
| 离线模型推理 | 直接使用 AI 硬件相关离线模型文件推理，编译速度快但仅限对应硬件 |

### 亮点特征

- 统一 AI 加速硬件推理接口，支持无感知跨 AI 硬件推理
- 提供构图接口，让 AI 推理框架对接 NNRt
- 模型编译缓存功能，大幅加快模型加载速度
- 硬件相关离线模型加载，缩短编译时间
- 支持配置推理优先级、性能模式、FP16 模式及自定义扩展属性
- 通过 AI 硬件驱动共享内存实现数据"零拷贝"

### 能力范围

| 项目 | 说明 |
|---|---|
| 硬件支持 | 仅提供已接入的 AI 加速硬件推理能力，不提供 CPU 等通用硬件推理 |
| 算子支持 | 目前支持常用算子 56 个，后续版本逐步增加 |
| 推理模式 | 目前仅支持同步推理，后续版本支持异步推理 |
| 并发构图 | 不支持多线程并发构图；并发编译/执行取决于底层硬件驱动 |

### 关键 API

| API | 说明 |
|---|---|
| `neural_network_runtime.h` | NNRt 核心 C/C++ 接口头文件 |
| `neural_network_core.h` | NNRt 核心 API 头文件 |
| `NN_Tensor` | 张量管理接口 |
| 构图接口 | 将推理框架模型图转换为 NNRt 内部模型图 |
| 编译接口 | 编译模型为硬件相关对象 |
| 执行接口 | 创建执行器并执行推理 |

### 与其他 Kit 的关系

HarmonyOS AI 开放层次（上层→底层）：

1. **MindSpore Lite Kit** — 轻量化 AI 引擎
2. **Neural Network Runtime Kit** — 跨芯片推理计算运行时（本 Kit）
3. **CANN Kit** — 海思 AI 硬件统一开放计算架构

MindSpore Lite 与 NNRt 共享 MindIR 格式，无需构图即可对接。CANN Kit 作为麒麟平台后端接入 NNRt，支撑麒麟平台 AI 计算能力。

### 约束与限制

| 项目 | 说明 |
|---|---|
| 硬件要求 | 强依赖硬件，仅适用于支持 NPU 的设备 |

### 权限要求

无特殊权限要求，但依赖 NPU 硬件支持。

### 官方链接

- [Neural Network Runtime Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/neural-network-runtime-kit-introduction)
- [NNRt 对接 AI 推理框架开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/neural-network-runtime-guidelines)
- [neural_network_runtime.h 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-runtime-h)
- [neural_network_core.h 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-neural-network-core-h)
