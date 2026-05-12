# 媒体开发示例（Media）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## 示例总览

| 示例场景 | Kit/模块 | 关键 API |
|---------|---------|---------|
| 相机预览+录像 | CameraKit | CameraManager/CameraOutputVideo |
| Video 长视频播放 | AVPlayer | prepare/play/pause/seek |
| Video 短视频播放 | AVPlayer | 循环播放/连播 |
| SoundPool 短音频 | AudioKit | SoundPool.load/play |
| 媒体会话控制 | AVSessionKit | AVSession.create/setAVMetadata |
| 相册图片选择 | PhotoAccessHelper | PhotoViewPicker |

---

## CameraKit 示例

### 相机预览+录像

```typescript
// 完整相机开发步骤
import { camera } from '@kit.CameraKit';
import { avRecorder } from '@kit.MediaKit';

// 1. 获取相机管理器
let cameraManager = camera.getCameraManager(getContext(this));

// 2. 获取支持的相机列表
let cameras = cameraManager.getSupportedCameras();

// 3. 创建预览输出流
let previewProfile = cameraManager.getSupportedPreviewProfile(cameras[0].cameraId);
let previewOutput = cameraManager.createPreviewOutput(previewProfile[0], surfaceId);

// 4. 创建录像输出流
let videoProfile = cameraManager.getSupportedVideoProfile(cameras[0].cameraId);
let videoOutput = cameraManager.createVideoOutput(videoProfile[0]);

// 5. 创建 Session 并添加输入输出
let session = cameraManager.createSession();
session.beginConfig();
session.addInput(cameras[0]);
session.addOutput(previewOutput);
session.addOutput(videoOutput);
session.commitConfig();
session.start();

// 6. 开始录像
videoOutput.start();

// 7. 停止录像
videoOutput.stop();
session.stop();
```

**Gitee 仓**：https://gitee.com/harmonyos_samples/camera-kit-avrecorder

---

## AVPlayer 示例

### 基础音频播放

```typescript
import avPlayer from '@kit.MediaKit';

// 创建播放器
let avPlayer = await avPlayer.createAVPlayer();

// 设置监听
avPlayer.on('playbackCompleted', () => {
  console.log('播放完成');
});

// 设置播放源（fd 或 url）
await avPlayer.setUrl(url);

// 播放控制
avPlayer.play();
avPlayer.pause();
avPlayer.seek(timeMs);
avPlayer.stop();
avPlayer.release();
```

### Video 组件播放

```typescript
// 布局
Video({
  src: 'https://example.com/video.mp4',
  currentProgressRate: PlaybackRate.Speed_Forward_1_00,
  controller: this.controller
})
  .width('100%')
  .height(300)
  .autoPlay(true)
  .muted(false)
  .onPrepared((event) => {
    console.info('视频准备完成，时长：' + event.duration);
  })
  .onFinish(() => {
    console.info('播放结束');
  })
```

---

## SoundPool 示例

```typescript
import soundPool from '@kit.AudioKit';

// 创建 SoundPool（短音频）
let soundPool = new soundPool.SoundPool({
  audioRendererInfo: {
    usage: 1, // STREAM_USAGE_MEDIA
    rendererFlags: 0
  }
});

// 加载音频
let soundId = soundPool.load('entry/resources/rawfile/click.mp3', 0, (err, id) => {
  console.info('加载完成，ID：' + id);
});

// 播放
soundPool.play(soundId, {});

// 停止
soundPool.stop(soundId);

// 释放
soundPool.release();
```

---

## 媒体会话（AVSessionKit）

```typescript
import { avSession } from '@kit.AVSessionKit';

// 创建会话
let session = await avSession.createAVSession(getContext(this), 'audio_test', 'audio');

// 设置元数据
session.setAVMetadata({
  title: '歌曲名称',
  artist: '歌手',
  album: '专辑',
  duration: 240000
});

// 设置播放状态
session.setAVPlaybackState({
  state: 0, // PLAYBACK_STATE_PLAY
  currentTime: 0,
  bufferedTime: 0
});

// 激活会话
session.activate();
```

---

## 相册访问（PhotoAccessHelper）

```typescript
import { photoAccessHelper } from '@kit.MediaLibraryKit';

// 创建图片选择器
let photoViewPicker = new photoAccessHelper.PhotoViewPicker();

// 选择图片
let result = await photoViewPicker.select({
  MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
  maxSelectNumber: 9
});

console.info('选择的图片：' + JSON.stringify(result.photoUris));
```

---

## 官方参考

- CameraKit 官方指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-session-management
- AVPlayer 官方指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/avplayer-guidelines-V5
- AVSessionKit 官方指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/local-avsession-V5
- 媒体会话示例仓：https://gitee.com/harmonyos_samples/camera-kit-avrecorder
