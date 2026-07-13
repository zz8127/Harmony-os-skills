---
name: harmonyos-master
description: |
  HarmonyOS 生态知识库总索引。整合华为 HarmonyOS 应用开发的完整技能体系。
  适用场景：开发 HarmonyOS 应用时，涉及 UI/框架、系统能力、媒体、AI、设计规范等任一领域。
---

# HarmonyOS 技能库

> **版本**：HarmonyOS 26.0.0 / API 26（Beta1，2026-06-12）；HarmonyOS 6.1.1 / API 24（Release，2026-05-26；Patch 6.1.1.290，2026-06-30）
> **更新时间**：2026-07-13
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/

---

## 技能目录

| 技能 | 路径 | 覆盖内容 |
|------|------|---------|
| **开发规范** | `dev/SKILL.md` | Stage模型、ArkUI、ArkTS、权限、发布、NDK、行业实践、应用质量、最佳实践、FAQ |
| **系统能力** | `system/SKILL.md` | 蓝牙/Wi-Fi/NFC/定位/传感器/安全/车机/星闪/企业管理/穿戴/协同/测试/健康/天气 |
| **媒体服务** | `media/SKILL.md` | CameraKit/AVPlayer/AVSession/DRM/3D图形/铃声/编解码/2D绘制/ScanKit |
| **AI与元服务** | `ai-meta/SKILL.md` | IntentsKit/SpeechKit/VisionKit/基础AI/推理运行时/元服务/服务流转/智能体 |
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
| 系统 | ConnectivityKit、LocationKit、SensorServiceKit、NetworkKit、**NetworkBoostKit**、AssetStoreKit、CarKit、FfrtKit、NearLinkKit、DriverDevelopmentKit、WearEngineKit、UniversalKeystoreKit、CryptoArchitectureKit、BasicServicesKit、DistributedKit、ServiceCollaborationKit、TestKit、EnterpriseThreatProtectionKit、FASTKit、HealthServiceKit、WeatherServiceKit、**InputKit**、**MultimodalAwarenessKit**、**MDMKit**、**DataLossPreventionKit**、**DeviceCertificateKit**、**OnlineAuthenticationKit**、**RemoteCommunicationKit**、**EnterpriseDataGuardKit**、**EnterpriseSpaceKit**、**UserAuthenticationKit**、**PerformanceAnalysisKit**、**TelephonyKit** | 蓝牙/Wi-Fi/NFC/星闪、定位、传感器、网络、**网络加速**、安全存储、车机、并发调度、驱动开发、穿戴、加解密、分布式、协同、测试、企业威胁防护、算法加速、运动健康、天气、**多模输入**、**多模态融合感知**、**企业设备管理**、**数据防泄漏**、**设备证书**、**在线认证**、**远场通信**、**企业数据保护**、**企业数字空间**、**用户认证**、**性能分析**、**电话蜂窝** |
| 媒体 | CameraKit、MediaKit、AVSessionKit、AudioKit、AVCodecKit、DRMKit、RingtoneKit、ImageKit、MediaLibraryKit、**ScanKit** | 相机、音视频、播控、音频管理、编解码、版权保护、铃声、图片、相册、**统一扫码** |
| 图形 | ArkGraphics 2D、ArkGraphics 3D、SpatialReconKit、GraphicsAccelerateKit、XEngineKit、AREngine | 2D/3D绘制、空间建模、图形加速、GPU引擎、AR |
| 应用服务 | PushKit、AccountKit、AdsKit、IAPKit、PaymentKit、WalletKit、AppGalleryKit、**AppLinkingKit**、CalendarKit、ContactsKit、PreviewKit、ReaderKit、ScenarioFusionKit、CallServiceKit、LiveViewKit、LocationKit、MapKit、ShareKit、NotificationKit、**CloudFoundationKit**、**PDFKit**、HealthServiceKit、WeatherServiceKit、GameServiceKit、GameControllerKit、ScreenTimeGuardKit | 推送、账号、广告、支付、钱包、应用市场、**应用链接**、日历、联系人、预览、阅读、场景融合、通话、实况窗、地图、分享、通知、**云开发**、**PDF处理**、健康、天气、游戏 |
| AI | IntentsKit、SpeechKit、VisionKit、CoreSpeechKit、CoreVisionKit、NaturalLanguageKit、CANNKit、MindSporeLiteKit、NeuralNetworkRuntimeKit、AgentFrameworkKit、**ContentEmbedKit** | 意图分发、语音、视觉、基础语音/视觉/NLP、NPU加速、推理框架、智能体、**内容嵌入** |

---

## 版本历史

| HarmonyOS 版本 | API 版本 | DevEco Studio | 性质 | 发布日期 |
|---------------|---------|--------------|------|---------|
| **26.0.0** | **26** | **26.0.0 Beta1（26.0.0.461）** | **Beta** | **2026.06.12** |
| **6.1.1** | **24** | **6.1.1 Release（6.1.1.280）；Patch（6.1.1.290，2026.06.30）** | **Release（生产推荐）** | **2026.05.26** |
| **6.1.0** | **23** | **6.1.0 Release（6.1.0.830）** | **稳定** | **2026.04.20** |
| 6.0.2 | 22 | 6.0.2 Release | 稳定 | 2026.01.21 |
| 6.0.1 | 21 | 6.0.1 Release | 稳定 | 2025.11.20 |
| 6.0.0 | 20 | 6.0.0 Release | 稳定 | 2025.09.25 |
| 5.1.1 | 19 | 5.1.1 Release | 稳定 | 2025.06.30 |
| 5.0.5 | 17 | 5.0.5 Release | 稳定 | 2025.05.14 |
| 5.0.4 | 16 | 5.0.4 Release | 稳定 | 2025.03.29 |
| 5.0.2 | 14 | 5.0.2 Release | 稳定 | 2025.01.27 |

> ⚠️ **生产环境推荐 API 24**（HarmonyOS 6.1.1 Release）。API 26 为 Beta 版本，适合尝鲜体验新特性。

### 6.1.1 Patch 版本说明（2026-06-30）

DevEco Studio 6.1.1 Release 于 2026-06-30 发布 Patch 版本（6.1.1.290），API 版本号仍为 6.1.1(24)。Patch 版本主要修复 DevEco Studio 工具链问题，不涉及 API 能力新增。开发者可按需升级 DevEco Studio 至 Patch 版本以获得更稳定的开发体验。

---

## HarmonyOS 26.0.0 Beta1 新增特性（API 26，2026-06-12）

### 版本说明

26.0.0 Beta1 在 6.1.1(24) 的基础上进一步增强，本次发布对版本号格式进行了调整。ArkWeb 的 Chromium 内核从 132 升级为 144 版本。

### UI 与设计

- **系统材质效果增强**：所有支持通用属性的组件均支持 `systemMaterial` 属性，实现更好的沉浸光感效果
- **Chip 组件材质配置**：支持 `backgroundSystemMaterial` 和 `activatedBackgroundSystemMaterial` 配置
- **弹窗类组件材质效果**：Tips、Toast、对话框、操作菜单、自定义弹窗、半模态、Popup 均支持系统材质效果

### ArkUI 增强

- **组件级沉浸光感**：提供高品质视觉与动效体系
- **自定义组件全局复用**：支持配置复用池，提供全局复用能力
- **ContainerReader 容器断点组件**：基于容器尺寸而非窗口尺寸实现自适应布局
- **LazyVWaterFlowLayout 瀑布流**：懒加载垂直瀑布流布局容器，按需加载子组件
- **闪控窗**：窗口管理新增闪控窗能力，悬浮在桌面/应用界面上的小型窗口

### ArkWeb 增强

- **Chromium 内核升级**：从 132 升级为 144 版本
- **安全特性配置**：新增安全配置属性类

### Kit 能力新增

- **Accessory Kit【全新】**：配件接入服务，提供关联唤醒、系统服务联动、按需调度与安全授信管理
- **Ability Kit**：新增 AgentCard 支持、ArkTS 脚本应用 Skill 开发能力、ModularObjectExtensionAbility C API
- **Accessibility Kit**：新增关怀模式接入，提升长辈关怀功能及体验
- **Account Kit**：LoginWithHuaweiIDButton 支持文本多语言显示、自定义动效加载
- **Core File Kit**：支持沙箱目录共享为系统级可见、文件 mmap 能力、UNCACHE 参数、递归文件列表
- **Device Security Kit**：星盾机密风控引擎、统一风控凭证、超级隐私策略化管控、文件事件订阅与正则过滤
- **Graphics Accelerate Kit**：游戏预启动特性，提升启动体验；资源包下载能力查询
- **Notification Kit**：锁屏通知设置、半模态方式拉起通知设置界面
- **Online Authentication Kit**：新增 DID（去中心化身份）能力
- **FAST Kit**：实数快速傅里叶变换、智能序列预测
- **Core Vision Kit**：图像超分能力、文本语意搜索图片
- **Background Tasks Kit**：倒计时实例新增重复周期和重复次数参数
- **Data Augmentation Kit**：知识加工新增邮件智能分析模块（分类、摘要、待办抽取）
- **Driver Development Kit**：查询外接 USB Hub 并开发用户态驱动
- **Enterprise Data Guard Kit**：文件分级管控 getPolicy、isKia 接口
- **Enterprise Space Kit**：查询双空间状态、判断工作空间是否为企业空间
- **Input Kit**：输入事件注入模块，提供键盘和鼠标输入事件模拟能力
- **Nearlink Kit**：startScan 接口扫描周边星闪设备
- **Network Boost Kit**：setDataFlowDesc 接口，按五元组设置流描述
- **Performance Analysis Kit**：应用灰度采集、HiAppEvent 冻屏告警事件
- **Remote Communication Kit**：HTTP 版本选择、流式上传、有序表单、QUIC 客户端
- **Scan Kit**：查询设备是否支持默认/自定义界面扫码
- **Share Kit**：碰一碰分享获取轻碰位置信息（PC/2in1/Tablet）
- **AVCodec Kit**：H265 硬件编码器 CBRHQ、Audio Vivid 编码及 C API
- **Image Kit**：GIF/JFIF/TIFF/PNG/AVIS 图像元数据类、XMP 元数据
- **AR Engine**：闪光灯控制、预览流图片数据、3D 高斯模型加载、外部相机传感器
- **Spatial Recon Kit**：3DGS 高斯球编辑、空间照片能力
- **Game Service Kit**：近场快传免集成实现安装包传输
- **Live View Kit**：实况窗卡片辅助区模板，支持百分比进度环
- **PDF Kit**：多张页面指定区域转化为一张图片
- **Preview Kit**：文件加速 C API（扫描、预加载策略、可用性查询）
- **Push Kit**：推送实况窗消息支持 Wearable 设备
- **Scenario Fusion Kit**：场景化分享 Button 支持图片、视频、文本
- **UI Design Kit**：标题顶部/底部自定义区域更新节点配置
- **NDK**：JSVM 支持从外部内存创建 ArrayBuffer 对象

### DevEco Studio 工具链升级

- 支持开发 API 26.0.0 工程
- 按需加载模块，提升代码索引效率
- 新增 Code Scanner 工具，检查资源泄漏
- 支持同时预览 8 个档位断点的 UI 效果
- 新增 Car 设备模拟器
- 支持设备投屏到 DevEco Studio
- 支持解析应用崩溃 dump 文件

---

## HarmonyOS 6.1.1 Release 新增特性（API 24，Release 2026-05-26）

### API 24 Release 新增特性（Beta1 后新增）

#### Ability Kit
- **AbilityStage 生命周期增强**：新增 `onAboutToCreateAbility` 回调（首个 Ability 创建前）和 `onLaunchFromHypersnap` 回调（进程从应用快照启动时）

#### ArkTS
- **Local Handle 检测**：`enableLocalHandleDetection` 接口保证 EventHandler 和 libuv 任务在 scope 范围内执行，避免跨语言内存泄漏
- **XML 解析增强**：新增 `XmlSAXHandler`，支持 SAX 方式解析 XML

#### ArkWeb
- **下载任务回调增强**：新增 `getOriginalUrl` 和 `getReferrerUrl` 接口

#### Call Service Kit
- **企业服务信息查询**：企业员工来电/去电时，可通过手机号查询企业服务信息（目前支持快递类型）

#### Camera Kit
- **闪光灯状态订阅**：支持订阅/取消订阅闪光灯状态变化事件
- **OIS 光学防抖**：支持查询和设置 OIS 模式、轴向偏移量
- **手动曝光/对焦/ISO/光圈**：完整的手动拍摄专业能力
- **逻辑摄像头管理**：支持通过 `isLogicalCamera` 查询逻辑摄像头，通过 `constituentCameraDevices` 获取物理摄像头列表

#### CANN Kit
- **PC 大语言模型推理**：针对 PC 设备开放大语言模型推理 API，支持计算链路加速封装

#### MDM Kit
- **隐藏设置项管理**：支持对当前用户下被隐藏的设置项列表进行添加、删除、查询操作

### API 24 Beta1 新增特性（已包含在 Release 中）

#### UI 与设计
- **平行视界状态获取**：应用可获取平行视界当前分栏状态
- **自定义组件跨 Ability 迁移**：支持组件状态跨应用迁移
- **动态布局容器**：新增动态布局容器能力

#### ArkUI 增强
- 新增多个组件的 C API 支持
- List/Grid 组件长按聚拢动效增强

#### ArkTS 增强
- **虚拟机维测能力增强**：提供更详细的运行时诊断信息
- **taskpool 任务超时设置**：支持为任务池设置超时时间

#### ArkWeb 增强
- **下载任务回调增强**：更精细的下载进度控制
- **URL 白名单和安全控制接口**：增强网络安全能力

#### Kit 能力新增
- **Camera Kit**：新增延迟预览输出和影随人动能力
- **Audio Kit**：新增 MIDI C API 支持外接设备
- **FAST Kit**：新增并发哈希表、向量运算和滤波器功能
- **Performance Analysis Kit**：增强资源采集和崩溃日志分析能力
- **Content Embed Kit**：**全新 Kit** — 内容嵌入服务

#### DevEco Studio 工具链升级
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
| PDF文件处理/批注/水印 | `dev/references/pdf-kit.md` |
| 扫码/码识别/直达服务 | `system/references/scan-kit.md` |
| 电话/蜂窝通信 | `system/references/telephony-kit.md` |
| 网络加速/远场通信 | `system/references/network-boost-remote-kit.md` |
| 性能分析/事件跟踪/日志 | `dev/references/performance-analysis-kit.md` |
| 云开发/云函数/云数据库 | `agc/references/cloud-development.md` |
| 应用链接/延迟链接 | `agc/references/growth.md` |

---

## API 26 Beta1 变更追踪（2026-06-12）

> API 26 Beta1 详细变更请参见上方「HarmonyOS 26.0.0 Beta1 新增特性」章节。

| 领域 | Kit | 变更 |
|------|-----|------|
| 应用框架 | Ability Kit | 新增 AgentCard、ArkTS 脚本应用 Skill 开发、脚本管理 API、ModularObjectExtensionAbility C API |
| 应用框架 | Accessibility Kit | 新增关怀模式接入，提升长辈关怀功能及体验 |
| 应用框架 | Account Kit | LoginWithHuaweiIDButton 支持文本多语言显示、自定义动效加载 |
| 应用框架 | ArkUI | systemMaterial 属性、组件级沉浸光感、全局复用、闪控窗、ContainerReader 容器断点组件、LazyVWaterFlowLayout 瀑布流 |
| 应用框架 | ArkWeb | Chromium 内核 132→144、安全特性配置 |
| 应用框架 | Background Tasks Kit | 倒计时实例新增重复周期（repeatInterval）和重复次数（repeatCount） |
| 应用框架 | Core File Kit | 沙箱目录共享、mmap 能力、UNCACHE 参数、递归文件列表 |
| 应用框架 | Data Augmentation Kit | 知识加工新增邮件智能分析模块（分类、摘要、待办抽取） |
| 应用框架 | NDK | JSVM 支持从外部内存创建 ArrayBuffer 对象 |
| 应用框架 | UI Design Kit | 标题顶部/底部自定义区域更新节点配置 |
| 系统 | Accessory Kit | **全新 Kit** — 配件接入服务 |
| 系统 | Device Security Kit | 星盾机密风控引擎、统一风控凭证、超级隐私管控、文件事件订阅、文件路径正则过滤 |
| 系统 | Driver Development Kit | 查询外接 USB Hub 并开发用户态驱动 |
| 系统 | Enterprise Data Guard Kit | 文件分级管控 getPolicy、isKia 接口 |
| 系统 | Enterprise Space Kit | 查询双空间状态、判断工作空间是否为企业空间 |
| 系统 | Graphics Accelerate Kit | 游戏预启动特性、资源包下载支持、isSupportAssetDownload 查询 |
| 系统 | Input Kit | 输入事件注入模块（键盘和鼠标事件模拟） |
| 系统 | Nearlink Kit | startScan 接口扫描周边星闪设备 |
| 系统 | Network Boost Kit | setDataFlowDesc 接口（五元组流描述） |
| 系统 | Notification Kit | 锁屏通知设置、半模态通知设置界面 |
| 系统 | Online Authentication Kit | DID（去中心化身份）能力 |
| 系统 | Performance Analysis Kit | 应用灰度采集、HiAppEvent 冻屏告警事件 |
| 系统 | Remote Communication Kit | HTTP 版本选择、流式上传、有序表单、QUIC 客户端 |
| 系统 | Scan Kit | 查询设备是否支持默认/自定义界面扫码 |
| 系统 | Share Kit | 碰一碰分享获取轻碰位置信息（PC/2in1/Tablet） |
| 媒体 | AVCodec Kit | H265 硬件编码器 CBRHQ、Audio Vivid 编码及 C API |
| 媒体 | AVSession Kit | 新增不同场景额外键的枚举 |
| 媒体 | Image Kit | GIF/JFIF/TIFF/PNG/AVIS 图像元数据类、XMP 元数据 |
| 图形 | AR Engine | 闪光灯控制、预览流图片数据、3D 高斯模型加载、外部相机传感器 |
| 图形 | ArkGraphics 2D | 坐标点处理类（取反、偏移量设置） |
| 图形 | Spatial Recon Kit | 3DGS 高斯球编辑（选择/变换/上色/删除）、空间照片能力 |
| 应用服务 | Game Service Kit | 近场快传免集成 Game Service Kit 实现安装包传输 |
| 应用服务 | Live View Kit | 实况窗卡片辅助区模板（百分比进度环） |
| 应用服务 | PDF Kit | 多张页面指定区域转化为一张图片 |
| 应用服务 | Preview Kit | 文件加速 C API（扫描、预加载策略、可用性查询、事件上报） |
| 应用服务 | Push Kit | 推送实况窗消息支持 Wearable 设备 |
| 应用服务 | Scenario Fusion Kit | 场景化分享 Button 支持图片、视频、文本 |
| AI | FAST Kit | 实数 FFT、智能序列预测 |
| AI | Core Vision Kit | 图像超分、文本语意搜索图片 |

---

## API 24 Release 变更追踪（2026-05-26）

> API 24 Release 详细变更请参见上方「HarmonyOS 6.1.1 Release 新增特性」章节。

### Release 新增（Beta1 后新增）

| 领域 | Kit | 变更 |
|------|-----|------|
| 应用框架 | Ability Kit | AbilityStage 新增 `onAboutToCreateAbility` 和 `onLaunchFromHypersnap` 回调 |
| 应用框架 | ArkTS | `enableLocalHandleDetection` 接口、XmlSAXHandler |
| 应用框架 | ArkWeb | 下载任务 `getOriginalUrl` 和 `getReferrerUrl` |
| 应用服务 | Call Service Kit | 企业服务信息查询（快递类型） |
| 媒体 | Camera Kit | 闪光灯状态订阅、OIS 光学防抖、手动曝光/对焦/ISO/光圈、逻辑摄像头管理 |
| AI | CANN Kit | PC 设备大语言模型推理 API |
| 系统 | MDM Kit | 隐藏设置项管理 |

### Beta1 变更（已包含在 Release 中）

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
