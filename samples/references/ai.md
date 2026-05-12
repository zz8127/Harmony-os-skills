# AI 功能示例（AI）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## VisionKit（端侧视觉）

### 多目标识别

**Gitee 仓**：https://gitee.com/HarmonyOS_Samples/CoreVisionKit-SampleCode-ArkTS-ObjectDetectDemo

```typescript
import vision from '@kit.VisionKit';

// 创建视觉分析器
let visionAnalyzer = vision.createVisionAnalyzer();
visionAnalyzer.setCallback((result) => {
  result.items.forEach(item => {
    console.info('识别类别：' + item.type);
    console.info('置信度：' + item置信度);
  });
});

// 配置分析器（多目标识别）
let config = {
  type: 'multiObjectDetection'
};
visionAnalyzer.setVisionConfiguration(config);

// 传入图像并分析
visionAnalyzer.analyzeImage(imageSource);
```

### 文字识别（OCR）

```typescript
import textRecognition from '@kit.VisionKit';

let textRecognizer = textRecognition.createTextRecognizer();
let result = await textRecognizer.recognize(imageSource);
console.info('识别文字：' + result.value);
```

---

## AR Engine（AR Engine）

### FaceAR — 人脸跟踪（API 23 新增）

`@kit.AREngine` 新增 FaceAR 能力，支持人脸几何数据 + 微表情捕捉（虚拟主播/动态特效/摄影美化）：

```typescript
import { arEngine, ARView, arViewController } from '@kit.AREngine';
import { Node, Scene } from '@kit.ArkGraphics3D';

let face: arEngine.ARFace;
let faceGeometry: arEngine.ARGeometry;
let faceBlendShapes: arEngine.ARBlendShapes;
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-face

### BodyAR — 人体骨骼关键点识别（API 23 新增）

人体跟踪与骨骼关键点识别，适用于健身/瑜伽/舞蹈教学/虚拟穿搭应用：

```typescript
// 获取 AR Session
let session: arEngine.ARSession = arEngine.createSession(context);

// 获取人体跟踪数据
let frame = session.getFrame();
let bodySkeleton = frame.acquireBodySkeleton();  // 人体对象数组
let landmarks2D = bodySkeleton.getLandmarks2D();  // 骨骼关键点数组
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arengine-body

---

## MLKit（端侧 AI 推理）

```typescript
import mlService from '@kit.AIMLKit';

// 加载模型
let modelManager = mlService.getModelManager();
let model = await modelManager.loadModelFromFd(fd, {});

// 执行推理
let inputs = [inputTensor];
let outputs = await modelService.execute(model, inputs);
```

---

## 语音合成（TTS）

```typescript
import speech from '@kit.SpeechKit';

// 创建语音合成器
let synthesizer = speech.createTtsEngine();

// 设置监听
synthesizer.setCallback({
  onStart(sessionId, requestId) {
    console.info('开始合成');
  },
  onComplete(sessionId, requestId) {
    console.info('合成完成');
  },
  onError(sessionId, errorCode, errorMsg) {
    console.error('合成失败：' + errorMsg);
  }
});

// 合成文本
let options = {
  requestId: '1',
  text: '你好 HarmonyOS',
  extra: { speed: 1.0, pitch: 1.0, volume: 1.0 }
};
synthesizer.speak(options);

// 停止
synthesizer.stop();
synthesizer.shutdown();
```

---

## 意图框架（IntentsKit）

```技能已在 `../ai-meta/SKILL.md` 中详细描述，此处仅列示例入口

## IFAA 免密认证

**Gitee 仓**：https://gitee.com/heshengbang/OnlineAuthenticationkit-sample-IFAAClientdemo-ArkTS

```typescript
import { ifaa } from '@kit.OnlineAuthenticationKit';

// 开通认证
let preAuthResult = await ifaa.preAuth();

// 发起认证
let authToken = new Uint8Array([/* 服务器下发的 token */]);
let authData = new Uint8Array([/* 认证数据 */]);
let result = await ifaa.auth(authToken, authData);
console.info('认证结果：' + result);
```

---

## 官方参考

- VisionKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/vision-kit
- MLKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ai-ml-kit
- 语音合成：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/speech-synthesis
- IFAA：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ifaa-intro
