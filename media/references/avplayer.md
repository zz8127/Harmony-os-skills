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

## 官方参考

- AVPlayer 开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/avplayer-guidelines-V5
- AVSessionKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/local-avsession-V5
