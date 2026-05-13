# Form Kit — 卡片开发

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Form Kit（卡片开发框架）是 HarmonyOS 提供的桌面卡片开发能力，允许应用以卡片形式在桌面、服务中心等位置展示关键信息和交互入口。

### 卡片类型

| 类型 | 说明 | 尺寸 |
|------|------|------|
| 静态卡片 | 数据固定，定时刷新 | 1×2 / 2×2 / 2×4 / 4×4 |
| 动态卡片 | 实时数据更新，支持交互 | 1×2 / 2×2 / 2×4 / 4×4 |

---

## ArkTS 卡片开发

### 卡片配置（form_config.json）

```json
{
  "forms": [
    {
      "name": "Widget",
      "displayName": "我的卡片",
      "description": "示例卡片",
      "src": "./ets/widget/pages/WidgetCard.ets",
      "uiSyntax": "arkts",
      "window": {
        "designWidth": 720,
        "autoDesignWidth": true
      },
      "colorMode": "auto",
      "isDefault": true,
      "updateEnabled": true,
      "scheduledUpdateTime": "10:30",
      "updateDuration": 1,
      "defaultDimension": "2*2",
      "supportDimensions": ["1*2", "2*2", "2*4", "4*4"]
    }
  ]
}
```

### 卡片页面开发

```typescript
@Entry
@Component
struct WidgetCard {
  @LocalStorageProp('title') title: string = '默认标题'
  @LocalStorageProp('content') content: string = '默认内容'

  build() {
    Column() {
      Text(this.title)
        .fontSize(16)
        .fontWeight(FontWeight.Bold)
      Text(this.content)
        .fontSize(12)
        .fontColor('#999999')
    }
    .width('100%')
    .height('100%')
    .padding(12)
  }
}
```

### 卡片数据更新

```typescript
import { formProvider } from '@kit.AbilityKit'
import { formInfo } from '@kit.AbilityKit'

formProvider.updateForm(formId, {
  'title': '新标题',
  'content': '新内容'
})
```

---

## API 23 新增（HarmonyOS 6.1.0）

### V2 装饰器语法

ArkTS 卡片开发支持 V2 装饰器语法，提供更灵活的卡片开发体验。

### 待机屏保卡片

新增待机屏保卡片能力，满足更丰富的 UI 设计及美观诉求。

### 透明卡片

新增透明卡片能力，提供更沉浸式的体验。

---

## module.json5 卡片声明

```json
{
  "extensionAbilities": [
    {
      "name": "FormAbility",
      "srcEntry": "./ets/formability/FormAbility.ets",
      "type": "form",
      "metadata": [
        {
          "name": "ohos.extension.form",
          "resource": "$profile:form_config"
        }
      ]
    }
  ]
}
```

---

## 卡片生命周期

```typescript
import { FormExtensionAbility, formInfo } from '@kit.AbilityKit'

export default class FormAbility extends FormExtensionAbility {
  onAddForm(want: Want) {
    return formInfo.FormBindingData({ 'title': 'Hello', 'content': 'World' })
  }

  onUpdateForm(formId: string) {
    return formInfo.FormBindingData({ 'title': 'Updated' })
  }

  onRemoveForm(formId: string) {
  }
}
```

---

## 官方参考

- Form Kit 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-widget-overview-V5
- ArkTS卡片开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-ui-widget-overview
- 卡片开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/widget-development
