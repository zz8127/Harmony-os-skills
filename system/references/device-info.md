# 设备标识与信息

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 获取设备标识

```typescript
import { deviceInfo } from '@kit.BasicServicesKit';

// 获取设备基本信息
let deviceId = deviceInfo.uuid;         // 设备唯一标识
let deviceType = deviceInfo.deviceType;  // 设备类型
let osFullName = deviceInfo.osFullName;  // 系统版本
```

## 获取网络信息

```typescript
import { netManager } from '@kit.ConnectivityKit';

// 检查网络连接状态
let isConnected = netManager.isDefaultNetAvailable();

// 获取激活的网络信息
let netHandle = netManager.getActiveNetId();
let netCapabilities = netManager.getNetCapabilities(netHandle);
console.info('Network type: ' + netCapabilities.bearerTypes);
```

## 获取 SIM 卡信息

```typescript
import { telephony from '@kit.TelephonyKit';

let simCount = telephony.getSimCount();  // SIM 卡数量
for (let i = 0; i < simCount; i++) {
  let simInfo = telephony.getSimInfo(i);
  console.info('SIM ' + i + ': ' + simInfo.spn);
}
```

## 官方参考

- 设备标识：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-identifier-V14
- 网络管理：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/netmanager-overview-V5
