# 媒体服务

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

HarmonyOS 媒体服务覆盖相机、音视频播放/录制、音频管理、媒体库访问等能力。

| 能力 | Kit | 说明 |
|------|-----|------|
| 相机 | CameraKit | 预览/拍照/录像/元数据 |
| 音视频播放 | AVPlayer / AVRecorder | 媒体播放与录制 |
| 音视频播控 | AVSessionKit | 媒体会话管理（控制中心显示） |
| 音频管理 | AudioKit | 音量管理/音频流/焦点管理 |
| 相册 | PhotoAccessHelper | 图片/视频访问与编辑 |
| 媒体元数据 | MediaMetadataExtractor | 音视频文件元数据读取 |

---

## 相机开发（CameraKit）

### 相机开发流程

```
1. 创建 CameraManager（相机管理器）
2. 创建相机会话（PhotoSession / VideoSession）
3. 配置输入流（选择镜头）+ 输出流（预览/拍照/录像）
4. 提交会话，开始预览/拍摄
```

### 核心 API

```typescript
import { camera } from '@kit.CameraKit';
import { BusinessError } from '@kit.BasicServicesKit';

// 1. 获取相机管理器
let cameraManager: camera.CameraManager = camera.getCameraManager(context);

// 2. 获取相机列表
let cameraArray: camera.CameraOutputCapability = cameraManager.getSupportedCameras();

// 3. 创建相机会话
let photoSession: camera.PhotoSession = cameraManager.createPhotoSession();

// 4. 配置预览流（XComponent）
// ...

// 5. 提交会话
photoSession.start();
```

### CameraPicker（系统相机拉起）

无需申请相机权限，直接拉起系统相机拍照/录像：

```typescript
import { cameraPicker } from '@kit.CameraKit';

let pickerResult = await cameraPicker.pick(
  getContext(this) as common.UIAbilityContext,
  [cameraPicker.PickType.PHOTO],
  new cameraPicker.PickOptions()
);
```

### 相机权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.CAMERA` | 相机访问 |
| `ohos.permission.MICROPHONE` | 麦克风（录像时） |

---

## 音视频播放（AVPlayer）

### AVPlayer 音频播放

```typescript
import { avPlayer } from '@kit.MediaKit';

let avPlayer: avPlayer.AVPlayer = await avPlayer.createAVPlayer();
avPlayer.url = 'https://example.com/audio.mp3';
avPlayer.prepare();
avPlayer.play();
```

### AVSessionKit（媒体会话）

媒体会话用于在系统控制中心显示播放状态，支持耳机、智慧屏等设备控制：

```typescript
// 创建本地媒体会话
import { avSession } from '@kit.AVSessionKit';

let session = await avSession.createAVSession(context, 'audio', 'audio');
session.setAVPlayer({ url: 'https://example.com/audio.mp3' });
```

---

## 相册访问（PhotoAccessHelper）

```typescript
import { photoAccessHelper } from '@kit.MediaLibraryKit';

let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

// 请求用户授权
let permissions = ['ohos.permission.READ_MEDIA_IMAGES'];
let result = await requestUserGrant(permissions);

// 查询图片
let fetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: ['uri', 'display_name'],
  predicates: {
    uriPrefix: ''
  }
};
let fetchResult = await phAccessHelper.getAssets(fetchOptions);
```

### 相册权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.READ_MEDIA_IMAGES` | 读取图片 |
| `ohos.permission.READ_MEDIA_VIDEO` | 读取视频 |
| `ohos.permission.WRITE_MEDIA_IMAGES` | 写入图片 |
