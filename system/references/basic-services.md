# 基础服务（Basic Services Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 概述

BasicServicesKit 提供窗口管理、系统属性、剪贴板、屏幕亮度、显示信息等基础服务能力，是应用开发中最常用的基础工具集。

## 窗口管理

### 获取主窗口

```typescript
import { window } from '@kit.ArkUI';

let mainWindow: window.Window | undefined = undefined;

window.getLastWindow(getContext(this), (err, data) => {
  if (err.code) {
    console.error('Failed to obtain the window. Cause: ' + err.message);
    return;
  }
  mainWindow = data;
  console.info('Succeeded in obtaining the window.');
});
```

### 设置窗口大小

```typescript
let mainWindow: window.Window = window.findWindow('mainWindow');

mainWindow.resize(720, 1280, (err) => {
  if (err.code) {
    console.error('Resize failed: ' + err.message);
    return;
  }
  console.info('Resize succeeded.');
});
```

### 沉浸式模式

```typescript
import { window } from '@kit.ArkUI';

let mainWindow = window.findWindow('mainWindow');

let sysBarProps: window.SystemBarProperties = {
  statusBarColor: '#00000000',
  statusBarContentColor: '#000000',
  navigationBarColor: '#00000000',
  navigationBarContentColor: '#000000'
};

mainWindow.setWindowSystemBarProperties(sysBarProps);

mainWindow.setWindowLayoutFullScreen(true);
```

### 状态栏控制

```typescript
let mainWindow = window.findWindow('mainWindow');

mainWindow.setSpecificSystemBarEnabled('status', true);
mainWindow.setSpecificSystemBarEnabled('navigation', false);

mainWindow.on('systemBarTintChange', (data: window.SystemBarTintChangeInfo) => {
  console.info('System bar tint changed: ' + JSON.stringify(data));
});
```

### WindowStage 生命周期

```typescript
import { AbilityConstant, UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage): void {
    console.info('onWindowStageCreate');

    windowStage.loadContent('pages/Index', (err, data) => {
      if (err.code) {
        console.error('Load content failed: ' + err.message);
        return;
      }
      console.info('Load content succeeded.');
    });

    windowStage.on('windowStageEvent', (event: window.WindowStageEventType) => {
      console.info('WindowStage event: ' + event);
    });
  }

  onWindowStageDestroy(): void {
    console.info('onWindowStageDestroy');
  }
}
```

## 系统属性

```typescript
import { systemParameter } from '@kit.BasicServicesKit';

let deviceType = systemParameter.getSync('const.ohos.devicetype', 'default');
let osVersion = systemParameter.getSync('const.ohos.fullname.version', 'unknown');

systemParameter.get('const.ohos.releasetype', (err, value) => {
  if (err) {
    console.error('Get system parameter failed: ' + err.message);
    return;
  }
  console.info('Release type: ' + value);
});
```

## 剪贴板

### 写入剪贴板

```typescript
import { pasteboard } from '@kit.BasicServicesKit';
import { BusinessError } from '@kit.BasicServicesKit';

let pasteboardData = pasteboard.createData(pasteboard.MIMETYPE_TEXT_PLAIN, 'Hello HarmonyOS');

let systemPasteboard = pasteboard.getSystemPasteboard();
systemPasteboard.setData(pasteboardData, (err: BusinessError) => {
  if (err) {
    console.error('Failed to set pasteboard data: ' + err.message);
    return;
  }
  console.info('Set pasteboard data succeeded.');
});
```

### 读取剪贴板

```typescript
let systemPasteboard = pasteboard.getSystemPasteboard();
systemPasteboard.getData((err: BusinessError, data: pasteboard.PasteData) => {
  if (err) {
    console.error('Failed to get pasteboard data: ' + err.message);
    return;
  }
  let text = data.getPrimaryText();
  console.info('Pasteboard text: ' + text);
});
```

### 剪贴板变化监听

```typescript
let systemPasteboard = pasteboard.getSystemPasteboard();

systemPasteboard.on('update', () => {
  console.info('Pasteboard content updated.');
});

systemPasteboard.off('update');
```

## 屏幕亮度

```typescript
import { brightness } from '@kit.BasicServicesKit';

brightness.setValue(0.8);

let currentBrightness = brightness.getValue();
console.info('Current brightness: ' + currentBrightness);

brightness.setKeepScreenOn(true, (err) => {
  if (err) {
    console.error('Set keep screen on failed: ' + err.message);
    return;
  }
  console.info('Keep screen on succeeded.');
});
```

## 显示信息

```typescript
import { display } from '@kit.ArkUI';
import { BusinessError } from '@kit.BasicServicesKit';

let displayClass: display.Display | null = null;

display.getDefaultDisplaySync();

display.getAllDisplays((err: BusinessError, data: Array<display.Display>) => {
  if (err) {
    console.error('Get all displays failed: ' + err.message);
    return;
  }
  data.forEach(d => {
    console.info('Display id: ' + d.id + ', width: ' + d.width + ', height: ' + d.height + ', densityDPI: ' + d.densityDPI);
  });
});

display.on('add', (data: number) => {
  console.info('Display added: ' + data);
});

display.on('change', (data: number) => {
  console.info('Display changed: ' + data);
});

display.off('add');
display.off('change');
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.PASTEBOARD_READ` | 读取剪贴板 |
| `ohos.permission.PASTEBOARD_WRITE` | 写入剪贴板 |
| `ohos.permission.GET_WIFI_INFO` | 获取 Wi-Fi 信息（系统属性依赖） |

## API 23 新增能力

### API 注解（@SuppressWarnings）

新增 `@SuppressWarnings` 注解，用于消除 API 产生的告警。在源码中用此注解后，编译时会根据配置的规则来抑制对应警告。

### 免打扰状态查询

新增支持查询免打扰相关功能的开启状态（`@ohos.intelligentscene`）。

---

## 官方参考

- 窗口管理开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-window-stage-V5
- 剪贴板开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pasteboard-V5
- 屏幕亮度：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-brightness-V5
- 显示信息：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-display-V5
- 系统属性：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-system-parameter-V5