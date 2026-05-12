# 其他参考

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 网络请求

### HTTP模块

```typescript
import http from '@ohos.net.http'

let httpRequest = http.createHttp()
httpRequest.request(
  'https://api.example.com/data',
  {
    method: http.RequestMethod.GET,
    header: { 'Content-Type': 'application/json' },
    connectTimeout: 60000,
    readTimeout: 60000
  },
  (err, data) => {
    if (err) {
      console.error(`Error: ${err.code}`)
      return
    }
    console.info(`Result: ${data.result}`)
    httpRequest.destroy()
  }
)
```

### 权限要求

```json
{
  "requestPermissions": [
    {
      "name": "ohos.permission.INTERNET",
      "usedScene": { "abilities": ["EntryAbility"], "when": "always" }
    }
  ]
}
```

---

## 数据存储

### 首选项（Preferences）

```typescript
import dataPreferences from '@ohos.data.preferences'

async function saveData() {
  let prefs = await dataPreferences.getPreferences(getContext(this), 'myPrefs')
  await prefs.put('username', 'john')
  await prefs.flush()
}
```

### API 14+：flushSync同步持久化

```typescript
// API 14+ 新增：将缓存数据同步持久化
import dataPreferences from '@ohos.data.preferences'

async function syncSave() {
  let prefs = await dataPreferences.getPreferences(getContext(this), 'myPrefs')
  await prefs.put('key', 'value')
  await prefs.flushSync()  // 同步持久化（API 14+新增）
}
```

### 关系型数据库（RDB）

API 14+ 新增：
- `StoreConfig` 新增 `cryptoParam` 参数支持自定义加密
- 新增支持创建**可并发事务对象**

```typescript
import relationalStore from '@ohos.data.relationalStore'

const STORE_CONFIG: relationalStore.StoreConfig = {
  name: 'mydb.db',
  securityLevel: relationalStore.SecurityLevel.S1,
  cryptoParam: { /* API 14+ 自定义加密参数 */ }
}
```

---

## UIAbility生命周期

```typescript
export default class EntryAbility extends UIAbility {
  onCreate(want, launchParam) {
    console.info('Ability onCreate')
  }

  onWindowStageCreate(windowStage) {
    windowStage.loadContent('pages/Index')
  }

  onWindowStageDestroy() {
    console.info('WindowStage onDestroy')
  }

  onForeground() {
    // 进入前台
  }

  onBackground() {
    // 进入后台
  }

  onDestroy() {
    console.info('Ability onDestroy')
  }
}
```

---

## AppStorage与LocalStorage

### AppStorage（应用级）

```typescript
import AppStorage from '@ohos.app.ability.AppStorage'

AppStorage.setOrCreate('theme', 'dark')
let theme = AppStorage.get<string>('theme')

// 组件中使用
@StorageProp('theme') theme: string = 'light'
@StorageLink('theme') theme: string = 'dark'
```

### LocalStorage（页面级）

```typescript
let localStorage = new LocalStorage({ 'count': 0 })

@LocalStorageProp('count') count: number = 0
@LocalStorageLink('count') count: number = 0
```

---

## API 14+ 行为变更（适配提醒）

| 变更项 | 条件 | 说明 |
|--------|------|------|
| `orientationId` 必填 | targetSdkVersion ≥ 5.0.2(14) | 构造AbilityInfo时必须设置 |
| blob空数组行为 | targetSdkVersion ≥ 5.0.2(14) | 空Uint8Array插入RDB后，getRow返回空数组而非null |
| `flushSync()` 新增 | API 14+ | Preferences同步持久化接口 |

---

## 常见问题

**Q: 为什么图片无法加载？**
A: 检查路径格式，`$r('app.media.xxx')` 且图片在 `resources/base/media/` 下。

**Q: @State变量改变但UI不更新？**
A: 确保变量在@Component装饰的struct内声明，且在build()外修改。

**Q: HTTP请求返回乱码？**
A: 确保服务端返回UTF-8编码。

**Q: 如何获取字体ID？**
A: `this.config.fontId`（API 14+，在AbilityStage.onConfigurationUpdated中）

---

## 官方文档速查

| 内容 | 链接 |
|------|------|
| 文档中心 | https://developer.huawei.com/consumer/cn/doc/ |
| ArkUI框架 | https://developer.huawei.com/consumer/cn/arkui/ |
| 版本说明 | https://developer.huawei.com/consumer/cn/doc/harmonyos-releases |
| DevEco Studio | https://developer.huawei.com/consumer/cn/develop/devo/studio |
| API参考 | https://developer.huawei.com/consumer/cn/doc/harmonyos-references |
