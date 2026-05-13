# Pen Kit — 手写笔

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Pen Kit 提供手写笔开发能力，支持画布绘制、笔迹渲染、长画布滚动等场景，适用于笔记、绘画、签名等应用。

---

## 核心组件

### HandWriteComponent

Pen Kit 的核心组件，提供手写绘制画布。

```typescript
import { HandWriteComponent } from '@kit.PenKit'

HandWriteComponent({
  canvasConfig: {
    width: 360,
    height: 600,
    backgroundColor: Color.White
  }
})
```

---

## API 23 新增（HarmonyOS 6.1.0）

### 禁用画布缩放

新增禁用画布缩放能力，防止用户误触缩放。

### ScrollTo 滚动位置

新增设置滚动位置 `ScrollTo` 及监听长画布滚动位置能力，适用于长笔记、长画卷等场景。

### 自定义长画布最大高度

新增自定义长画布最大高度能力，开发者可根据业务需求设置画布最大高度。

---

## Kit 导入

```typescript
import { HandWriteComponent } from '@kit.PenKit'
```

---

## 官方参考

- Pen Kit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pen-suite
- 手写组件开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pen-handwritecomponent
