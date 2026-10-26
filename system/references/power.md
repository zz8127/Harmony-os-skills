# 电源管理

> **适用版本**：HarmonyOS 26.0.0 / API 26（Release，2026-08-29，底座 OpenHarmony 7.0）；兼容 HarmonyOS 6.1.1 / API 24（Release）及更低版本。兼容 API 14+。

## 概述

电源管理包括休眠/唤醒、亮灭屏、充电状态、电池信息等。

## 亮灭屏控制

```typescript
import { powerManager from '@kit.PowerManagerKit';

// 保持屏幕常亮
powerManager.setKeepScreenOn(true);

// 取消常亮
powerManager.setKeepScreenOn(false);

// 获取屏幕状态
let isScreenOn = powerManager.isScreenOn();
```

## 电池信息

```typescript
import { batteryInfo from '@kit.BasicServicesKit';

// 获取电池信息
console.info('Battery level: ' + batteryInfo.batteryLevel);
console.info('Charging: ' + batteryInfo.chargingStatus);

// 订阅电池变化
batteryInfo.on('batteryChange', (info) => {
  console.info('Battery: ' + info.batteryLevel + '%');
});
```

## 设备休眠

```typescript
// 保持活跃（禁止设备休眠）
powerManager.lock(powerManager.LockMode.SLEEP);

// 解锁休眠
powerManager.unlock(powerManager.LockMode.SLEEP);
```

---

## 官方参考

- PowerManagerKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-powermanager-V5
