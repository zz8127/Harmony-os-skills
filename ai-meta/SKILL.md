---
name: harmonyos-ai-meta
description: |
  HarmonyOS AI 能力与元服务开发规范。
  触发场景：开发意图智能分发、语音合成/识别、图像识别、元服务（服务卡片）、服务流转时。
  包含：IntentsKit（意图框架/智慧分发）、SpeechKit（语音）、VisionKit（视觉）、MLKit（端侧AI）、元服务（Service Widget/卡片）、服务流转。
---

# HarmonyOS AI 与元服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 快速导航

| 能力 | 说明 |
|------|------|
| [意图框架](references/intent-speech.md) | IntentsKit：智慧分发到小艺/搜索/建议 |
| [语音合成/识别](references/intent-speech.md) | SpeechKit：TTS / ASR |
| [元服务/卡片](references/meta-service.md) | Service Widget：免安装服务卡片 |
| [服务流转](references/meta-service.md) | 设备间服务无缝迁移 |
| [异构计算](references/cann-kit.md) | CANN Kit：NPU 推理加速/模型部署 |
| [智能体框架](references/agent-framework.md) | Agent Framework Kit：Agent 创建/Tool/多 Agent 协作 |

---

## AI Kit 总览

| Kit | npm 包 | 说明 |
|-----|-------|------|
| IntentsKit | `@kit.IntentsKit` | 意图框架，智慧分发 |
| SpeechKit | `@kit.SpeechKit` | 语音合成（TTS）、语音识别（ASR） |
| VisionKit | `@kit.VisionKit` | 文字识别、物体识别、人脸检测 |
| MLKit | @kit.MLKit | 端侧 AI 模型推理 |
| CANNKit | @kit.CANNKit | NPU 异构计算，推理加速 |
| AgentFrameworkKit | @kit.AgentFrameworkKit | 智能体框架，多 Agent 协作（API 23 新增） |

---

## 意图框架（IntentsKit）

### 智慧分发价值

- **新流量入口**：出现在小艺对话、小艺搜索、小艺建议
- **主动服务**：无需用户主动搜索，服务主动触达用户
- **意图匹配**：基于 AI 大模型理解用户当前需求，精准匹配应用能力

### 接入流程

1. 在 AppGallery Connect 开通 IntentsKit 能力
2. 在应用中定义应用的技能（Skill）
3. 配置意图描述文件（intent.json）
4. 提交审核，审核通过后自动出现在系统入口

### 场景示例

| 场景 | 用户意图 | 应用响应 |
|------|---------|---------|
| 订餐 | "帮我订个外卖" | 打开订餐应用，搜索附近餐厅 |
| 出行 | "打车去机场" | 拉起打车应用，预填目的地 |
| 音乐 | "播放点轻松的音乐" | 打开音乐应用，推荐歌单 |

---

## 端侧 AI（MLKit）

```typescript
import { mlAiSession } from '@kit.MLKit';

// 创建本地 AI 会话（无需联网）
let session = await mlAiSession.createSession({
  modelPath: 'model/mlmodel'
});

// 执行推理
let result = await session.run({ input: imageData });
```

---

## AR Engine 扩展（API 23）

| 新增能力 | 说明 |
|---------|------|
| 人脸识别与跟踪 | FaceAR：支持人脸识别与跟踪能力（ArkTS + C/C++） |
| 人体骨骼关键点识别 | BodyAR：支持人体骨骼关键点识别与跟踪能力（ArkTS + C/C++） |
| 3D 空间重建会话管理 | 支持实时 3D 环境重建、3DGS 场景建模、任务控制、进度查询、模型导出 |
| 营销组件 | AR 营销互动能力 |
| 多设备扩展 | 多 Kit 扩展对 PC/2in1、TV 设备支持 |

FaceAR 和 BodyAR 此前已支持，详见 dev/SKILL.md。

---

## Vision Kit（视觉识别）

| 能力 | 说明 |
|------|------|
| 文字识别（OCR） | 图片中识别文字内容 |
| 物体识别 | 识别图片中的物体类别 |
| 人脸检测 | 检测人脸位置和关键点 |
| 条码识别 | 识别二维码/条形码 |

> Vision Kit 能力通过 `@kit.VisionKit` 导入，与 Scan Kit 的扫码能力互补。

---

## API 24 Beta1 变更追踪（2026-04-30）

| Kit | 变更 |
|-----|------|
| FAST Kit | 并发哈希表、向量运算和滤波器 |
| Performance Analysis Kit | 资源采集和崩溃日志分析增强 |
| Content Embed Kit | **全新 Kit** — 内容嵌入服务 |
| Enterprise Threat Protection Kit | **全新 Kit** — 企业威胁防护服务 |

---

## 官方参考

- IntentsKit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/intents-introduction-V5
- IntentsKit SDK：https://developer.huawei.com/consumer/cn/sdk/intents-kit
- ML Kit 端侧 AI：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ml-kit-overview-V5
- 元服务概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-widget-overview-V5
