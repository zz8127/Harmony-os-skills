# Audio Kit — 音频管理

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Audio Kit 提供音频管理能力，包括音量控制、音频流管理、音频焦点、设备管理、系统音效等。

---

## 音量管理

```typescript
import { audio } from '@kit.AudioKit'

let audioManager = audio.getAudioManager()
let volumeManager = audioManager.getVolumeManager()

let volume = await volumeManager.getVolume(audio.AudioVolumeType.MEDIA)

await volumeManager.setVolume(audio.AudioVolumeType.MEDIA, 50)

volumeManager.on('volumeChange', (volumeEvent: audio.VolumeEvent) => {
  console.info('Volume changed: ' + volumeEvent.volume)
})
```

---

## 音频渲染（播放）

```typescript
import { audio } from '@kit.AudioKit'

let audioRenderer = await audio.createAudioRenderer({
  streamInfo: {
    samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
    channels: audio.AudioChannel.CHANNEL_2,
    sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
    encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
  },
  rendererInfo: {
    usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
    rendererFlags: 0
  }
})

await audioRenderer.start()
await audioRenderer.write(buffer)
await audioRenderer.stop()
await audioRenderer.release()
```

---

## 音频采集（录音）

```typescript
import { audio } from '@kit.AudioKit'

let audioCapturer = await audio.createAudioCapturer({
  streamInfo: {
    samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
    channels: audio.AudioChannel.CHANNEL_2,
    sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
    encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
  },
  capturerInfo: {
    source: audio.SourceType.SOURCE_TYPE_MIC,
    capturerFlags: 0
  }
})

await audioCapturer.start()
let buffer = await audioCapturer.read(BUFFER_SIZE)
await audioCapturer.stop()
await audioCapturer.release()
```

---

## 音频焦点

```typescript
import { audio } from '@kit.AudioKit'

let audioManager = audio.getAudioManager()
let audioSessionManager = audioManager.getAudioSessionManager()

await audioSessionManager.requestAudioFocus({
  streamUsage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  contentType: audio.ContentType.CONTENT_TYPE_MUSIC,
  pauseWhenDucked: true
})

await audioSessionManager.abandonAudioFocus()
```

---

## API 23 新增（HarmonyOS 6.1.0）

### 变声效果

新增 C API，支持变声效果节点变声类型设置和设置结果查询。

### 系统音效管理

新增 `@ohos.multimedia.systemSoundManager` 模块，提供管理系统声音的基础能力，包括系统音效类型定义、获取系统音效播放器等。

```typescript
import { systemSoundManager } from '@kit.AudioKit'

let manager = systemSoundManager.getSystemSoundManager()
```

### 音频路由时延

AudioRenderer 新增 `getLatency` 接口，获取当前音频路由的预估时延。

```typescript
let latency = audioRenderer.getLatency()
```

### 音量变化回调增强

StreamVolumeEvent 新增"上一音量值"字段，用于获取音量变化前的音量值。

---

## Kit 导入

```typescript
import { audio } from '@kit.AudioKit'
```

---

## 官方参考

- Audio Kit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-overview-V5
- 音频播放：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-playback
- 音频录制：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-recording
- 音量管理：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/audio-volume-management
