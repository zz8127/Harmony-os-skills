---
name: harmonyos-templates
description: |
  HarmonyOS 官方模板与组件库技能。收录 DevEco Studio 工程模板、生态市场模板/组件、设计资源等索引。
  触发场景：创建新工程时需要选模板；需要参考官方模板快速上手；需要主题/图标/字体等设计资源时。
  包含：DevEco Studio 内置模板、生态市场模板、主题规范、图标库、设计资源链接。
---

# HarmonyOS 模板与组件库

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。
> **模板市场**：https://developer.huawei.com/consumer/cn/market/prod-list?origin=template
> **主题图标库**：https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/
> **主题设计规范**：https://developer.huawei.com/consumer/cn/doc/content/themes-specification-0000001160896163

## 相关技能

| 关联 skill | 路径 | 说明 |
|-----------|------|------|
| 总索引 | `../SKILL.md` | HarmonyOS 全技能入口 |
| 开发规范 | `../dev/SKILL.md` | 工程创建/Stage模型/ArkTS |
| 设计规范 | `../design/SKILL.md` | 色彩/字体/图标/布局/动效规范 |
| 示例代码 | `../samples/SKILL.md` | 官方示例代码参考 |

---

## 快速导航

| 资源类型 | 说明 |
|---------|------|
| [DevEco Studio 工程模板](references/deveco-templates.md) | IDE 内置模板（Empty/TV/Wearable等） |
| [生态市场模板](references/market-templates.md) | 行业应用模板（新闻/电商/餐饮等） |
| [主题图标设计资源](references/design-resources.md) | HarmonyOS Sans/Symbol/主题规范 |
| [ArkUI 组件库](references/arkui-components.md) | 80+ ArkUI 标准化组件速查 |

---

## 模板资源总览

| 资源 | 来源 | 链接 |
|------|------|------|
| DevEco Studio 内置模板 | DevEco Studio 新建工程 | IDE 内置 |
| 生态市场模板 | 华为生态市场 | market/prod-list |
| ArkUI 组件 | 华为文档/设计规范 | design/ 目录下各 ref |
| HarmonyOS Symbol | 设计频道 | design/harmonyos-symbol |
| HarmonyOS Sans | 系统内置 | 无需下载 |
| 主题工具 | 华为主题工作室 | design/resource |

---

## DevEco Studio 内置工程模板

在 DevEco Studio 中：`File → New → Create Project`

| 模板类型 | 适用设备 | 说明 |
|---------|---------|------|
| **Empty Ability** | Phone/Tablet | 空白页面，最基础的 Stage 模型工程 |
| **Atomic Service** | 全部 | 元服务（免安装）模板 |
| **ets** | Phone | ArkTS 单语言工程 |
| **Native C++** | Phone | 支持 Native 开发 |
| **TV** | 智慧屏 | 电视设备专用模板 |
| **Wearable** | 智能手表 | 手表设备模板 |
| **Car** | 车机 | 车机设备模板 |

**工程模板文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template

---

## 生态市场模板（行业模板）

华为生态市场提供多种行业应用模板，覆盖常见业务场景：

| 行业类别 | 模板示例 | 说明 |
|---------|---------|------|
| 新闻资讯 | 列表+详情布局 | 新闻列表、图文详情 |
| 电商购物 | 商品列表/详情/购物车 | 商品展示、购物车、下单 |
| 社交聊天 | 聊天列表/详情 | 即时通讯、朋友圈 |
| 餐饮美食 | 菜单/订单/外卖 | 菜品浏览、订单管理 |
| 商务办公 | 笔记/日程/文档 | 效率工具类 |
| 教育备考 | 课程/题库/学习 | 在线教育 |
| 旅游出行 | 行程/酒店/票务 | 旅行预订 |

**市场地址**：https://developer.huawei.com/consumer/cn/market/prod-list?origin=template&ha_source=yzc&ha_sourceId=89000071

---

## 设计资源

| 资源类型 | 说明 | 链接 |
|---------|------|------|
| HarmonyOS Sans | 多语言可变字体，系统内置 | 无需下载 |
| HarmonyOS Symbol | 1500+ 矢量图标字库 | https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/ |
| 主题设计规范 | 大主题/小主题/锁屏/图标主题规范 | https://developer.huawei.com/consumer/cn/doc/content/themes-specification-0000001160896163 |
| 设计资源下载 | 色板/字体/图标包 | https://developer.huawei.com/consumer/cn/design/resource/ |

---

## API 24 Beta1 变更追踪（2026-04-30）

> HarmonyOS 6.1.1(24) Beta1 已发布，模板与组件库暂无重大变更。持续关注官方更新。

---

## 使用建议

1. **快速启动**：从 DevEco Studio Empty Ability 模板开始，按需添加功能
2. **参考行业模板**：生态市场模板可直接下载导入，参考其工程结构和页面布局
3. **复用组件**：使用 ArkUI 80+ 内置组件，避免重复造轮子
4. **设计一致性**：使用 HarmonyOS Sans + Symbol 保持视觉一致性
5. **主题定制**：通过主题工具制作图标主题和锁屏主题
