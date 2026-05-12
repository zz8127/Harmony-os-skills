# Wi-Fi

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

ConnectivityKit 提供 Wi-Fi 连接管理能力，包括 Wi-Fi 扫描、连接、热点共享等。

## Wi-Fi 状态

```typescript
import { wifiManager } from '@kit.ConnectivityKit';

// 获取 Wi-Fi 连接状态
let isConnected = wifiManager.isConnected();

// 获取当前 Wi-Fi 信息
let wifiInfo = wifiManager.getLinkedInfo();
console.info('Wi-Fi SSID: ' + wifiInfo?.ssid);
```

## Wi-Fi 扫描

```typescript
import { wifiManager } from '@kit.ConnectivityKit';
import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';

// 获取扫描结果
wifiManager.getScanInfoList((err: BusinessError, result: Array<wifiManager.WifiScanInfo>) => {
  if (err) {
    console.error('Scan failed: ' + err.message);
    return;
  }
  console.info('Found ' + result.length + ' networks');
  result.forEach(info => {
    console.info('SSID: ' + info.ssid + ', Signal: ' + info.rssi);
  });
});
```

## Wi-Fi 连接

```typescript
import { wifiManager } from '@kit.ConnectivityKit';

// 连接指定 Wi-Fi
let config: wifiManager.WifiDeviceConfig = {
  ssid: 'MyWiFi',
  preSharedKey: 'password123',
  securityType: wifiManager.WifiSecurityType.WIFI_SEC_TYPE_PSK
};

let networkId = wifiManager.addDeviceConfig(config);
wifiManager.connectToNetwork(networkId);
```

## Wi-Fi 事件订阅

```typescript
// 订阅 Wi-Fi 状态变化
wifiManager.on('wifiStateChange', (state: number) => {
  console.info('Wi-Fi state: ' + state);
});

// 订阅扫描结果变化
wifiManager.on('scanStateChange', (state: number) => {
  console.info('Scan state: ' + state);
});
```

## Wi-Fi 权限

```json
"requestPermissions": [
  { "name": "ohos.permission.GET_WIFI_INFO" },
  { "name": "ohos.permission.SET_WIFI_INFO" },
  { "name": "ohos.permission.INTERNET" }
]
```

---

## 官方参考

- Wi-Fi 开发概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wifi-overview-V5
- Wi-Fi 连接：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wifi-development-guide-V5
