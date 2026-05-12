# 传统蓝牙（BR/EDR）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

传统蓝牙（Basic Rate/Enhanced Data Rate, BR/EDR）通信范围约 100m，传输速率 2-3Mbps。适用于音频（耳机/音箱）、车载免提、数据传输等场景。

## 蓝牙状态管理

```typescript
import { access } from '@kit.ConnectivityKit';
import { BusinessError } from '@kit.BasicServicesKit';

// 订阅蓝牙开关状态变化
function onReceiveEvent(data: access.BluetoothState) {
  if (data === access.BluetoothState.STATE_ON) {
    console.info('Bluetooth is ON');
  } else if (data === access.BluetoothState.STATE_OFF) {
    console.info('Bluetooth is OFF');
  }
}

access.on('stateChange', onReceiveEvent);

// 获取当前蓝牙状态
let state = access.getState();
```

## 获取配对设备列表

```typescript
let pairedDevices = access.getPairedDevices();
console.info('Paired devices: ' + JSON.stringify(pairedDevices));
```

## 开启蓝牙扫描

```typescript
import { connection } from '@kit.ConnectivityKit';

// 获取蓝牙设备 MAC 地址
connection.on('bluetoothDeviceFind', (data: Array<string>) => {
  console.info('Found devices: ' + JSON.stringify(data));
});

connection.startBluetoothDiscovery();
```

## 蓝牙权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.ACCESS_BLUETOOTH` | 蓝牙开关控制 |
| `ohos.permission.BLUETOOTH_SCANNING` | 蓝牙扫描 |
| `ohos.permission.BLUETOOTH_ADMINISTRATOR` | 蓝牙管理 |

---

## 官方参考

- 蓝牙设置开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/br-development-guide-V14
- 蓝牙服务概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/bluetooth-overview
