# 基础 AI Kit 合集

## Core Speech Kit — 基础语音服务

### 概述

Core Speech Kit 集成了语音类基础 AI 能力，包括文本转语音（TextToSpeech）及语音识别（SpeechRecognizer）能力，便于用户与设备进行互动，实现实时输入的语音与文本之间相互转换。

- npm 包名：`@kit.CoreSpeechKit`
- 模拟器：支持（6.0.0(20) 版本起）

### 核心能力

| 能力 | 说明 |
|---|---|
| 文本转语音（TTS） | 将不超过 10000 字符的文本合成为语音并播报 |
| 语音识别（ASR） | 将音频信息转换为文本，短语音模式不超过 60s，长语音模式不超过 8h |

### 能力限制

| AI 能力 | 约束 |
|---|---|
| 文本转语音 | 语种：中文、英文；音色：聆小珊女声、英语劳拉女声、凌飞哲男声；文本长度 ≤ 10000 字符 |
| 语音识别 | 语种：中文普通话；模型：离线；短语音 ≤ 60s，长语音 ≤ 8h |

### 关键 API

| API | 说明 |
|---|---|
| `textToSpeech` | 文本转语音引擎，支持启动/停止/暂停合成播报 |
| `speechRecognizer` | 语音识别引擎，支持短语音/长语音模式识别 |
| 朗读控件 | 系统提供的 TTS UI 控件 |
| AI 字幕控件 | 系统提供的语音识别 UI 控件 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持设备 | Phone、Tablet、PC/2in1 |
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |

### 权限要求

- 麦克风权限（语音识别场景）

### 官方链接

- [Core Speech Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-speech-introduction)
- [文本转语音](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/texttospeech-guide)
- [示例：语音识别](https://gitcode.com/harmonyos_samples/core-speech-kit-sample-code-ark-ts-kit-asrdemo)
- [示例：文本转语音](https://gitcode.com/harmonyos_samples/core-speech-kit-sample-code-ark-ts-kit-ttsdemo)

---

## Core Vision Kit — 基础视觉服务

### 概述

Core Vision Kit 提供机器视觉相关基础能力，包括通用文字识别（OCR）、人脸检测、人脸比对、主体分割、多目标识别、骨骼点检测等。可结合 Vision Kit 的 UI 控件能力（如人脸活体检测）提升应用智能化交互体验。

- npm 包名：`@kit.CoreVisionKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 通用文字识别（OCR） | 扫描识别文档、名片、票据等印刷品文字 |
| 人脸检测 | 检测和定位照片中的人脸 |
| 人脸比对 | 1v1 人脸比对，用于身份验证场景 |
| 主体分割 | 检测前景物体/区域并从背景中分离 |
| 多目标识别 | 识别图片中常见目标对象（动物、植物、建筑、人、文本等）并给出位置 |
| 骨骼点检测 | 人体骨骼关键点检测，用于智能监控、人机交互等 |

### 能力限制

| AI 能力 | 约束 |
|---|---|
| 文字识别 | 图片格式：JPEG/JPG/PNG；语言：简中/英/日/韩/繁中；文本 ≤ 10000 字符；建议 720p+ |
| 人脸检测 | 建议 720p+；224px<高<15210px，100px<宽<10000px；不适合实时检测 |
| 人脸比对 | 仅 1v1；建议 720p+；同上尺寸约束 |
| 主体分割 | 物体占比 ≥ 0.5%；不建议含大量文字的图片；20px<高/宽<9000px |
| 多目标识别 | 建议 720p+；100px<高/宽<10000px；物体占比 > 0.1% |
| 骨骼点检测 | 建议 720p+；100px<高/宽<10000px |

### 关键 API

| API | 说明 |
|---|---|
| 文字识别接口 | OCR 文字识别与结果返回 |
| 人脸检测接口 | 检测图像中人脸位置及属性 |
| 人脸比对接口 | 1v1 人脸相似度比对 |
| 主体分割接口 | 前景主体检测与分割 |
| 多目标识别接口 | 多类别目标检测与定位 |
| 骨骼点检测接口 | 人体骨骼关键点检测 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持设备 | Phone、Tablet、PC/2in1 |
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 并发限制 | 支持多用户接入，不支持同一用户并发调用同一特性 |

### 权限要求

- 相机权限（实时检测场景）
- 图片/文件读取权限

### 官方链接

- [Core Vision Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-introduction)
- [通用文字识别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-text-recognition)
- [人脸检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-detector)
- [人脸比对](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-face-comparator)
- [主体分割](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-subject-segmentation)
- [多目标识别](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-object-detection)
- [骨骼点检测](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-vision-skeleton-detection)

---

## Natural Language Kit — 自然语言理解服务

### 概述

Natural Language Kit 提供文本语义理解相关基础能力，包括分词和实体抽取，帮助开发者处理和分析文本数据。

- npm 包名：`@kit.NaturalLanguageKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 分词 | 将文本切分为独立词语单元，是 NLP 基础步骤 |
| 实体抽取 | 从文本中识别特定实体：人名、地名、时间日期、数字、电话号码、邮箱地址、快递单号、航班号、网址链接、验证码、证件号 |

### 能力限制

| AI 能力 | 约束 |
|---|---|
| 分词 | 语言：简中/中文语境英文/繁中；文本 ≤ 1000 字符 |
| 实体抽取 | 语言：简中/中文语境英文/繁中；文本 ≤ 1000 字符；实体类型：时间/地点/邮箱/快递单号/航班号/人名/电话/网址/验证码/证件号 |

### 关键 API

| API | 说明 |
|---|---|
| 分词接口 | 文本分词，返回词语单元列表 |
| 实体抽取接口 | 从文本中识别并返回命名实体 |
| `textProcessing` | 文本处理统一 API |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持设备 | Phone、Tablet、PC/2in1 |
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 并发限制 | 支持多用户接入，不支持同一用户并发调用同一特性 |

### 权限要求

无特殊权限要求。

### 官方链接

- [Natural Language Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/natural-language-introduction)
- [分词](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/natural-language-getwordsegmentation)
- [示例：分词/实体抽取](https://gitcode.com/harmonyos_samples/natural-language-kit-sample-code-client-demo-arkts)
