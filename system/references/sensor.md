# 传感器（SensorServiceKit）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

SensorServiceKit 提供设备传感器数据订阅能力，包括加速度、陀螺仪、计步、环境光、距离、心率等传感器。

## 常用传感器列表

| 传感器 ID | 说明 | 单位 |
|----------|------|------|
| ACCELEROMETER | 加速度传感器 | m/s² |
| GYROSCOPE | 陀螺仪 | rad/s |
| AMBIENT_LIGHT | 环境光传感器 | lux |
| MAGNETIC_FIELD | 磁场传感器 | μT |
| PROXIMITY | 距离传感器 | cm |
| STEP_COUNTER | 计步传感器 | 步数 |
| STEP_DETECTOR | 步数检测 | 事件 |
| BAROMETER | 气压计 | Pa |
| HEART_RATE | 心率传感器 | bpm |

## 传感器开发步骤

### 1. 查询设备支持的所有传感器

```typescript
import { sensor } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

sensor.getSensorList((error: BusinessError, data: Array<sensor.Sensor>) => {
  if (error) {
    console.error('getSensorList failed');
    return;
  }
  data.forEach(s => {
    console.info('Sensor: ' + s.sensorName);
  });
});
```

### 2. 持续订阅传感器数据

```typescript
import { sensor } from '@kit.SensorServiceKit';

// 加速度传感器订阅
sensor.on(sensor.SensorId.ACCELEROMETER, (data: sensor.AccelerometerResponse) => {
  console.info('X: ' + data.x + ', Y: ' + data.y + ', Z: ' + data.z);
});

// 带选项的订阅（采样间隔）
let options: sensor.Options = {
  interval: 100000  // 微秒（10Hz）
};
sensor.on(sensor.SensorId.ACCELEROMETER, options, callback);
```

### 3. 单次获取传感器数据

```typescript
sensor.once(sensor.SensorId.ACCELEROMETER, (data: sensor.AccelerometerResponse) => {
  console.info('One-time reading: ' + JSON.stringify(data));
});
```

### 4. 取消订阅

```typescript
sensor.off(sensor.SensorId.ACCELEROMETER);
```

## 计步传感器

```typescript
// 持续订阅步数
sensor.on(sensor.SensorId.STEP_COUNTER, (data: sensor.StepCounterResponse) => {
  console.info('Total steps: ' + data.steps);
});
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.ACCELEROMETER` | 加速度传感器 |
| `ohos.permission.GYROSCOPE` | 陀螺仪 |
| `ohos.permission.ACTIVITY_BASED_MOTION` | 计步/运动 |

---

## 官方参考

- 传感器开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/sensor-V5
- 传感器 ArkTS API：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sensor-V5
