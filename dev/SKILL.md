---
name: harmonyos-development
description: |
  HarmonyOS 6.1 应用开发规范与指南，基于 API 23（稳定）。用于鸿蒙应用/元服务开发时参考华为官方规范。
  触发场景：开发HarmonyOS应用/元服务时，需要了解ArkTS、Stage模型、ArkUI、权限配置、打包上架等。
  包含：开发准备、应用框架(Stage模型)、UI开发(ArkUI/ArkTS)、一次开发多端部署、权限与安全、打包签名上架等。
---

# HarmonyOS 6 应用开发规范

> **版本说明**：本文档基于 **HarmonyOS 6.1**（API 23 稳定）编写，兼容 API 14+。
> HarmonyOS 6 于 2025年10月22日 HDC2025 正式发布（首批消费者版本基于 API 22）。
> 2026年1月21日发布稳定版 API 22（DevEco Studio 6.0.2）；2026年4月20日 HarmonyOS 6.1 正式发布（API 23 稳定）。
> 历史版本：HarmonyOS 5.x = API 12/13/14/16。

## 扩展技能（独立 Skill）

以下专题已拆分为独立 skill，如需深入开发请查阅：

| 扩展专题 | 路径 | 说明 |
|---------|------|------|
| 系统能力 | `../system/SKILL.md` | 蓝牙/Wi-Fi/NFC/定位/传感器/电源/安全 |
| 媒体服务 | `../media/SKILL.md` | 相机/音视频/AVSession/相册访问 |
| AI与元服务 | `../ai-meta/SKILL.md` | 意图框架/语音/MLKit/元服务/服务流转 |
| 设计规范 | `../design/SKILL.md` | 色彩/字体/图标/布局/动效设计 |

---

## 快速导航

- [开发准备](references/dev-preparation.md) — 环境搭建、工程创建、签名配置
- [应用框架](references/app-framework.md) — Stage模型、UIAbility、module.json5
- [UI开发](references/ui-development.md) — ArkUI声明式开发、ArkTS语法、组件、布局
- [一次开发多端部署](references/multi-device.md) — 响应式布局、断点、栅格、工程组织
- [权限与安全](references/permissions.md) — 权限声明、user_grant、system_grant、APL等级
- [打包上架](references/publish.md) — 签名配置、App Pack打包、AGC上架流程
- [数据持久化](references/arkdata.md) — ArkData：RDB/Preferences/分布式数据/UDMF
- [通知服务](references/notification.md) — Notification Kit：本地通知/通知渠道/WantAgent
- [应用测试](references/testing.md) — Hypium框架：单元测试/UI测试/专项测试
- [Web开发](references/arkweb.md) — ArkWeb：WebView/JSBridge/安全控制
- [应用架构与质量](references/architecture.md) — 分层架构/模块化/性能优化/安全编码
- [其他参考](references/other.md) — 网络请求、数据存储、生命周期、常见问题
- [PDF阅读](references/pdf-kit.md) — PDF Kit：PDF页面视图/文本获取/缩放
- [实况窗](references/live-view-kit.md) — Live View Kit：地理围栏触发实况窗/API 23新增
- [UI组件库](references/ui-design-kit.md) — UI Design Kit：官方UI组件库/底部页签/导航/材质效果
- [卡片开发](references/form-kit.md) — Form Kit：ArkTS卡片/V2装饰器/待机屏保卡片/透明卡片
- [手写笔](references/pen-kit.md) — Pen Kit：画布绘制/长画布滚动/API 23新增
- [无障碍](references/accessibility-kit.md) — Accessibility Kit：屏幕朗读/无障碍扩展/分组聚合播报
- [性能分析](references/performance-analysis-kit.md) — Performance Analysis Kit：HiAppEvent/HiDebug/AppFreeze

---

## 版本与API对照

| HarmonyOS版本 | API Level | DevEco Studio | 状态 | 发布时间 |
|-------------|-----------|-------------|------|---------|
| 5.0.0 | 12 | — | 稳定 | 2024 |
| 5.0.1 | 13 | — | 稳定 | 2024 |
| 5.0.2 | 14 | — | 稳定 | 2025.01 |
| 5.0.4 | 16 | 5.0.4 Release | 稳定 | 2025.03.27 |
| **6.0.2** | **22** | **6.0.2 Release** | **稳定** | **2026.01.21** |
| **6.1.0** | **23** | **6.1.0 Release（6.1.0.830）** | **稳定（当前生产推荐）** | **2026.04.20** |
| **6.1.1** | **24** | **6.1.1 Beta1** | **Beta（按需使用）** | **2026.04.30** |

> ⚠️ **生产环境推荐 API 23**（HarmonyOS 6.1.0 稳定版）。API 22 仍可用，但新项目建议使用 API 23。

---

## 核心概念速查

### Stage模型 vs FA模型

| 对比项 | Stage模型 | FA模型 |
|--------|-----------|--------|
| 主推版本 | API 9+（当前） | API 8及更早（已废弃） |
| 配置文件 | app.json5 + module.json5 | config.json |
| 语言 | ArkTS | JS/Java |
| 模块化 | 支持HAP/HAR/HSP分包 | 不支持 |

**结论：新项目一律使用Stage模型。**

### 应用包结构

```
Bundle（应用包）
├── Entry HAP（主模块，type=entry）
│   └── 一个应用只能有一个Entry
├── Feature HAP（功能模块，type=feature）
│   └── 可按需下载
└── HSP（动态共享包，API 14+支持声明多UIAbility）
```

### 线程模型

- **主线程**：UI绘制、生命周期管理、ArkTS引擎实例管理
- **TaskPool**：执行耗时操作，系统自动管理线程数，推荐使用
- **Worker**：执行耗时操作，开发者自行管理生命周期

---

## HarmonyOS 6 新增特性（API 22+）

### ArkUI 引擎升级
- **NODE级函数式更新**：Diff算法从COMPONENT/ELEMENT树形对比升级为单节点NODE函数式更新，UI渲染性能大幅提升
- **逻辑与UI分离优化**：流转开发代码量降低40%以上

### HarmonyOS 6.1.0 Release 新增（API 23，2026-04-20）

#### ArkUI 增强
- List 与 Grid 组件支持**长按聚拢动效**，交互操作更直观
- 自定义组件新增 **Attach 与 Detach** 生命周期阶段，完善多语言环境排版与阅读
- Navigation **分栏样式可定制**，满足多栏布局个性化设计需求

#### ArkTS 增强
- **模块持久化**：支持模块持久化功能，优化冷启动性能
- **模块懒加载**：扫描工具识别未使用模块，通过懒加载优化冷启动
- **Local Handle / Global Handle**：跨语言内存泄漏检测定位工具，打通 ArkTS ↔ C++ 边界
- ArkTS 快照增强：新增对象属性名和 boolean 变量显式打印，提高 OOM 定位效率

#### Ability Kit 新增
- **启动时间戳能力**：开发者可根据不同启动时间更精准地进行性能调优

#### Form Kit 新增
- **待机屏保卡片**：满足更丰富的 UI 设计及美观诉求
- **透明卡片**：提供更沉浸式的体验

#### ArkWeb 新增
- 画中画、字体预下载
- 同层渲染图层对齐方式自定义
- 默认右键菜单
- 首屏渲染时间统计

#### UI Design Kit 新增
- 底部页签悬浮样式及迷你栏，支持动态折叠展开
- 导航组件支持双栏分割线、右侧默认占位页、标题字号设置
- 底部页签和导航组件新增沉浸式材质效果
- 列表卡片新增无障碍能力
- 新增材质模块，支持设置材质类型和等级

#### ArkUI 增强（Beta2 补充）
- 自定义键盘切换接续（不收回）
- 跑马灯间距配置和滚动时间间隔
- 滚动组件模拟拖拽功能
- RichEditor 单行模式
- PersistenceV2 globalConnect 支持集合类型持久化

#### ArkWeb 增强（Beta1 补充）
- 模拟点击检测
- Cookies 全量获取和属性访问
- 白屏插帧接口
- 禁用 AI 识图能力
- ConsoleMessage 日志来源获取

#### Media Kit 全面升级
- 新增支持 **20 余种媒体格式**
- **系统级边播边缓存**：帮助开发者便捷实现流媒体缓存与起播控制
- **窗口级录屏**：安全隐私自主可控
- **多屏自适应与双屏录制**：大幅降低多屏设备适配成本

#### AR Engine 扩展
- 3D 空间重建会话管理
- 营销组件能力
- 扩展多 Kit 对 PC/2in1、TV 设备支持

### Ability Kit 新增（API 14+）
- HSP 支持在配置文件中声明除入口Ability以外的UIAbility组件
- 新增 UIAbility 备份恢复能力
- 新增获取应用多实例唯一实例标识
- 通过Want传递时可携带应用分身索引（`ohos.param.callerAppCloneIndex`）
- 新增应用级上下文获取能力

### ArkData 新增（API 14+）
- `Preferences.flushSync()` 同步持久化接口
- RDB 新增 `cryptoParam` 参数支持自定义加密
- RDB 新增支持创建可并发事务对象
- UDMF 新增 ContentForm 数据结构

### ArkGraphics2D（API 14+）
- 新增模糊效果处理能力
- 支持动态帧率

---

## 开发环境

### 工具链

- **IDE**：DevEco Studio **6.1.0 Release（6.1.0.830）**（推荐最新版）
- **语言**：ArkTS（主推）
- **构建工具**：hvigor（基于TypeScript）
- **SDK**：Public SDK（**API 23** 稳定版；可通过DevEco Studio切换其他版本）

### 工程目录结构（Stage模型）

```
entry/  # 模块目录
├── src/main/ets/
│   ├── entryability/     # 程序入口类
│   │   └── EntryAbility.ets
│   ├── pages/            # 页面目录
│   │   ├── index.ets     # 首页
│   │   └── xxx.ets
│   └── app.ets           # 应用级别生命周期
├── src/main/module.json5  # 模块配置
├── src/main/resources/   # 资源文件
│   ├── base/             # 默认资源
│   └── rawfile/          # 原始文件
AppScope/
├── app.json5             # 应用全局配置
└── resources/
hvigor/                   # 构建配置
build-profile.json5
```

---

## ArkTS装饰器速查

| 装饰器 | 作用 |
|--------|------|
| `@Entry` | 页面入口 |
| `@Component` | 自定义组件 |
| `@State` | 组件内私有状态 |
| `@Prop` | 父→子单向传递 |
| `@Link` | 父↔子双向同步 |
| `@Provide` | 祖→孙单向传递 |
| `@Consume` | 响应@Provide |
| `@StorageProp` | AppStorage→组件单向 |
| `@StorageLink` | AppStorage↔组件双向 |
| `@ObjectLink` | 嵌套对象双向绑定 |
| `@Preview` | 预览器预览组件 |
| `@Builder` | 自定义构建函数 |
| `@Styles` | 组件复用样式 |
| `@Extend` | 多态样式扩展 |

---

## 页面路由

```typescript
import { router } from '@kit.ArkUI'

// 跳转
router.pushUrl({ url: 'pages/Detail', params: { id: 1 } })

// 返回
router.pop()

// 获取参数
let params = router.getParams() as Record<string, number>
```

---

## 权限声明规范

在 `module.json5` 的 `requestPermissions` 中声明：

```json
{
  "requestPermissions": [
    {
      "name": "ohos.permission.INTERNET",
      "usedScene": {
        "abilities": ["EntryAbility"],
        "when": "always"
      }
    }
  ]
}
```

**user_grant 权限**必须同时：
1. 在配置文件中声明
2. 在代码中调用 `abilityAccessCtrl.requestPermissions()` 动态申请
3. 提供 `reason` 字段用于上架审核（多语种适配）

---

## 签名与上架流程

1. **AGC创建应用**：bundleName 必须与 module.json5 中一致
2. **生成密钥**：DevEco Studio → Build → Generate Key and CSR
3. **申请证书**：AGC → 证书管理 → 调试/发布证书
4. **签名配置**：Project Structure → Signing Configs
5. **打包**：Build → Build App Pack(s)
6. **上架**：AGC → 我的应用 → 上架审核

---

## 关键规则（必读）

1. **bundleName 全局唯一**，一旦确定不可修改
2. **module.json5 中 `mainElement`** 必须对应一个实际存在的 UIAbility
3. **UIAbility 划分原则**：每个 UIAbility 在最近任务列表显示一个任务
4. **API 14+**：`AbilityInfo` 构造时**必须**包含 `orientationId` 属性
5. **API 14+**：`Preferences.flushSync()` 可同步持久化（之前只能异步）
6. **API 14+**：RDB blob类型列插入空数组时返回空数组而非 null
7. **@State 变量改变**会触发所在组件的 `build()` 重新执行
8. **避免在 build() 中直接修改 @State**，会导致循环渲染
9. **网络请求必须声明** `ohos.permission.INTERNET` 权限
10. **user_grant 权限**上架时 reason 字段必填，需多语种适配

---

## API 24 Beta1 变更追踪（2026-04-30）

> 以下为 HarmonyOS 6.1.1(24) Beta1 新增特性，待 API 24 正式发布后纳入正式文档。

| Kit | 变更 |
|-----|------|
| Ability Kit | AbilityStage 上下文能力增强，支持动态加载资源 |
| ArkUI | 平行视界状态获取、自定义组件跨 Ability 迁移、动态布局容器 |
| ArkTS | 虚拟机维测能力增强、taskpool 任务超时设置 |
| ArkWeb | 下载任务回调增强、URL 白名单和安全控制接口 |
| DevEco Studio | Hot Reload 增强（支持 C++ 和资源文件）、AppFreeze 日志解析、ComMemory 模板 |

---

## 参考链接

- 华为开发者文档中心：https://developer.huawei.com/consumer/cn/doc/
- DevEco Studio下载：https://developer.huawei.com/consumer/cn/develop/deveco/studio
- 版本说明：https://developer.huawei.com/consumer/cn/doc/harmonyos-releases
- ArkUI框架：https://developer.huawei.com/consumer/cn/arkui/
