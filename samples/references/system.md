# 系统能力示例（System）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## 蓝牙 BLE

### API 15+ BleScanner（推荐）

```typescript
import { ble } from '@kit.ConnectivityKit';

// 1. 权限申请（user_grant）
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
let atManager = abilityAccessCtrl.createAtManager();
atManager.requestPermissions(/* context, permissions array */);

// 2. 获取扫描器
let scanner = ble.createBleScanner();

// 3. 设置扫描结果回调
scanner.on('BLEDeviceFind', (results) => {
  results.forEach(result => {
    console.info('发现设备：' + result.deviceId);
  });
});

// 4. 开始扫描
scanner.startScan();

// 5. 停止扫描
scanner.stopScan();
```

### 传统蓝牙

```typescript
import bluetooth from '@ohos.bluetooth';

// 获取配对设备列表
let devices = bluetooth.getPairedDevices();
console.info('配对设备数：' + devices.length);
```

---

## Wi-Fi

### 连接管理

```typescript
import wifiManager from '@ohos.wifiManager';

// 扫描 Wi-Fi
wifiManager.scan();

// 获取扫描结果
setTimeout(() => {
  let results = wifiManager.getScanInfoList();
  results.forEach(info => {
    console.info('SSID: ' + info.ssid);
  });
}, 3000);

// 连接指定网络
wifiManager.connectToNetwork(info.networkId);
```

---

## NFC

```typescript
import nfcController from '@ohos.nfc.controller';

// 检查 NFC 状态
let isEnabled = nfcController.isNfcOpen();
console.info('NFC 开启：' + isEnabled);
```

---

## 定位

### GNSS + 网络定位

```typescript
import geolocation from '@ohos.geoLocationManager';

// 权限：ohos.permission.LOCATION
// user_grant，需要动态申请

// 获取当前位置
geolocation.getCurrentLocation({
  priority: 0, // LOCATION_PRIORITY_ACCURACY
  scenario: 0  // UNSET_SCENARIO
}, (err, location) => {
  if (err) {
    console.error('定位失败：' + err.message);
    return;
  }
  console.info('经度：' + location.longitude);
  console.info('纬度：' + location.latitude);
});

// 订阅位置变化
geolocation.on('locationChange', {
  priority: 0,
  scenario: 0
}, (location) => {
  console.info('位置更新：' + JSON.stringify(location));
});
```

---

## 传感器（SensorServiceKit）

```typescript
import sensor from '@kit.SensorServiceKit';

// 加速度计
sensor.on(sensor.SensorType.SENSOR_TYPE_ID_ACCELEROMETER, (data) => {
  console.info('X: ' + data.x + ' Y: ' + data.y + ' Z: ' + data.z);
}, { interval: 100000000 }); // 100ms

// 计步器
sensor.on(sensor.SensorType.SENSOR_TYPE_ID_STEP_COUNTER, (data) => {
  console.info('步数：' + data.steps);
});

// 陀螺仪
sensor.on(sensor.SensorType.SENSOR_TYPE_ID_GYROSCOPE, (data) => {
  console.info('角速度 X: ' + data.x);
});
```

---

## 官方参考

- ConnectivityKit BLE：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ble-scan
- Wi-Fi：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wifi-connection
- 定位：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/location-service
- 传感器：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/sensor-kit-guide
