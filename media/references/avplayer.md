# 音视频播放（AVPlayer）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## AVPlayer 开发流程

```
1. 创建 AVPlayer 实例
2. 设置播放源（url / fdSrc）
3. 配置播放参数
4. prepare() → play()
5. 监听播放事件
6. 播放完成或退出时 release()
```

## 基础播放

```typescript
import { avPlayer } from '@kit.MediaKit';
import { common } from '@kit.AbilityKit';

let context = getContext(this) as common.UIAbilityContext;
let avPlayer: avPlayer.AVPlayer = await avPlayer.createAVPlayer();

// 设置播放源
avPlayer.url = 'https://example.com/video.mp4';

// 配置监听
avPlayer.on('playbackEvent', (errCode: number, errMsg: string) => {
  console.info('Event: ' + errCode + ', ' + errMsg);
});

// 准备并播放
await avPlayer.prepare();
await avPlayer.play();

// 暂停
await avPlayer.pause();

// 停止
await avPlayer.stop();

// 释放
await avPlayer.release();
```

## 播放进度控制

```typescript
// 跳转
await avPlayer.seek(50000);  // 毫秒

// 倍速播放
await avPlayer.setPlaybackSpeed(avPlayer.PlaybackSpeed.Speed_Forward_2_00_X);

// 获取当前进度
let currentTime = avPlayer.currentTime;
let duration = avPlayer.duration;
```

## 音频焦点管理（AudioKit）

```typescript
import { audio from '@kit.AudioKit';

// 创建音频流
let audioManager = audio.getAudioManager();
let audioRenderer = await audioManager.createAudioRenderer({
  streamInfo: {
    samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
    channels: audio.AudioChannel.CHANNEL_2,
    encodingType: audio.AudioEncodingType.ENCODING_TYPE_MP3,
    contentType: audio.AudioContentType.CONTENT_TYPE_MUSIC,
    usage: audio.AudioUsage.AUDIO_USAGE_MEDIA
  }
});

// 开始渲染
await audioRenderer.start();

// 停止
await audioRenderer.stop();
```

---

## API 23 新增（HarmonyOS 6.1.0）

### AVCodec Kit — 软解码能力扩展

新增支持以下视频格式的软解码：AV1、VP9、VP8、RV30、RV40、WVC1、DVVIDEO、RAWVIDEO、MPEG1。

```typescript
import { avcodec } from '@kit.MediaKit'

// 创建软解码器
let videoDecoder = await avcodec.createVideoDecoder('avcodec.video.decoder.av1')
```

### Media Kit 增强

- **批量视频缩略图提取**：AVMetadataExtractor 新增 `fetchFramesByTimes` 接口，传入时间戳数组即可批量获取对应帧缩略图
- **HDR→SDR 转码**：支持将 HDR VIVID/HLG/HDR10 视频转换为 SDR 视频，以及 SDR 视频转码

```typescript
import { avMetadataExtractor } from '@kit.MediaKit'

let extractor = await avMetadataExtractor.createAVMetadataExtractor()
// API 23+: 批量获取指定时间戳的视频帧
let frames = await extractor.fetchFramesByTimes([1000, 5000, 10000])
```

### Audio Kit 增强

- **变声效果**：新增 C API，支持变声效果节点变声类型设置
- **系统音效管理**：新增系统音效管理和播放 API（`@ohos.multimedia.systemSoundManager`），提供管理系统声音的基础能力
- **音频路由时延**：AudioRenderer 新增 `getLatency` 接口，获取当前音频路由的预估时延
- **音量变化回调增强**：StreamVolumeEvent 新增"上一音量值"字段

```typescript
import { audio } from '@kit.AudioKit'

// API 23+: 获取音频路由时延
let audioRenderer = await audio.createAudioRenderer(renderInfo)
let latency = audioRenderer.getLatency()
```

---

## 官方参考

- AVPlayer 开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/avplayer-guidelines-V5
- AVSessionKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/local-avsession-V5
