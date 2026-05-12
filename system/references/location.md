# 位置服务（LocationKit）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

位置服务（LocationKit）支持 GNSS 定位、网络定位（基站+Wi-Fi/蓝牙）、地理围栏、地理编码等功能。定位时综合使用多种技术（GNSS + 网络定位），确保室内外均可准确定位。

坐标系统：1984 年世界大地坐标系（WGS84），使用经纬度描述位置。

## 权限申请

```json
"requestPermissions": [
  { "name": "ohos.permission.LOCATION" },
  { "name": "ohos.permission.LOCATION_IN_BACKGROUND" }
]
```

## 获取单次位置

```typescript
import { geoLocationManager } from '@kit.LocationKit';
import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';

// 获取单次位置
geoLocationManager.getCurrentLocation((err: BusinessError, location: geoLocationManager.Location) => {
  if (err) {
    console.error('Location failed: ' + err.message);
    return;
  }
  console.info('Latitude: ' + location.latitude + ', Longitude: ' + location.longitude);
});
```

## 连续位置订阅

```typescript
// 订阅位置变化
let requestInfo: geoLocationManager.LocationRequest = {
  priority: geoLocationManager.LocationRequestPriority.LOCATION_PRIORITY_ACCURACY,
  timeInterval: 3,  // 位置更新间隔（秒）
  distanceInterval: 0
};

let callback: geoLocationManager.LocationCallback = {
  onLocationReport(location: geoLocationManager.Location) {
    console.info('Location update: ' + JSON.stringify(location));
  },
  onError(error: BusinessError) {
    console.error('Location error: ' + error.message);
  }
};

geoLocationManager.startLocating(requestInfo, callback);

// 停止订阅
geoLocationManager.stopLocating(callback);
```

## 地理围栏

```typescript
// 创建圆形地理围栏
let geofence: geoLocationManager.Geofence = {
  longitude: 116.397,
  latitude: 39.909,
  radius: 500,           // 半径（米）
  uniqueId: 'myGeofence',
  geofenceTransition: geoLocationManager.GeofenceTransition.ENTER_GEOFENCE_TRANSITION
};

geoLocationManager.addGnssGeofence([geofence]);
```

## 定位精度策略

| 策略 | 说明 | 适用场景 |
|------|------|---------|
| ACCURACY | 高精度（GPS优先） | 导航、定位打卡 |
| LOW_POWER | 低功耗（网络定位优先） | 天气、附近推荐 |
| FIRST_FIX | 快速定位 | 应用冷启动 |

---

## 官方参考

- 位置服务概述：https://developer.huawei.com/consumer/cn/doc/atomic-ascf/develop-location-retrieval
- 获取位置信息：https://developer.huawei.com/consumer/cn/doc/atomic-ascf/develop-location-retrieval
