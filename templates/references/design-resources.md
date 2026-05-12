# 主题图标设计资源（Design Resources）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## HarmonyOS Symbol 图标字库

**下载地址**：https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/

**特点**：
- 1500+ 矢量图标，任意分辨率清晰
- 每个图标支持分层颜色（单色/多色/分层）
- 支持 7 种动态效果（消失/出现/弹跳等）
- 与 HarmonyOS Sans 无缝集成，字重同步变化

### ArkTS 中使用 SymbolGlyph

```typescript
// 基础用法
SymbolGlyph($r('sys.symbol.ohos_folder_badge_plus'))
  .fontSize(96)
  .fontColor([Color.Black])

// 渲染策略
// SINGLE - 单色模式
// MULTIPLE - 多色模式
// HIERARCHICAL - 分层颜色（不同灰度层级）
SymbolGlyph($r('sys.symbol.ohos_folder'))
  .renderingStrategy(SymbolRenderingStrategy.SINGLE)
  .fontColor([Color.Grey])

// 动态效果 - 7种
SymbolGlyph($r('sys.symbol.ohos_checkmark_circle'))
  .symbolEffect(new SymbolSweepEffect())   // 扫过效果
// 还有：SymbolBounceEffect / SymbolFadeEffect / SymbolScaleEffect 等
```

---

## HarmonyOS Sans 字体

**状态**：系统内置，无需下载

| 特性 | 说明 |
|------|------|
| 字重 | Thin / Light / Regular / Medium / Bold / Black（10档） |
| 语言 | 简繁中文、拉丁、西里尔、希腊、阿拉伯等 105+ 语言 |
| 数字 | 支持变宽数字、等宽数字（`fontVariant: 'tabular-nums'`）、时钟数字 |
| 动态字重 | 支持 `fontWeight` 动态调节 |

### ArkTS 字体使用

```typescript
Text('Hello HarmonyOS')
  .fontFamily('HarmonyOS Sans')
  .fontWeight(FontWeight.Medium)
  .fontSize(16)
  .fontVariant(['tabular-nums'])  // 等宽数字
```

---

## 主题设计规范

**官方文档**：https://developer.huawei.com/consumer/cn/doc/content/themes-specification-0000001160896163

### 主题类型

| 主题类型 | 覆盖范围 | 说明 |
|---------|---------|------|
| **大主题** | 锁屏+桌面+图标+联系人+信息+控制中心+拨号+通话 | 全系统换肤 |
| **小主题** | 锁屏+桌面+图标范围 | 轻度换肤 |
| **锁屏主题** | 仅锁屏范围 | 专注锁屏样式 |
| **图标主题** | 仅图标范围 | 仅替换应用图标 |

### 主题工具

华为提供主题制作工具，开发者可制作自定义图标主题：

1. 下载主题工具
2. 按规范设计图标（尺寸/格式要求）
3. 导出主题包（.hwt）
4. 在设备上安装使用

---

## 色彩系统

| 色彩类型 | 色值 |
|---------|------|
| 主色（宇宙蓝） | #007DFF |
| 深蓝 | #003BB3 |
| 浅蓝 | #99CCFF |
| 成功色 | #36D1A1 |
| 警告色 | #F7CE46 |
| 错误色 | #E84026 |
| 信息色 | #478EDC |

---

## 设计资源下载

**官方资源下载页**：https://developer.huawei.com/consumer/cn/design/resource/

| 资源 | 说明 |
|------|------|
| HarmonyOS Sans | 字体包（系统内置无需下载） |
| HarmonyOS Symbol | 图标字库包 |
| 色板 | 色彩规范文件 |
| 模板 | 界面设计模板 |
| 音效 | 官方音效资源 |

---

## ArkUI 组件速查

> 详见：[arkui-components.md](arkui-components.md)

| 类别 | 组件 |
|------|------|
| 基础 | Text / Button / Image / Span |
| 容器 | Column / Row / Flex / Stack / List / Grid |
| 媒体 | Video / Audio / Camera |
| 画布 | Canvas / XComponent |
| 弹窗 | Dialog / ActionSheet / AlertDialog |
| 导航 | Navigation / Tabs / TabContent |
| 绘图 | Circle / Rect / Path / Shape |

---

## 官方参考

- Symbol 图标库：https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/
- 设计资源中心：https://developer.huawei.com/consumer/cn/design/resource/
- 主题设计规范：https://developer.huawei.com/consumer/cn/doc/content/themes-specification-0000001160896163
- 设计首页：https://developer.huawei.com/consumer/cn/design/
