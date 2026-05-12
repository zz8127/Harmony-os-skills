# 媒体会话（AVSessionKit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

AVSessionKit 用于将音视频播控能力接入系统控制中心，使用户能在锁屏、控制中心、耳机等设备上控制应用播放。

## 创建本地媒体会话

```typescript
import { avSession } from '@kit.AVSessionKit';

let session: avSession.AVSession = await avSession.createAVSession(
  getContext(this),
  'audio_test',
  'audio',
  'playback'
);

// 设置元数据
session.setAVMetadata({
  title: '歌曲名称',
  artist: '歌手',
  album: '专辑',
  duration: 240000
});

// 设置播放状态
session.setAVPlaybackState({
  state: avSession.PlaybackState.PLAYBACK_STATE_PLAY,
  position: { currentTime: 30000, duration: 240000 }
});
```

## 订阅远端播控命令

```typescript
// 订阅来自系统控制中心的命令
session.on('play', () => {
  avPlayer.play();
});

session.on('pause', () => {
  avPlayer.pause();
});

session.on('seek', (time: number) => {
  avPlayer.seek(time);
});
```

## 官方参考

- 本地媒体会话：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/local-avsession-V5
