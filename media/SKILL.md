---
name: harmonyos-media
description: |
  HarmonyOS 媒体服务开发规范。涉及相机、音视频播放录制、音频管理、媒体库访问。
  触发场景：开发拍照、录像、音频播放、媒体库访问等媒体能力时。
  包含：CameraKit（相机）、AVPlayer/AVRecorder（播放录制）、AVSessionKit（媒体会话）、AudioKit（音频管理）、PhotoAccessHelper（相册）。
---

# HarmonyOS 媒体服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 快速导航

| 能力 | 说明 |
|------|------|
| [相机开发](references/camera.md) | CameraKit：预览/拍照/录像/XComponent |
| [音视频播放](references/avplayer.md) | AVPlayer：音频/视频播放控制 |
| [媒体会话](references/avsession.md) | AVSessionKit：控制中心显示与控制 |
| [音频管理](references/audio-kit.md) | AudioKit：音量/音频流/焦点管理/变声效果/系统音效 |
| [编解码](references/avcodec-kit.md) | AVCodec Kit：音视频编解码/AV1/VP9软解/API 23新增 |
| [相册访问](references/photo.md) | PhotoAccessHelper：图片/视频读写 |
| [图形开发](references/graphics2d.md) | ArkGraphics 2D：Canvas/自定义绘图/模糊效果 |
| [DRM+铃声](references/drm-ringtone-kit.md) | DRM Kit：数字版权保护 + Ringtone Kit：铃声设置 |
| [3D图形](references/arkgraphics-3d.md) | ArkGraphics 3D + SpatialRecon + GraphicsAccelerate + XEngine |

---

## 媒体 Kit 总览

| Kit | npm 包 | 用途 |
|-----|-------|------|
| CameraKit | `@kit.CameraKit` | 相机预览、拍照、录像 |
| MediaKit | `@kit.MediaKit` | AVPlayer、AVRecorder |
| AVSessionKit | `@kit.AVSessionKit` | 媒体会话（播控中心） |
| AudioKit | `@kit.AudioKit` | 音量、音频流管理 |
| MediaLibraryKit | `@kit.MediaLibraryKit` | 相册访问 |
| ArkGraphics2D | `@kit.ArkGraphics2D` | Canvas 绘图、模糊效果、动态帧率 |
| ImageKit | `@kit.ImageKit` | 图片处理、元数据读写 |
| AVCodecKit | `@kit.AVCodecKit` | 音视频编解码（AV1/VP9软解） |
| DRMKit | `@kit.DRMKit` | 数字版权保护 |
| RingtoneKit | `@kit.RingtoneKit` | 铃声设置 |
| ArkGraphics3D | `@kit.ArkGraphics3D` | 3D场景绘制、模型加载 |
| SpatialReconKit | `@kit.SpatialReconKit` | 3D空间建模 |
| GraphicsAccelerateKit | `@kit.GraphicsAccelerateKit` | 图形加速、超帧 |
| XEngineKit | `@kit.XEngineKit` | GPU加速引擎 |

---

## 常见权限

| 权限 | 场景 |
|------|------|
| `ohos.permission.CAMERA` | 相机 |
| `ohos.permission.MICROPHONE` | 录音 |
| `ohos.permission.READ_MEDIA_IMAGES` | 读图片 |
| `ohos.permission.READ_MEDIA_VIDEO` | 读视频 |
| `ohos.permission.WRITE_MEDIA_IMAGES` | 写图片 |

---

## HarmonyOS 6.1 Media Kit 全面升级（API 23）

| 新增能力 | 说明 |
|---------|------|
| 20+ 媒体格式 | 新增支持 20 余种媒体格式 |
| 边播边缓存 | 系统级流媒体缓存与起播控制，开发者无需自行实现 |
| 窗口级录屏 | 安全隐私自主可控，支持选择全屏/窗口/应用级 |
| 多屏自适应 | 大幅降低多屏设备适配成本 |
| 双屏录制 | 支持折叠屏等双屏设备同时录制 |

---

## API 24 Beta1 变更追踪（2026-04-30）

| Kit | 变更 |
|-----|------|
| Camera Kit | 延迟预览输出、影随人动能力 |
| Audio Kit | MIDI C API 支持外接设备 |

---

## 官方参考

- CameraKit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/camera-overview-V5
- 会话管理：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/camera-session-management
- 本地媒体会话：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/local-avsession-V5
- ArkGraphics 2D 图形：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics-2d
