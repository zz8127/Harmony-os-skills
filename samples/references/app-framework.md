# 应用框架示例（App Framework）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## 核心示例

### Stage 模型基础

| 示例名称 | 说明 | 关键 API |
|---------|------|---------|
| UIAbility 生命周期 | EntryAbility/Stage模型的完整生命周期演示 | UIAbilityContext |
| UIAbility 跨设备流转 | 同一应用在不同设备间无缝迁移 | ContinuationExtraParams（API 22 已废弃→用 `ohos.param.devicebasicinfo` 替代） |
| 多实例支持（API 14+） | 应用分身唯一标识 | callerAppCloneIndex |
| Service Widget | 元服务卡片开发 | FormBindingData |

### 代码示例：UIAbility 生命周期

```typescript
// EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import hilog from '@ohos.hilog';

const TAG = 'EntryAbility';
const DOMAIN = 0xF100;

export default class EntryAbility extends UIAbility {
  onCreate(want, launchParam) {
    hilog.info(DOMAIN, TAG, 'onCreate');
  }

  onDestory() {
    hilog.info(DOMAIN, TAG, 'onDestory');
  }

  onWindowStageCreate(windowStage) {
    // 加载主页面
    windowStage.loadContent('pages/Index', (err) => {
      if (err.code) {
        hilog.error(DOMAIN, TAG, 'Failed to load content');
      }
    });
  }

  onWindowStageDestroy() {
    hilog.info(DOMAIN, TAG, 'onWindowStageDestroy');
  }

  onContinue(wantParam) {
    hilog.info(DOMAIN, TAG, 'onContinue');
  }
}
```

### 代码示例：跨设备流转（API 14+，注意 API 22+ 变更）

```typescript
// 发起流转
import continuationManager from '@ohos.app.ability.continuationManager';

// 注册流转回调
async function registerContinuation() {
  let session = await continuationManager.continueDeviceSession({
    deviceType: 'tablet',
    wantParam: {
      'ohos.param.devicebasicinfo': 'info'
    }
  });
}

// 接收端恢复
onContinue(want, launchParam) {
  // 恢复应用状态
}
```

### 代码示例：多实例标识（API 14+）

```typescript
// 获取当前应用实例索引
import Want from '@ohos.app.ability.Want';

// 在 UIAbility 中获取
let callerCloneIndex = 0;
// 从 want 参数中获取（流转场景）
if (want.parameters) {
  callerCloneIndex = want.parameters['ohos.param.callerAppCloneIndex'];
}
```

### Service Widget（元服务卡片）

```typescript
// widget provider
import FormBindingData from '@ohos.app.ability.FormBindingData';

@Entry
@Component
struct Widget {
  @LocalStorageProp('title') title: string = '标题';
  @LocalStorageProp('count') count: number = 0;

  build() {
    Column() {
      Text(this.title)
        .fontSize(20)
      Text(`${this.count}`)
        .fontSize(48)
    }
    .padding(16)
  }
}
```

## 官方参考

- 官方示例首页：https://developer.huawei.com/consumer/cn/samples/
- Gitee 合集：https://gitee.com/HarmonyOS_Samples
