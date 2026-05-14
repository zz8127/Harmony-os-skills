# DRM Kit + Ringtone Kit

## DRM Kit — 数字版权保护服务

### 概述

DRM Kit（Digital Rights Management Kit）提供 DRM 加密节目授权解密功能，包括 DRM 插件管理、DRM 证书管理、DRM 许可证管理、DRM 节目授权、DRM 节目解密等，可实现 DRM 解决方案的集成、证书下载、节目授权及解密。

- npm 包名：`@kit.DRMKit`
- 模拟器：暂不支持

### 核心能力

| 能力 | 说明 |
|---|---|
| DRM 插件管理 | 通过实现 DRM HDI 接口，支持不同 DRM 解决方案的集成（由解决方案集成方实现） |
| DRM 证书管理 | 支持 DRM 解决方案的设备证书请求、处理及下载（Provision） |
| DRM 许可证管理 | 支持离线许可证的请求、处理及删除 |
| DRM 节目授权 | 支持在线许可证请求及处理、离线许可证加载、媒体密钥状态查询，按许可证权限要求对节目授权 |
| DRM 节目解密 | 支持 HLS/DASH 协议，MP4/TS 封装，H264/H265 视频编码，AAC 音频编码 |

### 关键 API

| API | 说明 |
|---|---|
| `mediaKeySystem` | DRM 证书管理及 MediaKeySession 管理 |
| `mediaKeySession` | 许可证管理及媒体节目解密，生命周期由 MediaKeySystem 管理 |
| `MediaKeySystemInfo` | DRM 节目加密描述信息，含解决方案 UUID 及 pssh 数据 |
| `keySystemRequired` 事件 | 无 DRM 证书或证书异常时触发，需调用证书下载接口 |
| `keyRequired` 事件 | 许可证需更新时触发，需重新请求许可证 |
| `keyExpired` 事件 | 许可证过期时触发，需停止节目播放 |

### 亮点特征

- 支持多 MediaKeySession 会话，许可证与解密会话绑定
- 支持安全视频通路（安全解密、安全解码、安全渲染、安全输出）

### 工作流程

1. 获取节目 DRM 信息，根据 UUID 创建 MediaKeySystem 及 MediaKeySession
2. 无证书或证书异常时，调用证书下载接口完成 Provision
3. 根据 pssh 数据调用许可证接口完成请求与处理
4. 将 MediaKeySession 设置到 Media Kit 或 AVCodec Kit 进行解密播放
5. 监听许可证更新/过期事件，动态处理

### 权限要求

无需特殊权限声明，但依赖对应 DRM 解决方案的实现。

### 官方链接

- [DRM Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/drm-overview)
- [数字版权保护 ArkTS 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/drm-arkts-dev-guide)
- [数字版权保护 C/C++ 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/drm-c-dev-guide)

---

## Ringtone Kit — 铃声服务

### 概述

Ringtone Kit 是用于设置铃声的工具库，开发者可在 HarmonyOS 应用中提供铃声设置功能，为用户提供简单一致、安全高品质的铃声设置体验。

- npm 包名：`@kit.RingtoneKit`
- 模拟器：支持

### 核心能力

| 能力 | 说明 |
|---|---|
| 多种铃声类型 | 可设置来电铃声、通知铃声、信息铃声、闹钟铃声 |
| 双卡铃声 | 可对双卡分别设置不同来电铃声和信息铃声 |
| 铃声快捷管理 | 点击"我的铃声"按钮快速跳转"设置-声音与振动"管理铃声 |

### 约束与限制

| 项目 | 说明 |
|---|---|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone、Tablet |
| 铃声最大时长 | 5 分钟 |
| 无 SIM 卡槽设备 | 来电铃声和信息铃声设置功能不可用 |

### 关键 API

| API | 说明 |
|---|---|
| 铃声设置组件 | 提供铃声设置 UI 组件，支持选择音频文件并设置为指定铃声类型 |
| 双卡铃声设置 | 支持对 SIM 卡 1/SIM 卡 2 分别设置来电铃声和信息铃声 |

### 权限要求

详情请参考官方文档。

### 官方链接

- [Ringtone Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ringtone-introduction)
- [设置铃声](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ringtone-preparations)
