# 异构计算（CANN Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。
> **Kit 导入**：`@kit.CANNKit`
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-kit-overview-V5

---

## 概述

CANN（Compute Architecture for Neural Networks）Kit 提供 NPU 异构计算加速能力，支持在华为设备上高效部署和运行 AI 推理模型。适用于图像分类、目标检测、自然语言处理等场景，通过 NNAPI 兼容层实现跨平台模型部署。

### 核心能力

| 能力 | 说明 |
|------|------|
| 模型部署 | 将训练好的模型转换为 CANN 支持格式并部署到设备 |
| 推理加速 | 利用 NPU 硬件加速推理，降低延迟、提升吞吐 |
| NNAPI 兼容 | 兼容 Android NNAPI 接口，降低迁移成本 |
| 多场景支持 | 图像分类、目标检测、语义分割、NLP 等 |

---

## 模型部署

### 模型转换

CANN 支持 ONNX、Caffe 等框架训练的模型，需通过 ATC（Ascend Tensor Compiler）工具转换为 `.om` 格式。

```bash
atc --model=resnet50.onnx \
    --framework=5 \
    --output=resnet50 \
    --soc_version=Ascend310P \
    --input_shape="input:1,3,224,224"
```

### 模型加载

```typescript
import { cann } from '@kit.CANNKit';

async function loadModel(modelPath: string): Promise<cann.Model> {
  const model = await cann.loadModel({
    modelPath: modelPath,
    deviceId: 0
  });
  return model;
}
```

---

## 推理加速

### 创建推理会话

```typescript
import { cann } from '@kit.CANNKit';

async function createInferenceSession(model: cann.Model): Promise<cann.InferenceSession> {
  const session = await cann.createInferenceSession({
    model: model,
    deviceId: 0
  });
  return session;
}
```

### 执行推理

```typescript
import { cann } from '@kit.CANNKit';

async function runInference(session: cann.InferenceSession, inputData: Float32Array): Promise<Float32Array> {
  const inputTensor: cann.Tensor = {
    data: inputData.buffer,
    shape: [1, 3, 224, 224],
    dataType: cann.DataType.FLOAT32
  };
  const outputTensors = await session.run([inputTensor]);
  return new Float32Array(outputTensors[0].data);
}
```

### 异步推理与回调

```typescript
import { cann } from '@kit.CANNKit';

async function runInferenceAsync(session: cann.InferenceSession, inputData: Float32Array): Promise<void> {
  const inputTensor: cann.Tensor = {
    data: inputData.buffer,
    shape: [1, 3, 224, 224],
    dataType: cann.DataType.FLOAT32
  };
  session.runAsync([inputTensor], (outputs: cann.Tensor[]) => {
    const result = new Float32Array(outputs[0].data);
    console.info(`inference completed, output size=${result.length}`);
  });
}
```

---

## NNAPI 兼容

CANN Kit 提供 NNAPI 兼容层，使基于 NNAPI 开发的模型可无缝迁移到 HarmonyOS NPU 上运行。

### NNAPI 模型编译

```typescript
import { cann } from '@kit.CANNKit';

async function compileNNAPIModel(modelPath: string): Promise<cann.CompiledModel> {
  const compiledModel = await cann.compileModel({
    modelPath: modelPath,
    preference: cann.ExecutionPreference.FAST_SINGLE_ANSWER,
    deviceId: 0
  });
  return compiledModel;
}
```

### NNAPI 推理执行

```typescript
import { cann } from '@kit.CANNKit';

async function executeNNAPIInference(compiledModel: cann.CompiledModel, inputData: Float32Array): Promise<Float32Array> {
  const inputTensor: cann.Tensor = {
    data: inputData.buffer,
    shape: [1, 3, 224, 224],
    dataType: cann.DataType.FLOAT32
  };
  const output = await compiledModel.execute([inputTensor]);
  return new Float32Array(output[0].data);
}
```

---

## 典型应用场景

### 图像分类

```typescript
import { cann } from '@kit.CANNKit';
import { image } from '@kit.ImageKit';

async function classifyImage(imagePath: string, session: cann.InferenceSession): Promise<number> {
  const imageSource = image.createImageSource(imagePath);
  const pixelMap = await imageSource.createPixelMap();
  const imageData = new Uint8Array(pixelMap.getPixelBytesNumber());
  await pixelMap.readPixelsToBuffer(imageData.buffer);
  const floatData = new Float32Array(imageData.length);
  for (let i = 0; i < imageData.length; i++) {
    floatData[i] = imageData[i] / 255.0;
  }
  const inputTensor: cann.Tensor = {
    data: floatData.buffer,
    shape: [1, 3, 224, 224],
    dataType: cann.DataType.FLOAT32
  };
  const outputs = await session.run([inputTensor]);
  const probabilities = new Float32Array(outputs[0].data);
  let maxIdx = 0;
  for (let i = 1; i < probabilities.length; i++) {
    if (probabilities[i] > probabilities[maxIdx]) {
      maxIdx = i;
    }
  }
  return maxIdx;
}
```

### 目标检测

```typescript
import { cann } from '@kit.CANNKit';

interface DetectionBox {
  x1: number;
  y1: number;
  x2: number;
  y2: number;
  score: number;
  classId: number;
}

function parseDetectionOutput(output: Float32Array, confidenceThreshold: number): DetectionBox[] {
  const boxes: DetectionBox[] = [];
  const numDetections = output.length / 6;
  for (let i = 0; i < numDetections; i++) {
    const offset = i * 6;
    const score = output[offset + 4];
    if (score >= confidenceThreshold) {
      boxes.push({
        x1: output[offset],
        y1: output[offset + 1],
        x2: output[offset + 2],
        y2: output[offset + 3],
        score: score,
        classId: Math.floor(output[offset + 5])
      });
    }
  }
  return boxes;
}

async function detectObjects(imageData: Float32Array, session: cann.InferenceSession): Promise<DetectionBox[]> {
  const inputTensor: cann.Tensor = {
    data: imageData.buffer,
    shape: [1, 3, 640, 640],
    dataType: cann.DataType.FLOAT32
  };
  const outputs = await session.run([inputTensor]);
  const rawOutput = new Float32Array(outputs[0].data);
  return parseDetectionOutput(rawOutput, 0.5);
}
```

### NLP 文本推理

```typescript
import { cann } from '@kit.CANNKit';

async function textInference(tokenIds: Int32Array, session: cann.InferenceSession): Promise<Float32Array> {
  const inputTensor: cann.Tensor = {
    data: tokenIds.buffer,
    shape: [1, tokenIds.length],
    dataType: cann.DataType.INT32
  };
  const outputs = await session.run([inputTensor]);
  return new Float32Array(outputs[0].data);
}
```

---

## 资源管理

### 释放资源

```typescript
import { cann } from '@kit.CANNKit';

async function releaseResources(session: cann.InferenceSession, model: cann.Model): Promise<void> {
  await session.release();
  await model.release();
}
```

---

## 权限配置

```json5
// module.json5
{
  "requestPermissions": [
    {
      "name": "ohos.permission.INTERNET"
    }
  ]
}
```

> CANN Kit 使用 NPU 硬件资源，需确保设备支持 Ascend NPU。部分设备可能不支持 CANN 加速，需通过 `cann.isDeviceSupported()` 检查。

---

## 官方参考

- **CANN Kit 概述**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-kit-overview-V5
- **模型部署指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-model-deployment-V5
- **推理加速指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-inference-acceleration-V5
- **NNAPI 兼容指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cann-nnapi-compatibility-V5
- **API 参考**：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cann-api-overview