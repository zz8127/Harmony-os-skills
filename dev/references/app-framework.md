# 应用框架 — Stage模型

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## Stage模型概述

Stage模型是HarmonyOS主推的应用模型，从API 9开始支持。相比FA模型，Stage模型支持模块化开发、资源分配管控、应用组件跨设备迁移。

### 构成要素

- **应用组件**：UIAbility、ExtensionAbility
- **应用进程模型**：进程创建与销毁方式
- **应用线程模型**：主线程/TaskPool/Worker
- **应用配置文件**：app.json5 + module.json5

---

## UIAbility组件

UIAbility是包含UI的应用组件，是系统调度的基本单元。

### UIAbility生命周期

```
Create（创建）
  → onCreate()     // 首次创建时调用
  → onWindowStageCreate()  // 窗口创建时调用
    → Foreground（前台可见）
    → Background（后台不可见）
  → onWindowStageDestroy()  // 窗口销毁时调用
  → onDestroy()    // 销毁时调用
```

### 基本用法

```typescript
import UIAbility from '@ohos.app.ability.UIAbility'

export default class EntryAbility extends UIAbility {
  onCreate(want, launchParam) {
    console.info('Ability onCreate')
  }

  onWindowStageCreate(windowStage) {
    windowStage.loadContent('pages/Index', (err, data) => {
      // 加载完成
    })
  }

  onWindowStageDestroy() {
    // 窗口销毁时调用
  }

  onDestroy() {
    // 应用销毁时调用
  }
}
```

### UIAbility启动模式

| 模式 | 说明 | 触发条件 |
|------|------|----------|
| singleton | 默认，单例模式 | 多次启动复用一个实例 |
| multiton | 多实例模式 | 每次启动创建新实例 |
| specified | 指定模式 | 由AbilityStage决定是否创建新实例 |

### API 14+ 新增：UIAbility备份恢复

```typescript
// 支持UIAbility整体备份和恢复
// 需在module.json5中配置backup配置
```

### API 14+ 新增：多实例唯一标识（应用分身）

```typescript
// 通过Want传递应用分身索引
let want = {
  parameters: {
    'ohos.param.callerAppCloneIndex': appCloneIndex
  }
}
```

---

## AbilityStage组件容器

AbilityStage是Module级别的组件容器，Module首次加载时创建。

```typescript
import AbilityStage from '@ohos.app.ability.AbilityStage'

export default class MyAbilityStage extends AbilityStage {
  onCreate() {
    // Module首次加载前初始化
  }

  onAcceptWant(want) {
    // specified模式下触发
    return 'MyAbilityStage'
  }

  onConfigurationUpdated(env) {
    // 环境配置更新时触发
  }

  onMemoryLevel(level) {
    // 内存级别变化时触发
  }
}
```

---

## module.json5 字段说明（API 14+ 更新）

### 基础配置

| 字段 | 类型 | 说明 |
|------|------|------|
| name | string | 模块名，必须唯一 |
| type | string | entry/feature/har/hsp |
| srcEntry | string | 入口文件路径 |
| description | string | 模块描述（支持$r:string:xxx引用） |
| mainElement | string | 主入口Ability名称 |
| deviceTypes | string[] | 支持的设备类型 |
| deliveryWithInstall | boolean | 是否随应用安装 |
| installationFree | boolean | 是否支持免安装 |
| pages | string | 页面路由配置文件路径 |

### API 14+：HSP支持声明多UIAbility

```json
{
  "module": {
    "type": "hsp",
    "abilities": [
      {
        "name": "MyHspAbility",  // API 14+ 支持在HSP中声明非入口Ability
        "srcEntry": "./ets/hspability/MyHspAbility.ets"
      }
    ]
  }
}
```

### abilities配置

```json
{
  "abilities": [
    {
      "name": "EntryAbility",
      "srcEntry": "./ets/entryability/EntryAbility.ets",
      "description": "$string:EntryAbility_desc",
      "icon": "$media:icon",
      "label": "$string:EntryAbility_label",
      "startWindowIcon": "$media:icon",
      "startWindowBackground": "$color:start_window_background",
      "exported": true,
      "launchType": "singleton"
    }
  ]
}
```

### API 14+：orientationId 必填

**重要**：API 14+ 中，如果应用在自己的业务中构造 `AbilityInfo` 结构体，需要**新增必填属性 `orientationId`**：

```typescript
import window from '@ohos.window'

// 获取当前窗口方向
let orientation = await window.getLastWindow(this.context).getWindowProperties().displayId

// 构造AbilityInfo时需要设置orientationId
let abilityInfo = {
  orientationId: 'landscape', // 或 'portrait' 等具体值
  // ... 其他属性
}
```

此变更已做版本隔离，仅在 `targetSdkVersion >= 5.0.2(14)` 时生效。

---

## Want机制

Want是应用间跳转的信息载体。

### 显式Want（启动指定应用）

```typescript
let want = {
  deviceId: '',
  bundleName: 'com.example.myapp',
  abilityName: 'EntryAbility',
  parameters: {
    // API 14+：应用分身索引
    'ohos.param.callerAppCloneIndex': 1
  }
}
context.startAbility(want)
```

### 隐式Want

在module.json5的skills中声明：

```json
{
  "skills": [
    {
      "entities": ["entity.system.home"],
      "actions": ["action.system.home"],
      "uris": [
        {
          "scheme": "https",
          "host": "www.example.com",
          "path": "detail"
        }
      ]
    }
  ]
}
```

---

## 线程模型

### TaskPool（推荐）

```typescript
import taskpool from '@ohos.taskpool'

@Concurrent
function heavyTask(n: number): number {
  let result = 0
  for (let i = 0; i < n; i++) {
    result += i
  }
  return result
}

taskpool.execute(heavyTask, 100000)
```

### Worker

```typescript
let w = new worker.ThreadWorker('entry/ets/workers/MyWorker.ts')
w.onmessage = (e) => console.info('Result: ' + e.data.result)
w.postMessage({ type: 'start', payload: 1000 })
```
