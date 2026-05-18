---
name: harmonyos-master
description: |
  HarmonyOS 生态知识库总索引。整合华为 HarmonyOS 应用开发的完整技能体系。
  适用场景：开发 HarmonyOS 应用时，涉及 UI/框架、系统能力、媒体、AI、设计规范等任一领域。
---

# HarmonyOS 技能库

> **版本**：HarmonyOS 6.1.1 / API 24（Beta1，2026-04-30）；HarmonyOS 6.1.0 / API 23（稳定，2026-04-20）
> **更新时间**：2026-05-18
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/

---

## 技能目录

| 技能 | 路径 | 覆盖内容 |
|------|------|---------|
| **开发规范** | `dev/SKILL.md` | Stage模型、ArkUI、ArkTS、权限、发布、NDK、行业实践、应用质量、最佳实践、FAQ |
| **系统能力** | `system/SKILL.md` | 蓝牙/Wi-Fi/NFC/定位/传感器/安全/车机/星闪/企业管理/穿戴/协同/测试/健康/天气 |
| **媒体服务** | `media/SKILL.md` | CameraKit/AVPlayer/AVSession/DRM/3D图形/铃声/编解码/2D绘制 |
| **AI与元服务** | `ai-meta/SKILL.md` | IntentsKit/SpeechKit/MLKit/基础AI/推理运行时/元服务/服务流转/智能体 |
| **设计规范** | `design/SKILL.md` | 设计原则/色彩/字体/图标/布局/动效/人机交互/UX最佳实践/控件/多设备 |
| **示例代码** | `samples/SKILL.md` | 官方示例代码/Gitee仓/按Kit分类索引 |
| **模板组件** | `templates/SKILL.md` | DevEco Studio模板/生态市场模板/主题图标资源 |
| **AGC 服务** | `agc/SKILL.md` | 应用分发/云开发/认证/增长/质量/变现/分析/游戏服务 |

---

## HarmonyOS SDK 六大领域

HarmonyOS SDK 开放 API 总数 **50000+**，覆盖六大领域：

| 领域 | 覆盖 Kit | 核心能力 |
|------|---------|---------|
| 应用框架 | AbilityKit、ArkUI、ArkData、ArkTS、ArkWeb、FormKit、AccessibilityKit、IMEKit、IPCKit、LocalizationKit、DataAugmentationKit、BackgroundTasksKit、CoreFileKit、PenKit、UIDesignKit、AccountKit、FileManagerServiceKit、DesktopExtensionKit | Stage模型、UIAbility、ArkTS声明式UI、数据管理、卡片、无障碍、输入法、IPC、国际化、数据增强、后台任务、文件管理、手写笔、华为账号、文件管理服务、桌面拓展 |
| 系统 | ConnectivityKit、LocationKit、SensorServiceKit、NetworkKit、AssetStoreKit、CarKit、FfrtKit、NearLinkKit、DriverDevelopmentKit、WearEngineKit、UniversalKeystoreKit、CryptoArchitectureKit、BasicServicesKit、DistributedKit、ServiceCollaborationKit、TestKit、EnterpriseThreatProtectionKit、FASTKit、HealthServiceKit、WeatherServiceKit、**InputKit**、**MultimodalAwarenessKit**、**MDMKit**、**DataLossPreventionKit**、**DeviceCertificateKit**、**OnlineAuthenticationKit**、**RemoteCommunicationKit**、**EnterpriseDataGuardKit**、**EnterpriseSpaceKit** | 蓝牙/Wi-Fi/NFC/星闪、定位、传感器、网络、安全存储、车机、并发调度、驱动开发、穿戴、加解密、分布式、协同、测试、企业威胁防护、算法加速、运动健康、天气、**多模输入**、**多模态融合感知**、**企业设备管理**、**数据防泄漏**、**设备证书**、**在线认证**、**远场通信**、**企业数据保护**、**企业数字空间** |
| 媒体 | CameraKit、MediaKit、AVSessionKit、AudioKit、AVCodecKit、DRMKit、RingtoneKit、ImageKit、MediaLibraryKit | 相机、音视频、播控、音频管理、编解码、版权保护、铃声、图片、相册 |
| 图形 | ArkGraphics 2D、ArkGraphics 3D、SpatialReconKit、GraphicsAccelerateKit、XEngineKit、AREngine | 2D/3D绘制、空间建模、图形加速、GPU引擎、AR |
| 应用服务 | PushKit、AccountKit、AdsKit、IAPKit、PaymentKit、WalletKit、AppGalleryKit、CalendarKit、ContactsKit、PreviewKit、ReaderKit、ScenarioFusionKit、CallServiceKit、LiveViewKit、LocationKit、MapKit、ScanKit、ShareKit、NotificationKit、TelephonyKit、HealthServiceKit、WeatherServiceKit、GameServiceKit、GameControllerKit、ScreenTimeGuardKit | 推送、账号、广告、支付、钱包、日历、联系人、预览、阅读、场景融合、通话、实况窗、地图、扫码、分享、通知、电话、健康、天气、游戏 |
| AI | IntentsKit、SpeechKit、MLKit、VisionKit、CoreSpeechKit、CoreVisionKit、NaturalLanguageKit、CANNKit、MindSporeLiteKit、NeuralNetworkRuntimeKit、AgentFrameworkKit、FASTKit、**ContentEmbedKit** | 意图分发、语音、端侧AI、视觉、基础语音/视觉/NLP、NPU加速、推理框架、智能体、**内容嵌入** |

---

## 版本历史

| HarmonyOS 版本 | API 版本 | DevEco Studio | 性质 | 发布日期 |
|---------------|---------|--------------|------|---------|
| **6.1.1** | **24** | **6.1.1 Beta1（6.1.1.268）** | **Beta（尝鲜）** | **2026.04.30** |
| **6.1.0** | **23** | **6.1.0 Release（6.1.0.830）** | **稳定（当前生产推荐）** | **2026.04.20** |
| 6.0.2 | 22 | 6.0.2 | 稳定 | 2026.01.21 |
| 6.0.1 | 21 | 6.0.1 | 稳定 | 2025.11.20 |
| 6.0.0 | 20 | 6.0.0 Release | 稳定 | 2025.09.25 |
| 5.1.1 | 19 | 5.1.1 | 稳定 | 2025.06.30 |
| 5.0.5 | 17 | 5.0.5 | 稳定 | 2025.05.14 |
| 5.0.4 | 16 | 5.0.4 | 稳定 | 2025.03.29 |
| 5.0.2 | 14 | 5.0.2 | 稳定 | 2025.01.27 |

> ⚠️ **生产环境推荐 API 23**（HarmonyOS 6.1.0 稳定版）。API 24 Beta1 适合尝鲜体验新特性。

---

## HarmonyOS 6.1.1 Beta1 新增特性（API 24，Release 2026-04-30）

### UI 与设计
- **平行视界状态获取**：应用可获取平行视界当前分栏状态
- **自定义组件跨 Ability 迁移**：支持组件状态跨应用迁移
- **动态布局容器**：新增动态布局容器能力

### ArkUI 增强
- 新增多个组件的 C API 支持
- List/Grid 组件长按聚拢动效增强

### ArkTS 增强
- **虚拟机维测能力增强**：提供更详细的运行时诊断信息
- **taskpool 任务超时设置**：支持为任务池设置超时时间

### ArkWeb 增强
- **下载任务回调增强**：更精细的下载进度控制
- **URL 白名单和安全控制接口**：增强网络安全能力

### Kit 能力新增
- **Camera Kit**：新增延迟预览输出和影随人动能力
- **Audio Kit**：新增 MIDI C API 支持外接设备
- **FAST Kit**：新增并发哈希表、向量运算和滤波器功能
- **Performance Analysis Kit**：增强资源采集和崩溃日志分析能力
- **Content Embed Kit**：**全新 Kit** — 内容嵌入服务

### DevEco Studio 工具链升级
- 支持开发 API 24 工程
- **Hot Reload 增强**：支持修改 C++ 代码和资源文件
- **AppFreeze 日志解析增强**：支持 Binder 通信信息、主线程任务队列和采样栈数据
- **ComMemory 模板**：分析 UI 界面各组件内存分配，定位内存泄漏问题

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
| 蓝牙/Wi-Fi/NFC/定位/星闪开发 | `system/` |
| 相机/音视频/相册/3D图形开发 | `media/` |
| 意图分发/语音合成/AI模型 | `ai-meta/` |
| 服务卡片/免安装应用 | `ai-meta/` |
| UI 设计/配色/字体/动效/人机交互 | `design/SKILL.md` |
| 参考官方示例代码 | `samples/SKILL.md` |
| 新建工程选模板/找设计资源 | `templates/SKILL.md` |
| 应用发布/AppGallery 上架 | `dev/` |
| 权限申请/用户授权 | `dev/references/permissions.md` |
| 应用上架/审核/灰度发布 | `agc/SKILL.md` |
| AGC 云函数/云数据库/云存储/云托管 | `agc/references/cloud-development.md` |
| App Linking/应用内消息/素材管理 | `agc/references/growth.md` |
| 云测试/云调试/接入检测 | `agc/references/quality.md` |
| 输入法/IPC/国际化/NDK | `dev/` |
| 数据增强/RAG/端侧问答 | `dev/references/data-augmentation-kit.md` |
| 车机/星闪/穿戴/驱动开发 | `system/` |
| 安全存储/DLP/用户认证 | `system/references/security-kits.md` |
| 企业管理/MDM/数据保护 | `system/references/enterprise-kits.md` |
| DRM版权保护/铃声设置 | `media/references/drm-ringtone-kit.md` |
| 3D图形/空间建模/GPU加速 | `media/references/arkgraphics-3d.md` |
| 基础AI/OCR/NLP/推理引擎 | `ai-meta/` |
| 应用质量/稳定性/功耗/安全隐私 | `dev/references/app-quality.md` |
| 行业实践/架构参考 | `dev/references/industry-practices.md` |
| 元服务设计/UX最佳实践 | `design/SKILL.md` |
| 分析服务/行业风向标 | `agc/references/analytics.md` |
| ArkTS语言/状态管理/并发 | `dev/references/arkts.md` |
| 文件基础服务/文件沙箱 | `dev/references/core-file-kit.md` |
| 华为账号/一键登录 | `dev/references/account-kit.md` |
| 文件管理服务/回收站 | `dev/references/file-manager-service-kit.md` |
| 最佳实践/架构设计 | `dev/references/best-practices.md` |
| 应用开发FAQ | `dev/references/app-faq.md` |
| ohpm-repo私仓 | `dev/references/deveco-service.md` |
| 协同服务/跨设备 | `system/references/service-collaboration-kit.md` |
| 应用测试/单元测试/UI测试 | `system/references/test-kit.md` |
| 企业威胁防护/杀毒 | `system/references/enterprise-threat-protection-kit.md` |
| 算法加速/数据结构 | `system/references/fast-kit.md` |
| 运动健康/步数心率 | `system/references/health-service-kit.md` |
| 天气服务/预报预警 | `system/references/weather-service-kit.md` |
| 控件设计规范 | `design/references/controls.md` |
| 多设备设计规范 | `design/references/multi-device-design.md` |
| 设计规范变更 | `design/references/design-changes.md` |

---

## API 24 Beta1 变更追踪（2026-04-30）

> API 24 Beta1 详细变更请参见上方「HarmonyOS 6.1.1 Beta1 新增特性」章节。

| 领域 | Kit | 变更 |
|------|-----|------|
| 应用框架 | Ability Kit | AbilityStage 上下文能力增强，支持动态加载资源 |
| 应用框架 | ArkUI | 平行视界状态获取、自定义组件跨 Ability 迁移、动态布局容器 |
| 应用框架 | ArkTS | 虚拟机维测能力增强、taskpool 任务超时设置 |
| 应用框架 | ArkWeb | 下载任务回调增强、URL 白名单和安全控制接口 |
| 开发工具 | DevEco Studio | Hot Reload 增强（支持 C++ 和资源文件）、AppFreeze 日志解析、ComMemory 模板 |
| 媒体 | Camera Kit | 延迟预览输出、影随人动能力 |
| 媒体 | Audio Kit | MIDI C API 支持外接设备 |
| AI | FAST Kit | 并发哈希表、向量运算和滤波器 |
| AI | Content Embed Kit | **全新 Kit** — 内容嵌入服务 |
| 系统 | Performance Analysis Kit | 资源采集和崩溃日志分析增强 |

---

## API 23 稳定版变更追踪（2026-04-20）

| 领域 | Kit | 变更 |
|------|-----|------|
| 应用框架 | Ability Kit | 新增启动时间戳能力 |
| 应用框架 | Form Kit | 待机屏保卡片、透明卡片 |
| 应用框架 | ArkWeb | 画中画、字体预下载、同层渲染、首屏渲染时间统计 |
| 媒体 | Media Kit | 20+ 媒体格式、边播边缓存、窗口级录屏、双屏录制 |
| 图形 | AR Engine | 3D 空间重建、营销组件、多 Kit 扩展 |
| 系统 | Scan Kit | 直达服务 |
| 系统 | Service Collaboration Kit | 跨设备互通增强 |
| 系统 | Device Security Kit | 防窥保护（DLP Anti-Peep） |
| AI | Agent Framework Kit | 智能体组合服务 |

---

## 文档中心链接

- **文档首页**：https://developer.huawei.com/consumer/cn/doc/
- **SDK 下载**：https://developer.huawei.com/consumer/cn/sdk/
- **示例代码**：https://developer.huawei.com/consumer/cn/samples/
- **模板市场**：https://developer.huawei.com/consumer/cn/market/prod-list?origin=template
- **设计频道**：https://developer.huawei.com/consumer/cn/design/
- **AppGallery Connect**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-overview-0000001100246618
- **AGC 应用分发**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-app-0000002235710234
