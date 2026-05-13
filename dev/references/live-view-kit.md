# 实况窗服务（Live View Kit）

> HarmonyOS 6.1 / API 23

## 概述

实况窗服务（Live View Kit）提供实时信息展示能力，可在锁屏、通知栏等场景展示动态内容，通过 `@kit.LiveViewKit` 引入。支持导航、打车、外卖等场景的实时状态展示。API 23 新增地理位置触发实况窗能力。

## LiveViewManager

LiveViewManager 是实况窗服务的管理入口，用于创建、更新和停止实况窗。

```typescript
import { liveViewManager } from '@kit.LiveViewKit';

const manager = liveViewManager.getInstance();
```

## 启动实况窗

创建并启动一个实况窗实例。

```typescript
import { liveViewManager, LiveViewInfo, LiveViewStyle } from '@kit.LiveViewKit';

async function startLiveView(manager: liveViewManager.LiveViewManager): Promise<string> {
  const liveViewInfo: LiveViewInfo = {
    liveViewStyle: LiveViewStyle.TRANSPORT,
    title: '导航中',
    content: '前往天安门广场',
    icon: $r('app.media.nav_icon'),
    progressValue: 60,
    progressMaxValue: 100
  };

  const liveViewId = await manager.startLiveView(liveViewInfo);
  return liveViewId;
}
```

## 更新实况窗

更新实况窗的显示内容。

```typescript
import { liveViewManager, LiveViewInfo } from '@kit.LiveViewKit';

async function updateLiveView(
  manager: liveViewManager.LiveViewManager,
  liveViewId: string
): Promise<void> {
  const updateInfo: LiveViewInfo = {
    title: '即将到达',
    content: '距离目的地 500 米',
    progressValue: 90,
    progressMaxValue: 100
  };
  await manager.updateLiveView(liveViewId, updateInfo);
}
```

## 停止实况窗

结束实况窗展示。

```typescript
import { liveViewManager } from '@kit.LiveViewKit';

async function stopLiveView(
  manager: liveViewManager.LiveViewManager,
  liveViewId: string
): Promise<void> {
  await manager.stopLiveView(liveViewId);
}
```

## 地理位置触发实况窗（API 23）

API 23 新增基于地理位置自动触发实况窗，当用户进入或离开指定区域时自动展示。

```typescript
import { liveViewManager, LiveViewTriggerInfo } from '@kit.LiveViewKit';

async function startLiveViewByTrigger(manager: liveViewManager.LiveViewManager): Promise<string> {
  const triggerInfo: LiveViewTriggerInfo = {
    liveViewStyle: LiveViewStyle.TRANSPORT,
    title: '到达提醒',
    content: '您已接近目的地',
    triggerLatitude: 39.9042,
    triggerLongitude: 116.4074,
    triggerRadius: 500,
    icon: $r('app.media.location_icon')
  };

  const liveViewId = await manager.startLiveViewByTrigger(triggerInfo);
  return liveViewId;
}
```

## 实况窗样式

| 样式 | 说明 | 适用场景 |
|------|------|----------|
| `TRANSPORT` | 交通出行样式 | 导航、打车 |
| `SPORTS` | 运动样式 | 健身、跑步 |
| `FOOD_DELIVERY` | 外卖样式 | 外卖配送 |
| `TAXI` | 出行样式 | 打车出行 |

```typescript
import { LiveViewStyle } from '@kit.LiveViewKit';

const transportStyle: LiveViewStyle = LiveViewStyle.TRANSPORT;
const sportsStyle: LiveViewStyle = LiveViewStyle.SPORTS;
const foodStyle: LiveViewStyle = LiveViewStyle.FOOD_DELIVERY;
const taxiStyle: LiveViewStyle = LiveViewStyle.TAXI;
```

## 完整示例

```typescript
import { liveViewManager, LiveViewInfo, LiveViewStyle } from '@kit.LiveViewKit';

@Entry
@Component
struct LiveViewPage {
  private manager: liveViewManager.LiveViewManager = liveViewManager.getInstance();
  private liveViewId: string = '';

  async onStartLiveView(): Promise<void> {
    const info: LiveViewInfo = {
      liveViewStyle: LiveViewStyle.TRANSPORT,
      title: '导航中',
      content: '前往目的地',
      progressValue: 0,
      progressMaxValue: 100
    };
    this.liveViewId = await this.manager.startLiveView(info);
  }

  async onUpdateProgress(value: number): Promise<void> {
    if (!this.liveViewId) return;
    const info: LiveViewInfo = {
      progressValue: value,
      progressMaxValue: 100
    };
    await this.manager.updateLiveView(this.liveViewId, info);
  }

  async onStopLiveView(): Promise<void> {
    if (!this.liveViewId) return;
    await this.manager.stopLiveView(this.liveViewId);
    this.liveViewId = '';
  }

  build() {
    Column() {
      Button('启动实况窗').onClick(() => this.onStartLiveView())
      Button('更新进度').onClick(() => this.onUpdateProgress(75))
      Button('停止实况窗').onClick(() => this.onStopLiveView())
    }
  }
}
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.NOTIFICATION_CONTROLLER` | 通知控制权限 |

在 `module.json5` 中声明：

```json
{
  "requestPermissions": [
    { "name": "ohos.permission.NOTIFICATION_CONTROLLER" }
  ]
}
```

## 官方参考

- [Live View Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/live-view-kit-overview-0000001820880925)
- [Live View Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/live-view-manager-0000001774121282)
