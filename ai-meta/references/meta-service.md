# 元服务（Service Widget / 卡片）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

元服务（Meta Service / Service Widget）是 HarmonyOS 的免安装轻量应用形态，通过**服务卡片**（Service Widget）在桌面、锁屏、负一屏等位置展示，提供即时服务。

### 与普通应用的区别

| 特性 | 普通应用 | 元服务 |
|------|---------|--------|
| 安装 | 需要安装 | 无需安装，即点即用 |
| 体积 | 通常较大 | 轻量（一般 < 2MB） |
| 分发 | 应用市场 | 服务市场/小艺推荐/扫码 |
| 更新 | 应用内更新 | 后台静默更新 |
| 入口 | 桌面图标 | 桌面卡片/小艺/搜索 |

---

## 服务卡片（Service Widget）

### 卡片尺寸规格

| 尺寸 | 宽高比 | 描述 |
|------|--------|------|
| 1×1 | 1:1 | 小卡片 |
| 1×2 | 1:2 | 纵向卡片 |
| 2×1 | 2:1 | 横向卡片 |
| 2×2 | 1:1 | 中卡片 |
| 2×4 | 1:2 | 大卡片 |

### 创建卡片

```typescript
// EntryAbility.ets - 配置卡片能力
onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
  // 卡片提供者生命周期回调
}

// MyForm.lz - 卡片组件
@Entry
@Component
struct MyForm {
  @LocalStorageProp('formId') formId: string = '';

  aboutToAppear() {
    // 卡片数据初始化
  }

  build() {
    Column() {
      Text('服务卡片')
        .fontSize(24)
      Text('点击刷新')
        .fontSize(12)
        .onClick(() => {
          // 更新卡片
        })
    }
  }
}
```

### 卡片路由（postCardAction）

```typescript
// 拉起应用指定页面
postCardAction({
  action: 'router',
  params: { targetPage: 'detail' }
});

// 拉起后台能力（call）
postCardAction({
  action: 'call',
  params: { method: 'refresh', data: 'token123' }
});
```

### 卡片数据更新

```typescript
import { formBindingData } from '@kit.FormKit';
import { formProvider } from '@kit.FormKit';

// 定时更新
formProvider.updateForm(formId, formBindingData.createFormBindingData({ value: 'new data' }));

// 定点更新（在 module.json5 中配置）
"scheduledUpdateTime": "22:00",
"updateDuration": 3600
```

---

## 服务流转

服务流转（Continuously Transfer）支持在设备间无缝迁移正在运行的服务：

```typescript
import { continuationManager } from '@kit.AbilityKit';

// 检查流转能力是否可用
continuationManager.registerContinuationCallback({
  onContinue(want: Want) {
    // 将业务状态序列化为 want
    want.parameters = { 'state': JSON.stringify(appState) };
  }
});

// 发起流转
continuationManager.startContinuityDevicePicker();
```

---

## 官方参考

- 元服务开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-widget-overview-V5
- 服务卡片开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/card-list-overview-V5
