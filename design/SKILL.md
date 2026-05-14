---
name: harmonyos-design
description: |
  HarmonyOS 设计规范指南。用于应用 UI/UX 设计时，参考华为官方 HarmonyOS Design 设计规范。
  触发场景：设计 HarmonyOS 应用界面、配色、字体、图标、布局、动效时，需要了解官方设计规范。
  包含：设计原则、色彩系统、字体规范、图标规范、布局规范、动效规范、多设备设计、设计资源等。
---

# HarmonyOS 设计规范

## 相关技能

| 关联 skill | 路径 | 说明 |
|-----------|------|------|
| 总索引 | `../SKILL.md` | HarmonyOS 全技能入口 |
| 开发规范 | `../dev/SKILL.md` | 代码层面的开发规范 |
| 系统能力 | `../system/SKILL.md` | 蓝牙/定位/传感器等技术规范 |
| 媒体服务 | `../media/SKILL.md` | 相机/音频等媒体规范 |

本文档基于华为官方 HarmonyOS Design 设计指南整理，适用于 HarmonyOS 6.1（API 23 稳定版）应用界面设计。

## 快速导航

- [设计原则](references/overview.md) — 设计理念、分层体系、设计哲学
- [色彩系统](references/color.md) — 主色调、Token机制、浅色/深色模式
- [字体规范](references/typography.md) — HarmonyOS Sans、多设备字号层级
- [图标规范](references/icon.md) — HarmonyOS Symbol、基础图标、多色/分层/动效
- [布局规范](references/layout.md) — 栅格系统、响应式布局、间距规范
- [动效规范](references/animation.md) — 时长曲线、转场动效、微动效
- [多设备设计](references/multi-device.md) — 手机/平板/智慧屏/手表/车机适配
- [设计资源](references/resources.md) — 图标库、色板、字体、模板下载
- [人机交互与系统特性](references/hmi-system-features.md) — 交互方式/导航条/通知/实况窗/多窗口/画中画/深色模式
- [元服务设计](references/atomic-service-design.md) — 免安装轻量服务/8大入口/分发方式
- [UX最佳实践](references/ux-best-practices.md) — 响应式布局/沉浸体验/折叠屏/UX体验标准

---

## 核心设计理念

HarmonyOS Design 采用**简洁高级**的设计哲学，追求：

| 理念 | 说明 |
|------|------|
| 简洁清晰 | 减少视觉噪音，核心内容和关键操作突出 |
| 界面一致 | 相同场景保持统一的布局、颜色、字体、交互 |
| 内容易读 | 图文信息清晰，字号色彩方案标准 |
| 多彩有序 | 色彩运用和谐，避免杂乱 |

---

## 设计分层体系

HarmonyOS Design 采用四层架构模型：

| 层级 | 内容 | 说明 |
|------|------|------|
| 战略层 | 用户体验目标 | 流畅性、无障碍等核心目标 |
| 范围层 | 功能边界与交互模式 | 分布式操作规范等 |
| 框架层 | 标准化组件库 | Button、List 等 80+ 组件 |
| 表现层 | 视觉规范 | 色彩系统、动效曲线、字体规范 |

---

## 设计三原则（多设备通用）

| 原则 | 说明 |
|------|------|
| 差异性 | 针对不同设备特性（屏幕尺寸/交互方式/使用场景）针对性设计 |
| 一致性 | 跨设备体验保持连续性，减少用户学习成本 |
| 协同性 | 多设备无缝流转，展现分布式独特体验 |

---

## HarmonyOS Symbol（新图标体系）

HarmonyOS Symbol 是华为与汉仪联合推出的矢量图标字库（2024年6月发布）：

- **1500+** 矢量图标，任意分辨率清晰
- 分层结构：每个图层可独立设置颜色和灰度
- 无缝集成 HarmonyOS Sans，支持字重同步变化
- **7种动态效果**：消失、出现、弹跳等，支持与点击/长按等操作绑定

```typescript
// ArkTS 中使用 SymbolGlyph
SymbolGlyph($r('sys.symbol.ohos_folder_badge_plus'))
  .fontSize(96)
  .renderingStrategy(SymbolRenderingStrategy.SINGLE)
  .fontColor([Color.Black, Color.Green, Color.White])
```

---

## 色彩系统

| 色彩类型 | 说明 |
|---------|------|
| 主色调 | #007DFF（宇宙蓝） |
| 功能色 | 成功/警告/错误/信息色 |
| Token | 分层颜色变量，支持浅色/深色自动切换 |

---

## 动效规范

| 动效类型 | 时长建议 |
|---------|---------|
| 通用过渡 | 300-500ms |
| 快速反馈 | 100-200ms |
| 强调动效 | 500-800ms |

曲线推荐：`ease`、`ease-in-out`、`fast-out-slow-in`

---

## 设计资源

| 资源类型 | 链接/说明 |
|---------|---------|
| HarmonyOS Symbol | https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/ |
| HarmonyOS Sans 字体 | 系统内置，支持下载 |
| 设计组件库 | 服务组件库、UI组件库、系统特性组件库 |
| 官方设计文档 | https://developer.huawei.com/consumer/cn/design/ |

---

## API 24 Beta1 变更追踪（2026-04-30）

> HarmonyOS 6.1.1(24) Beta1 已发布，设计规范暂无重大变更。持续关注官方更新。

---

## 官方参考

- 设计首页：https://developer.huawei.com/consumer/cn/design/
- 设计资源：https://developer.huawei.com/consumer/cn/design/resource/
- HarmonyOS Symbol：https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/
- 动效规范：https://developer.huawei.com/consumer/cn/doc/design-guides/animation-attributes-0000001797117229
- 色彩规范：https://developer.huawei.com/consumer/cn/doc/design-guides-V1/color-0000001111857246-V1
