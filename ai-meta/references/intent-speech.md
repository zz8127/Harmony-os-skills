# 意图框架与语音

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

HarmonyOS AI 能力覆盖意图智能分发、语音合成、语音识别、图像识别、ML 模型推理等。

| 能力 | Kit | 说明 |
|------|-----|------|
| 意图框架 | IntentsKit | 智能分发到小艺/搜索/建议 |
| 语音合成 | SpeechKit | TTS 文字转语音 |
| 语音识别 | SpeechKit | ASR 语音转文字 |
| 图像识别 | VisionKit | 文字/物体/面容识别 |
| 端侧 AI | MLKit | 本地模型推理 |

---

## 意图框架（IntentsKit）

### 核心概念

IntentsKit 是 HarmonyOS 级的**意图标准体系**，连接应用业务功能与系统入口，实现智慧分发。

- **系统入口**：小艺对话、小艺搜索、小艺建议
- **核心能力**：理解用户显性/潜在意图，匹配合适时宜的服务

### 意图分发流程

```
用户意图 → 系统感知 → AI大模型理解 → 意图框架匹配 → 应用/元服务响应
```

### 技能调用

```typescript
import { IntentsKit, IntentRequest, SkillContext } from '@kit.IntentsKit';

// 技能调用（应用向系统注册自身能力）
let skillContext: SkillContext = {
  skillId: 'my_skill_id',
  intentName: 'queryOrderStatus',
  params: {
    orderId: 'ORD12345'
  }
};

// 调用技能
IntentsKit.callSkill(skillContext, (result: IntentResult) => {
  console.info('Result: ' + JSON.stringify(result));
});
```

### 习惯推荐

应用可订阅用户习惯，在合适时机被系统主动推荐：

```typescript
// 注册习惯推荐回调
IntentsKit.onHabitRecommendation((habit: HabitInfo) => {
  console.info('User habit: ' + habit.action);
  // 根据用户习惯主动展示相关内容
});
```

### 场景化推送

| 场景 | 说明 |
|------|------|
| 习惯建议 | 根据用户规律行为定时推送 |
| 活动推荐 | 基于位置/时间的活动提醒 |
| 位置建议 | 进入特定区域时触发 |

---

## 语音合成（TTS）

```typescript
import { voicerTtsEngine } from '@kit.SpeechKit';

let ttsParams = {
  language: 'zh-CN',
  person: 0,      // 发音人（0=女声，1=男声）
  speed: 1.0,     // 语速（0.5-2.0）
  pitch: 1.0,     // 音调（0.5-2.0）
  volume: 1.0     // 音量（0.0-1.0）
};

let ttsEngine = voicerTtsEngine.createTtsEngine(context, ttsParams);
ttsEngine.speak('你好，这是语音合成示例', '');
```

---

## 语音识别（ASR）

```typescript
import { speechRecognizer } from '@kit.SpeechKit';

let recognizer = speechRecognizer.createSpeechRecognizer(context);

recognizer.on('recognize', (result: string) => {
  console.info('Recognized: ' + result);
});

recognizer.startListening({
  language: 'zh-CN',
  fullTextDictation: true
});
```

---

## 官方参考

- IntentsKit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-introduction-V5
- 技能调用方案：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-skill-all-rec-introduction
- IntentsKit SDK：https://developer.huawei.com/consumer/cn/sdk/intents-kit
