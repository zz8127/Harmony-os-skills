# Accessibility Kit — 无障碍

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Accessibility Kit 提供无障碍开发能力，帮助应用支持屏幕朗读、屏幕放大、无障碍扩展等功能，确保视障、听障等用户群体也能正常使用应用。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 屏幕朗读 | TalkBack 语音朗读界面元素 |
| 屏幕放大 | 手势放大屏幕内容 |
| 无障碍扩展 | AccessibilityExtensionAbility |
| 无障碍事件 | 监听和响应无障碍事件 |

---

## 无障碍扩展能力

```typescript
import { AccessibilityExtensionAbility } from '@kit.AccessibilityKit'

export default class MyAccessibilityExtension extends AccessibilityExtensionAbility {
  onConnect() {
  }

  onDisconnect() {
  }

  onAccessibilityEvent(event: AccessibilityEvent) {
  }
}
```

---

## ArkUI 无障碍属性

```typescript
@Entry
@Component
struct AccessiblePage {
  build() {
    Column() {
      Button('提交')
        .accessibilityText('提交订单按钮')
        .accessibilityDescription('点击此按钮提交您的订单')
        .accessibilityLevel('yes')
    }
  }
}
```

### 常用无障碍属性

| 属性 | 说明 |
|------|------|
| `.accessibilityText()` | 无障碍朗读文本 |
| `.accessibilityDescription()` | 无障碍描述 |
| `.accessibilityLevel()` | 是否可被朗读（'auto'/'yes'/'no'） |
| `.accessibilityGroup()` | 无障碍分组 |
| `.accessibilityRole()` | 无障碍角色类型 |

---

## API 23 新增（HarmonyOS 6.1.0）

### UI Design Kit 无障碍增强

- 列表卡片新增无障碍分组、聚合播报能力
- 新增拦截无障碍事件能力
- 新增设置列表预览菜单样式、横滑删除触发类型

---

## Kit 导入

```typescript
import { accessibility } from '@kit.AccessibilityKit'
```

---

## 官方参考

- Accessibility Kit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/accessibility-overview
- 无障碍开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/accessibility-development-guide
- ArkUI 无障碍属性：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/ts-universal-attributes-accessibility
