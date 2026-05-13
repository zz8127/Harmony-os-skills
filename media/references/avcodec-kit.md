# AVCodec Kit — 编解码

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

AVCodec Kit 提供音视频编解码能力，包括硬件编解码和软件编解码，支持多种媒体格式。

---

## 支持的编解码格式

### 视频解码

| 格式 | 硬解 | 软解 | 说明 |
|------|------|------|------|
| H.264 (AVC) | ✅ | ✅ | 主流格式，兼容性最好 |
| H.265 (HEVC) | ✅ | ✅ | 高压缩率 |
| AV1 | ✅ | ✅ (API 23+) | 开源免版税格式 |
| VP9 | — | ✅ (API 23+) | WebM 格式 |
| VP8 | — | ✅ (API 23+) | WebM 格式 |
| MPEG-1 | — | ✅ (API 23+) | 传统格式 |

### 视频编码

| 格式 | 硬编 | 软编 |
|------|------|------|
| H.264 (AVC) | ✅ | ✅ |
| H.265 (HEVC) | ✅ | ✅ |

### 音频编解码

| 格式 | 解码 | 编码 |
|------|------|------|
| AAC | ✅ | ✅ |
| MP3 | ✅ | — |
| FLAC | ✅ | — |
| OPUS | ✅ | ✅ |

---

## 基本用法

### 创建解码器

```typescript
import { avcodec } from '@kit.MediaKit'

let videoDecoder = avcodec.createVideoDecoder('avcodec.video.decoder.hevc')

let audioDecoder = avcodec.createAudioDecoder('avcodec.audio.decoder.aac')
```

### 创建编码器

```typescript
let videoEncoder = avcodec.createVideoEncoder('avcodec.video.encoder.hevc')

let audioEncoder = avcodec.createAudioEncoder('avcodec.audio.encoder.aac')
```

---

## API 23 新增（HarmonyOS 6.1.0）

### 软解码格式扩展

新增支持以下视频格式的软解码能力：AV1、VP9、VP8、RV30、RV40、WVC1、DVVIDEO、RAWVIDEO、MPEG1。

这意味着开发者无需依赖硬件解码，即可在更多设备上播放这些格式的视频内容。

---

## Kit 导入

```typescript
import { avcodec } from '@kit.MediaKit'
```

---

## 官方参考

- AVCodec Kit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/avcodec-support-formats
- 视频解码：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/video-decoding
- 视频编码：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/video-encoding
- 音频解码：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-decoding
