# 低功耗蓝牙（BLE）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

蓝牙分为传统蓝牙（BR/EDR）和低功耗蓝牙（BLE）。BLE 适合续航要求高的设备，传输速率最高 1Mbps，通信范围约 10m。

## BLE 扫描

### 开发步骤

1. 申请蓝牙权限 `ohos.permission.ACCESS_BLUETOOTH`
2. 导入 ble 模块
3. 创建 BleScanner 实例
4. 订阅扫描结果事件
5. 发起扫描

### API Version 15+（推荐）

```typescript
import { ble } from '@kit.ConnectivityKit';
import { BusinessError } from '@kit.BasicServicesKit';

// 定义扫描结果回调
function onReceiveEvent(scanReport: ble.ScanReport) {
  console.info('BLE scan result: ' + JSON.stringify(scanReport));
}

// 创建 BLE 扫描器
let bleScanner: ble.BleScanner = ble.createBleScanner();

// 订阅扫描结果
bleScanner.on('BLEDeviceFind', onReceiveEvent);

// 发起扫描
bleScanner.startScan();
```

### API Version 14 及以前

```typescript
function onReceiveEvent(data: Array<ble.ScanResult>) {
  console.info('BLE device find: ' + JSON.stringify(data));
}

ble.on('BLEDeviceFind', onReceiveEvent);
ble.startBLEScan(null);
```

---

## BLE 广播

```typescript
import { ble } from '@kit.ConnectivityKit';

// 设置广播参数
let advertiseSettings: ble.AdvertiseSettings = {
  interval: 160,  // 广播间隔（单位：0.625ms，160=100ms）
  txPower: 0,      // 发射功率
  connectable: true
};

// 设置广播数据
let advertiseData: ble.AdvertiseData = {
  serviceUuids: ['0000xxxx-0000-1000-8000-00805f9b34fb'],
  manufacturerData: [{ primaryValue: [1, 2, 3] }]
};

// 开始广播
ble.startAdvertising(advertiseSettings, advertiseData);
```

---

## BLE 连接

```typescript
import { ble } from '@kit.ConnectivityKit';

// BLE 连接状态变化订阅
ble.on('BLEConnectionStateChange', (data: ble.BLEConnectionStateChangeInfo) => {
  console.info('BLE state change: ' + data.state);
});

// 连接设备
let deviceId = 'XX:XX:XX:XX:XX:XX';
ble.createGattClientDevice(deviceId).connect();
```

---

## BLE 权限

```json
"requestPermissions": [
  { "name": "ohos.permission.ACCESS_BLUETOOTH" },
  { "name": "ohos.permission.BLUETOOTH_SCANNING" },
  { "name": "ohos.permission.BLUETOOTH_ADMINISTRATOR" }
]
```

---

## 官方参考

- BLE 开发指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ble-development-guide-V5
- 蓝牙设置（传统蓝牙）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/br-development-guide-V14
