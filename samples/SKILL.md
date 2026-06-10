---
name: harmonyos-samples
description: |
  HarmonyOS 官方示例代码库技能。收录华为官方示例代码的分类索引、代码仓地址和使用指导。
  触发场景：需要参考官方示例代码来学习某个 Kit 或功能如何实现时；需要找到某个场景的完整示例工程时。
  包含：示例代码总览、Gitee 仓列表、按类别索引、使用说明。
---

# HarmonyOS 官方示例代码

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。
> **示例代码首页**：https://developer.huawei.com/consumer/cn/samples/
> **Gitee 官方组织**：https://gitee.com/HarmonyOS_Samples

## 相关技能

| 关联 skill | 路径 | 说明 |
|-----------|------|------|
| 总索引 | `../SKILL.md` | HarmonyOS 全技能入口 |
| 开发规范 | `../dev/SKILL.md` | Stage模型/ArkUI/ArkTS 开发规范 |
| 系统能力 | `../system/SKILL.md` | 蓝牙/Wi-Fi/传感器等系统 Kit |
| 媒体服务 | `../media/SKILL.md` | 相机/音视频/相册 Kit |
| AI与元服务 | `../ai-meta/SKILL.md` | 意图/语音/MLKit |

---

## 快速导航

| 类别 | 说明 |
|------|------|
| [应用框架](references/app-framework.md) | Stage模型、UIAbility、流转、多实例 |
| [媒体开发](references/media.md) | CameraKit、AVPlayer、AVSession、PhotoAccessHelper |
| [系统能力](references/system.md) | 蓝牙BLE、Wi-Fi、NFC、定位、传感器 |
| [图形开发](references/graphics.md) | ArkGraphics 2D、Canvas、绘图、自定义渲染 |
| [网络开发](references/network.md) | HTTP、RCP、WebSocket、网络状态 |
| [AI功能](references/ai.md) | VisionKit、MLKit、语音合成/识别 |
| [应用服务](references/app-service.md) | 推送、支付、AppGallery Connect |
| [工具与测试](references/tool-test.md) | DevEco Studio 工具、异常处理、单元测试 |

---

## Gitee 官方示例仓

官方示例代码统一托管在 Gitee HarmonyOS_Samples 组织下：

| 仓名 | 用途 | 地址 |
|------|------|------|
| 官方示例合集 | 全部示例索引 | https://gitee.com/HarmonyOS_Samples |
| CameraKitAVRecorder | 相机预览+录像 | https://gitee.com/harmonyos_samples/camera-kit-avrecorder |
| NativeSoIntegration | Native .so 库集成 | https://gitee.com/harmonyos_samples/NativeSoIntegration |
| CoreVisionKit-SampleCode | 多目标识别/图像分析 | https://gitee.com/HarmonyOS_Samples/CoreVisionKit-SampleCode-ArkTS-ObjectDetectDemo |
| IFAAClientdemo | 在线认证（IFAA） | https://gitee.com/heshengbang/OnlineAuthenticationkit-sample-IFAAClientdemo-ArkTS |
| 网络编程示例 | HTTP/TCP/UDP/TLS/WebSocket | https://gitee.com/harmonyos4me/harmonyos_network_samples |

> **注意**：部分示例需要从 AppGallery Connect 下载 `agconnect-services.json` 并放入工程 `entry/` 根目录，同时修改 `module.json5` 中的 `bundleName` 为自己应用的包名。

---

## 示例页面分类体系

华为官方示例页面按技术领域分为以下大类：

| 大类 | 子类示例 | 说明 |
|------|---------|------|
| **技术质量** | 应用异常处理（hiAppEvent） | 崩溃/卡死信息获取 |
| **应用框架开发** | UIAbility 生命周期、流转、多实例 | Stage 模型核心 |
| **系统开发** | 蓝牙BLE扫描、Wi-Fi连接、NFC、定位 | ConnectivityKit 等 |
| **媒体开发** | CameraKit、AVPlayer、SoundPool | 相机/视频/音频 |
| **图形开发** | ArkGraphics 2D、Canvas 2D、自定义渲染 | 绘图/粒子 |
| **应用服务开发** | 推送服务、支付、AGC | PushKit/支付Kit |
| **AI功能开发** | 端侧AI推理、语音合成、意图框架 | MLKit/IntentsKit |
| **应用专项测试** | 单元测试、UI 测试 | hvigor / @ohos/hypium（Hypium单元测试框架） |
| **开发工具** | DevEco Studio 技巧、异常日志 | IDE 使用 |

---

## 如何使用官方示例

1. **找示例**：在示例页面按类别浏览，或在 Gitee 搜索 `harmonyos_samples`
2. **下载代码**：克隆对应 Git 仓，或在示例页面点击"下载"
3. **导入 DevEco Studio**：`File → Open →` 选择工程根目录
4. **配置签名**：Project Structure → Signing Configs → 配置 AGC 证书
5. **运行验证**：连接设备或启动模拟器，运行确认效果
6. **参考 README**：每个示例工程内的 README.md 有详细使用说明

---

## API 24 Release 变更追踪（2026-05-26）

> HarmonyOS 6.1.1(24) Release 已发布，示例代码暂无重大变更。持续关注官方更新。

---

## 注意事项

- 部分早期示例使用 Java/JS 语言，已不推荐；**优先参考 ArkTS 示例**
- 示例 API 版本可能低于当前，建议使用 DevEco Studio 6.1.0（API 23）配套
- 网络类示例需要声明 `ohos.permission.INTERNET` 权限
- 涉及用户隐私的示例（如位置、相机）需要配置相应 user_grant 权限
