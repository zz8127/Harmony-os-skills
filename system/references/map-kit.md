# 地图服务（Map Kit）

> HarmonyOS 6.1 / API 23

## 概述

地图服务（Map Kit）提供地图展示、交互、覆盖物绘制、位置追踪等能力，通过 `@kit.MapKit` 引入。支持标准 2D 地图与 3D 城市灯光效果，提供标记点碰撞优先级控制和审图号获取等 API 23 新增特性。

## 地图组件

Map 组件是地图展示的核心 UI 组件，需在页面中声明并绑定控制器。

```typescript
import { MapComponent, mapCommon, map } from '@kit.MapKit';
import { Context } from '@kit.AbilityKit';

@Entry
@Component
struct MapPage {
  private mapController?: map.MapComponentController;
  private context: Context = getContext(this);

  build() {
    Column() {
      MapComponent({ mapOptions: this.getMapOptions() })
        .width('100%')
        .height('100%')
        .onLoad(() => {
          this.mapController = new map.MapComponentController();
        });
    }
  }

  private getMapOptions(): mapCommon.MapOptions {
    return {
      position: { x: 0, y: 0 },
      width: 0,
      height: 0,
      cameraPosition: {
        target: { latitude: 39.9042, longitude: 116.4074 },
        zoom: 12
      }
    };
  }
}
```

## MapComponentController

控制器用于程序化操作地图，包括移动、缩放、获取状态等。

```typescript
import { map } from '@kit.MapKit';

async moveCamera(controller: map.MapComponentController): Promise<void> {
  const position: mapCommon.CameraPosition = {
    target: { latitude: 31.2304, longitude: 121.4737 },
    zoom: 15
  };
  await controller.moveCamera(position);
}

async getCameraPosition(controller: map.MapComponentController): Promise<mapCommon.CameraPosition> {
  return controller.getCameraPosition();
}
```

## 标记点（Marker）

在地图上添加可交互的标记点。

```typescript
import { map, mapCommon } from '@kit.MapKit';

async addMarker(controller: map.MapComponentController): Promise<map.Marker> {
  const markerOptions: mapCommon.MarkerOptions = {
    position: { latitude: 39.9042, longitude: 116.4074 },
    title: '天安门',
    snippet: '北京市东城区',
    icon: $r('app.media.marker_icon'),
    draggable: true,
    alpha: 1.0,
    anchor: { u: 0.5, v: 1.0 }
  };
  return controller.addMarker(markerOptions);
}

async removeMarker(controller: map.MapComponentController, marker: map.Marker): Promise<void> {
  await controller.removeMarker(marker);
}
```

## 圆形/折线/多边形

在地图上绘制圆形、折线和多边形覆盖物。

```typescript
import { map, mapCommon } from '@kit.MapKit';

async addCircle(controller: map.MapComponentController): Promise<map.Circle> {
  const circleOptions: mapCommon.CircleOptions = {
    center: { latitude: 39.9042, longitude: 116.4074 },
    radius: 1000,
    fillColor: 0x440000FF,
    strokeColor: 0xFF0000FF,
    strokeWidth: 5
  };
  return controller.addCircle(circleOptions);
}

async addPolyline(controller: map.MapComponentController): Promise<map.Polyline> {
  const polylineOptions: mapCommon.PolylineOptions = {
    points: [
      { latitude: 39.9042, longitude: 116.4074 },
      { latitude: 39.9142, longitude: 116.4174 },
      { latitude: 39.9242, longitude: 116.4274 }
    ],
    color: 0xFF0000FF,
    width: 8
  };
  return controller.addPolyline(polylineOptions);
}

async addPolygon(controller: map.MapComponentController): Promise<map.Polygon> {
  const polygonOptions: mapCommon.PolygonOptions = {
    points: [
      { latitude: 39.9042, longitude: 116.4074 },
      { latitude: 39.9142, longitude: 116.4174 },
      { latitude: 39.9042, longitude: 116.4274 }
    ],
    fillColor: 0x4400FF00,
    strokeColor: 0xFF00FF00,
    strokeWidth: 3
  };
  return controller.addPolygon(polygonOptions);
}
```

## 3D 地图城市灯光（API 23）

API 23 新增 3D 城市灯光效果，在夜间模式下展示建筑灯光。

```typescript
import { map, mapCommon } from '@kit.MapKit';

async enableCityLights(controller: map.MapComponentController): Promise<void> {
  await controller.set3DEffectEnabled(true);
  await controller.setCityLightsEnabled(true);
}
```

## 审图号（API 23）

API 23 新增审图号获取接口，用于合规展示。

```typescript
import { map } from '@kit.MapKit';

async getApproveNumber(controller: map.MapComponentController): Promise<string> {
  const approveInfo = await controller.getApproveNumber();
  return approveInfo;
}
```

## 标记点碰撞优先级（API 23）

API 23 支持设置标记点碰撞优先级，高优先级标记在重叠时优先显示。

```typescript
import { map, mapCommon } from '@kit.MapKit';

async addMarkerWithPriority(controller: map.MapComponentController): Promise<map.Marker> {
  const markerOptions: mapCommon.MarkerOptions = {
    position: { latitude: 39.9042, longitude: 116.4074 },
    title: '高优先级标记',
    collisionPriority: mapCommon.CollisionPriority.HIGH
  };
  return controller.addMarker(markerOptions);
}
```

## 位置追踪

结合位置服务实现地图位置追踪。

```typescript
import { map, mapCommon } from '@kit.MapKit';
import { geoLocationManager } from '@kit.LocationKit';

async startLocationTracking(controller: map.MapComponentController): Promise<void> {
  const request: geoLocationManager.SingleLocationRequest = {
    latitude: 39.9042,
    longitude: 116.4074,
    maxAccuracy: 100
  };
  const location = await geoLocationManager.getCurrentLocation(request);
  await controller.moveCamera({
    target: { latitude: location.latitude, longitude: location.longitude },
    zoom: 16
  });
}
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.LOCATION` | 精确定位权限 |
| `ohos.permission.APPROXIMATELY_LOCATION` | 粗略定位权限 |

精确定位权限依赖粗略定位权限，需同时申请。在 `module.json5` 中声明：

```json
{
  "requestPermissions": [
    { "name": "ohos.permission.APPROXIMATELY_LOCATION" },
    { "name": "ohos.permission.LOCATION" }
  ]
}
```

## 官方参考

- [Map Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/map-kit-overview-0000001820880889)
- [Map Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/map-0000001774121290)
