---
name: harmonyos-master
description: |
  HarmonyOS 生态知识库总索引。整合华为 HarmonyOS 应用开发的完整技能体系。
  适用场景：开发 HarmonyOS 应用时，涉及 UI/框架、系统能力、媒体、AI、设计规范等任一领域。
---

# HarmonyOS 技能库

> **版本**：HarmonyOS 6.1.0 / API 23（稳定，2026-04-20）；HarmonyOS 6.0 / API 22（稳定，2026-01-21）
> **更新时间**：2026-04-25
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/

---

## 技能目录

| 技能 | 路径 | 覆盖内容 |
|------|------|---------|
| **开发规范** | `dev/SKILL.md` | Stage模型、ArkUI、ArkTS、权限、发布（HarmonyOS 6.1 API 23） |
| **系统能力** | `system/SKILL.md` | 蓝牙BLE/Wi-Fi/NFC/定位/传感器/电源/安全 |
| **媒体服务** | `media/SKILL.md` | CameraKit/AVPlayer/AVSession/PhotoAccessHelper |
| **AI与元服务** | `ai-meta/SKILL.md` | IntentsKit/SpeechKit/MLKit/元服务/服务流转 |
| **设计规范** | `design/SKILL.md` | 设计原则/色彩/字体/图标/布局/动效 |
| **示例代码** | `samples/SKILL.md` | 官方示例代码/Gitee仓/按Kit分类索引 |
| **模板组件** | `templates/SKILL.md` | DevEco Studio模板/生态市场模板/主题图标资源 |
| **AGC 服务** | `agc/SKILL.md` | 应用分发/云开发/认证/增长(推送/App Linking/应用内消息/素材管理)/质量(崩溃/性能/云测试/云调试)/变现 |

---

## HarmonyOS SDK 六大领域

HarmonyOS SDK 开放 API 总数 **50000+**，覆盖六大领域：

| 领域 | 覆盖 Kit | 核心能力 |
|------|---------|---------|
| 应用框架 | AbilityKit、ArkUI | Stage模型、UIAbility、ArkTS声明式UI |
| 系统 | ConnectivityKit、LocationKit、SensorServiceKit | 蓝牙Wi-FiNFC、定位、传感器 |
| 媒体 | CameraKit、AVSessionKit、MediaKit | 相机、音频、播控、相册 |
| 图形 | ArkGraphics 2D、@ohos.graphics.drawing | 2D绘制、Canvas、自定义渲染 |
| 应用服务 | PushKit、AVSessionKit、广告、分析等 | 推送、支付、增长变现 |
| AI | IntentsKit、SpeechKit、MLKit、VisionKit | 意图分发、语音、端侧AI |

---

## 版本历史

| HarmonyOS 版本 | API 版本 | DevEco Studio | 性质 | 发布日期 |
|---------------|---------|--------------|------|---------|
| **6.1.0** | **23** | **6.0.2（当前最新）** | **稳定（当前生产推荐）** | **2026.04.20** |
| 6.0.2 | 22 | 6.0.2 | 稳定 | 2026.01.21 |
| 6.0.0 | 22 | 6.0.0 | 稳定 | 2025.10.22 |
| 5.0.2 | 14 | 5.0.4 | 稳定 | 2025.01.15 |

> ⚠️ **生产环境推荐 API 23**（HarmonyOS 6.1.0 稳定版）。API 22 仍可用，但新项目建议使用 API 23。

---

## HarmonyOS 6.1 新增特性（API 23，Release 2026-04-20）

### UI 与设计
- **悬浮标签页 + 迷你栏**：HdsTabs 组件支持 `barFloatingStyle`，可配合 `miniBar` 实现可折叠快捷栏
- **沉浸光感视效**：HDS 组件支持 `systemMaterialEffect`，系统自动适配性能与显示效果
- **平行视界**：支持 `easy_go.json` 配置，应用在大屏/折叠屏首次冷启动自动分栏

### ArkUI 增强
- List/Grid 组件支持**长按聚拢动效**
- 自定义组件新增 **Attach/Detach** 生命周期阶段
- Navigation **分栏样式可定制**

### ArkTS 增强
- **模块持久化** + **模块懒加载**：优化冷启动性能
- **Local Handle/Global Handle**：跨语言内存泄漏检测（ArkTS ↔ C++）
- ArkTS 快照增强

### Kit 能力新增
- **Ability Kit**：新增启动时间戳能力，精准性能调优
- **Form Kit**：待机屏保卡片 + 透明卡片
- **ArkWeb**：画中画/字体预下载/同层渲染/首屏渲染时间统计
- **Media Kit**：20+ 媒体格式 + 边播边缓存 + 窗口级录屏 + 双屏录制
- **AR Engine**：3D 空间重建会话管理 + 营销组件 + 多 Kit 扩展 PC/2in1/TV
- **Scan Kit 直达服务**：扫码直接拉起应用特定页面
- **Service Collaboration Kit**：跨设备互通能力增强
- **Device Security Kit**：新增防窥保护（DLP Anti-Peep）

### FaceAR / BodyAR
- **FaceAR**：人脸跟踪 + 几何数据 + 微表情捕捉（虚拟主播/动态特效）
- **BodyAR**：人体骨骼关键点识别（健身/舞蹈/虚拟穿搭）

### DevEco Studio 工具链升级
- 预置模拟器（一键启动）
- AI 智能辅助编程增强（自定义 Agent / 提示词库）
- AppAnalyzer 上架合规体检
- 热重载支持 import * / 动态 import / lazy import
- Code Linter 命令行代码检查
- ArkUI Inspector 交互事件查看
- Pura X Max 机型模拟器 + 三折叠模拟器 + WearableKid 模拟器

---

## 快速查询

| 需要做什么 | 去哪个 skill |
|-----------|-------------|
| Stage/UIAbility/ArkUI 基础开发 | `dev/` |
| 蓝牙/Wi-Fi/NFC/定位开发 | `system/` |
| 相机/音视频/相册开发 | `media/` |
| 意图分发/语音合成/AI模型 | `ai-meta/` |
| 服务卡片/免安装应用 | `ai-meta/` |
| UI 设计/配色/字体/动效 | `design/SKILL.md` |
| 参考官方示例代码 | `samples/SKILL.md` |
| 新建工程选模板/找设计资源 | `templates/SKILL.md` |
| 应用发布/AppGallery 上架 | `dev/` |
| 权限申请/用户授权 | `dev/references/permissions.md` |
| 应用上架/审核/灰度发布 | `agc/SKILL.md` |
| AGC 云函数/云数据库/云存储/云托管 | `agc/references/cloud-development.md` |
| App Linking/应用内消息/素材管理 | `agc/references/growth.md` |
| 云测试/云调试/接入检测 | `agc/references/quality.md` |

---

## 文档中心链接

- **文档首页**：https://developer.huawei.com/consumer/cn/doc/
- **SDK 下载**：https://developer.huawei.com/consumer/cn/sdk/
- **示例代码**：https://developer.huawei.com/consumer/cn/samples/
- **模板市场**：https://developer.huawei.com/consumer/cn/market/prod-list?origin=template
- **设计频道**：https://developer.huawei.com/consumer/cn/design/
- **AppGallery Connect**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-overview-0000001100246618
- **AGC 应用分发**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-app-0000002235710234
