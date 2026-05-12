# 数据持久化（ArkData）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## ArkData 概述

ArkData（方舟数据管理，`@kit.ArkData`）为应用提供数据存储、数据管理和数据同步能力：

| 能力 | 说明 |
|------|------|
| 标准化数据定义 | 跨应用、跨设备的统一数据类型标准（UTD + UDMF） |
| 数据存储 | 用户首选项（Preferences）、键值型数据库（KV-Store）、关系型数据库（RelationalStore） |
| 数据管理 | 权限管理、数据备份恢复、数据共享框架（DataShare） |
| 数据同步 | 分布式对象、分布式数据库跨设备同步 |

### 核心模块一览

```typescript
import { preferences } from '@kit.ArkData'
import { relationalStore } from '@kit.ArkData'
import { distributedKVStore } from '@kit.ArkData'
import { dataShare } from '@kit.ArkData'
import { uniformTypeDescriptor as utd } from '@kit.ArkData'
import { unifiedDataChannel } from '@kit.ArkData'
import { sendableRelationalStore } from '@kit.ArkData'
```

---

## 用户首选项（Preferences）

轻量级 Key-Value 配置数据持久化，适合保存用户偏好设置（字体大小、夜间模式开关等）。数据缓存在内存中，读取快；通过 `flush` / `flushSync` 持久化到文件。

### 约束限制

- Key 为 string，非空且长度 ≤ 1024 字节
- Value 为 string 时长度 ≤ 16MB（UTF-8 编码）
- 不支持多进程并发安全
- 建议存储数据不超过 10000 条，否则内存开销大
- 非标准 UTF-8 字符串需用 `Uint8Array` 存储

### 获取 Preferences 实例

```typescript
import { preferences } from '@kit.ArkData'
import { UIAbility } from '@kit.AbilityKit'
import { window } from '@kit.ArkUI'

let dataPreferences: preferences.Preferences | null = null

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: preferences.Options = { name: 'myStore' }
    dataPreferences = preferences.getPreferencesSync(this.context, options)
  }
}
```

异步方式：

```typescript
let options: preferences.Options = { name: 'myStore' }
preferences.getPreferences(this.context, options).then((val) => {
  dataPreferences = val
})
```

### 读写操作

```typescript
if (dataPreferences !== null) {
  if (!dataPreferences.hasSync('startup')) {
    dataPreferences.putSync('startup', 'auto')
  }

  let val = dataPreferences.getSync('startup', 'default')

  dataPreferences.deleteSync('startup')
}
```

特殊字符存储：

```typescript
import { util } from '@kit.ArkTS'

let uInt8Array = new util.TextEncoder().encodeInto("~！@#￥%……&*（）")
dataPreferences.putSync('specialKey', uInt8Array)

let raw: preferences.ValueType = dataPreferences.getSync('specialKey', new Uint8Array(0))
let textDecoder = util.TextDecoder.create('utf-8')
let decoded = textDecoder.decodeToString(raw as Uint8Array)
```

### 异步持久化（flush）

```typescript
import { BusinessError } from '@kit.BasicServicesKit'

dataPreferences.flush((err: BusinessError) => {
  if (err) {
    console.error(`Failed to flush. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in flushing.')
})
```

### API 14+ 同步持久化（flushSync）

```typescript
dataPreferences.flushSync()
```

`flushSync` 将缓存数据同步写入持久化文件，适用于对数据可靠性要求高、可接受短暂阻塞的场景。

### 观察数据变更

```typescript
let observer = (key: string) => {
  console.info(`The key '${key}' changed.`)
}

dataPreferences.on('change', observer)

dataPreferences.put('startup', 'manual', (err: BusinessError) => {
  if (err) {
    console.error(`Failed to put. Code:${err.code}, message:${err.message}`)
    return
  }
  dataPreferences.flush()
})

dataPreferences.off('change', observer)
```

### 删除 Preferences 文件

```typescript
let options: preferences.Options = { name: 'myStore' }
preferences.deletePreferences(this.context, options, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to delete. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in deleting preferences.')
})
```

> 调用 `deletePreferences` 后，订阅自动取消，实例不可再用，数据不可恢复。

---

## 关系型数据库（RelationalStore）

基于 SQLite 的关系型数据库，适用于存储包含复杂关系的数据（学生信息、雇员记录等）。支持事务、索引、视图、触发器、外键、参数化查询和预编译 SQL。

### 约束限制

- 默认 WAL 日志模式，FULL 落盘模式
- 4 个读连接 + 1 个写连接（无空闲读连接时写连接可降级为读连接）
- 同一时间仅支持一个写操作
- ArkTS 侧支持基本数据类型：number、string、二进制、boolean、bigint
- 单条数据建议不超过 2MB
- 单次查询建议不超过 5000 条，大数据量请在 TaskPool 中查询

### 创建数据库

```typescript
import { relationalStore } from '@kit.ArkData'
import { UIAbility } from '@kit.AbilityKit'
import { window } from '@kit.ArkUI'

let store: relationalStore.RdbStore | undefined = undefined

const STORE_CONFIG: relationalStore.StoreConfig = {
  name: 'RdbTest.db',
  securityLevel: relationalStore.SecurityLevel.S3,
  encrypt: false,
  customDir: 'customDir/subCustomDir',
  isReadOnly: false
}

const SQL_CREATE_TABLE = 'CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB, IDENTITY UNLIMITED INT)'

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    relationalStore.getRdbStore(this.context, STORE_CONFIG, (err, rdbStore) => {
      if (err) {
        console.error(`Failed to get RdbStore. Code:${err.code}, message:${err.message}`)
        return
      }
      store = rdbStore
      if (store.version === 0) {
        store.executeSql(SQL_CREATE_TABLE)
        store.version = 3
      }
      if (store.version === 1) {
        store.executeSql('ALTER TABLE EMPLOYEE ADD COLUMN AGE INTEGER')
        store.version = 2
      }
      if (store.version === 2) {
        store.executeSql('ALTER TABLE EMPLOYEE DROP COLUMN ADDRESS TEXT')
        store.version = 3
      }
    })
  }
}
```

### 安全级别

| 级别 | 说明 |
|------|------|
| S1 | 低级别，数据泄露后影响小 |
| S2 | 一般级别 |
| S3 | 较高级别，数据泄露后影响较大 |
| S4 | 最高级别，核心机密数据 |

### 插入数据

```typescript
import { BusinessError } from '@kit.BasicServicesKit'

const valueBucket: relationalStore.ValuesBucket = {
  NAME: 'Lisa',
  AGE: 18,
  SALARY: 100.5,
  CODES: new Uint8Array([1, 2, 3, 4, 5]),
  IDENTITY: BigInt('15822401018187971961171')
}

if (store !== undefined) {
  (store as relationalStore.RdbStore).insert('EMPLOYEE', valueBucket, (err: BusinessError, rowId: number) => {
    if (err) {
      console.error(`Failed to insert. Code:${err.code}, message:${err.message}`)
      return
    }
    console.info(`Succeeded in inserting data. rowId:${rowId}`)
  })
}
```

### 查询数据

```typescript
let predicates = new relationalStore.RdbPredicates('EMPLOYEE')
predicates.equalTo('NAME', 'Rose')

if (store !== undefined) {
  (store as relationalStore.RdbStore).query(predicates, ['ID', 'NAME', 'AGE', 'SALARY', 'IDENTITY'], (err: BusinessError, resultSet) => {
    if (err) {
      console.error(`Failed to query. Code:${err.code}, message:${err.message}`)
      return
    }
    while (resultSet.goToNextRow()) {
      const id = resultSet.getLong(resultSet.getColumnIndex('ID'))
      const name = resultSet.getString(resultSet.getColumnIndex('NAME'))
      const age = resultSet.getLong(resultSet.getColumnIndex('AGE'))
      const salary = resultSet.getDouble(resultSet.getColumnIndex('SALARY'))
      const identity = resultSet.getValue(resultSet.getColumnIndex('IDENTITY'))
      console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}, identity=${identity}`)
    }
    resultSet.close()
  })
}
```

### 更新数据

```typescript
const updateBucket: relationalStore.ValuesBucket = {
  NAME: 'Rose',
  AGE: 22,
  SALARY: 200.5,
  CODES: new Uint8Array([1, 2, 3, 4, 5]),
  IDENTITY: BigInt('15822401018187971967863')
}

let predicates = new relationalStore.RdbPredicates('EMPLOYEE')
predicates.equalTo('NAME', 'Lisa')

if (store !== undefined) {
  (store as relationalStore.RdbStore).update(updateBucket, predicates, (err: BusinessError, rows: number) => {
    if (err) {
      console.error(`Failed to update. Code:${err.code}, message:${err.message}`)
      return
    }
    console.info(`Updated rows: ${rows}`)
  })
}
```

### 删除数据

```typescript
let predicates = new relationalStore.RdbPredicates('EMPLOYEE')
predicates.equalTo('NAME', 'Lisa')

if (store !== undefined) {
  (store as relationalStore.RdbStore).delete(predicates, (err: BusinessError, rows: number) => {
    if (err) {
      console.error(`Failed to delete. Code:${err.code}, message:${err.message}`)
      return
    }
    console.info(`Deleted rows: ${rows}`)
  })
}
```

### 执行 SQL 语句

```typescript
if (store !== undefined) {
  (store as relationalStore.RdbStore).executeSql('ALTER TABLE EMPLOYEE ADD COLUMN ADDRESS TEXT')
}
```

### RdbPredicates 常用条件

| 方法 | 说明 |
|------|------|
| `equalTo(field, value)` | 等于 |
| `notEqualTo(field, value)` | 不等于 |
| `greaterThan(field, value)` | 大于 |
| `lessThan(field, value)` | 小于 |
| `between(field, low, high)` | 区间 |
| `like(field, value)` | 模糊匹配（%通配） |
| `in(field, values)` | 在列表中 |
| `orderByAsc(field)` | 升序 |
| `orderByDesc(field)` | 降序 |
| `limitAs(count)` | 限制条数 |
| `offsetAs(offset)` | 偏移量 |

### API 14+ 数据库加密（cryptoParam）

```typescript
const STORE_CONFIG_ENCRYPTED: relationalStore.StoreConfig = {
  name: 'EncryptedDb.db',
  securityLevel: relationalStore.SecurityLevel.S4,
  encrypt: true,
  cryptoParam: {
    iteration: 10000,
    keySize: 32
  }
}
```

`cryptoParam` 用于自定义加密参数，仅在 `encrypt: true` 时生效。

### API 12+ 并发事务对象（sendableRelationalStore）

`@ohos.data.sendableRelationalStore` 提供可跨线程传递的数据库操作对象，支持 TaskPool 并发场景：

```typescript
import { sendableRelationalStore } from '@kit.ArkData'

const valuesBucket: sendableRelationalStore.NonSendableBucket = {
  age: 18,
  name: 'hangman',
  salary: 100.5,
  passed: true,
  blobType: new Uint8Array([1, 2, 3]),
  bigValue: BigInt('15822401018187971961171')
}

const sendableBucket = sendableRelationalStore.toSendableValuesBucket(valuesBucket)

const normalBucket = sendableRelationalStore.fromSendableValuesBucket(sendableBucket)
```

核心转换方法：

| 方法 | 说明 |
|------|------|
| `toSendableValuesBucket(bucket)` | 转为可跨线程传递的 ValuesBucket |
| `fromSendableValuesBucket(bucket)` | 从可跨线程的 ValuesBucket 转回普通对象 |
| `toSendableAsset(asset)` | 转为可跨线程传递的 Asset |
| `fromSendableAsset(asset)` | 从可跨线程的 Asset 转回普通对象 |

### 备份与恢复

#### 手动备份

```typescript
if (store !== undefined) {
  (store as relationalStore.RdbStore).backup('Backup.db', (err: BusinessError) => {
    if (err) {
      console.error(`Failed to backup. Code:${err.code}, message:${err.message}`)
      return
    }
    console.info('Succeeded in backing up RdbStore.')
  })
}
```

#### 恢复数据

```typescript
if (store !== undefined) {
  (store as relationalStore.RdbStore).restore('Backup.db', (err: BusinessError) => {
    if (err) {
      console.error(`Failed to restore. Code:${err.code}, message:${err.message}`)
      return
    }
    console.info('Succeeded in restoring RdbStore.')
  })
}
```

#### 异常重建（allowRebuild）

数据库抛出错误码 `14800011` 时，表示数据库异常。需在 `StoreConfig` 中配置 `allowRebuild: true`，异常时自动删库重建：

```typescript
const STORE_CONFIG: relationalStore.StoreConfig = {
  name: 'RdbTest.db',
  securityLevel: relationalStore.SecurityLevel.S3,
  allowRebuild: true
}
```

重建后为空库，需重新建表并使用备份数据恢复。

### 删除数据库

```typescript
relationalStore.deleteRdbStore(this.context, 'RdbTest.db', (err) => {
  if (err) {
    console.error(`Failed to delete RdbStore. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in deleting RdbStore.')
})
```

---

## 键值型数据库（KV-Store）

分布式键值型数据库，支持跨设备数据同步。适用于数据结构简单、需要分布式同步的场景。

### 创建数据库

```typescript
import { distributedKVStore } from '@kit.ArkData'

let kvManager: distributedKVStore.KVManager
let kvStore: distributedKVStore.SingleKVStore | undefined = undefined

const kvManagerConfig: distributedKVStore.KVManagerConfig = {
  context: getContext(this),
  bundleName: 'com.example.myapp'
}

kvManager = distributedKVStore.createKVManager(kvManagerConfig)

const options: distributedKVStore.Options = {
  createIfMissing: true,
  encrypt: true,
  backup: false,
  autoSync: false,
  kvStoreType: distributedKVStore.KVStoreType.SINGLE_VERSION,
  securityLevel: distributedKVStore.SecurityLevel.S1
}

kvManager.getKVStore<distributedKVStore.SingleKVStore>('storeId', options, (err, store) => {
  if (err) {
    console.error(`Failed to get KVStore. Code:${err.code}, message:${err.message}`)
    return
  }
  kvStore = store
})
```

### 读写操作

```typescript
kvStore.put('key_test_string', 'value_test_string', (err) => {
  if (err) {
    console.error(`Failed to put. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in putting data.')
})

kvStore.get('key_test_string', (err, data) => {
  if (err) {
    console.error(`Failed to get. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info(`Got data: ${data}`)
})

kvStore.delete('key_test_string', (err) => {
  if (err) {
    console.error(`Failed to delete. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in deleting data.')
})
```

### 备份与恢复

```typescript
kvStore.backup('BK001', (err) => {
  if (err) {
    console.error(`Failed to backup. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in backing up data.')
})

kvStore.restore('BK001', (err) => {
  if (err) {
    console.error(`Failed to restore. Code:${err.code}, message:${err.message}`)
    return
  }
  console.info('Succeeded in restoring data.')
})

let files = ['BK001']
kvStore.deleteBackup(files).then((data) => {
  console.info(`Deleted backup. filename: ${data[0]}, result: ${data[1]}`)
})
```

---

## 跨应用数据共享（DataShare）

DataShare 提供 provider-consumer 模式的跨应用数据共享能力，支持静默数据访问（不拉起 provider，通过 DatamgrService 代理访问）。

### 数据提供方（Provider）

通过 `DataShareExtensionAbility` 实现数据提供：

```typescript
import { DataShareExtensionAbility } from '@kit.ArkData'
import { relationalStore } from '@kit.ArkData'

export default class DataShareExtAbility extends DataShareExtensionAbility {
  onCreate() {
    return true
  }

  insert(uri: string, valueBucket: relationalStore.ValuesBucket, callback: (err, result) => void) {
    callback(null, 1)
  }

  query(uri: string, predicates, columns, callback) {
    callback(null, resultSet)
  }

  update(uri: string, valueBucket, predicates, callback) {
    callback(null, 1)
  }

  delete(uri: string, predicates, callback) {
    callback(null, 1)
  }
}
```

### 数据消费方（Consumer）

```typescript
import { dataShare } from '@kit.ArkData'
import { dataSharePredicates } from '@kit.ArkData'

let uris = ['datashareproxy://com.example.dataprovider/entry/DB/TBL']
let dataShareHelper = dataShare.createDataShareHelper(this.context, uris[0])

let predicates = new dataSharePredicates.DataSharePredicates()
predicates.equalTo('name', 'test')

let columns = ['id', 'name', 'age']
dataShareHelper.query(uris[0], predicates, columns).then((resultSet) => {
  while (resultSet.goToNextRow()) {
    console.info(`id: ${resultSet.getLong(0)}, name: ${resultSet.getString(1)}`)
  }
  resultSet.close()
})
```

### module.json5 配置

```json
{
  "extensionAbilities": [
    {
      "name": "DataShareExtAbility",
      "srcEntry": "./ets/datashareextability/DataShareExtAbility.ets",
      "type": "dataShare",
      "exported": true,
      "metadata": [
        {
          "name": "ohos.extension.dataShare",
          "resource": "$profile:data_share_config"
        }
      ]
    }
  ]
}
```

---

## 统一数据管理框架（UDMF）

UDMF 定义了跨应用、跨设备数据交互的标准数据语言和通路，提升数据交互效率。

### 核心概念

- **标准化数据类型（UTD）**：`uniformTypeDescriptor`，定义统一的数据类型标识
- **标准化数据结构**：`unifiedDataChannel`，提供标准化的数据通路
- **ContentForm**（API 14+）：内容卡片类型数据结构，用于跨应用传递卡片化内容

### UTD 使用

```typescript
import { uniformTypeDescriptor as utd } from '@kit.ArkData'

let typeObj = utd.getUniformDataTypeByFilenameExtension('txt')
let typeObj2 = utd.getUniformDataTypeByMIMEType('text/plain')
```

### 数据通路

```typescript
import { unifiedDataChannel } from '@kit.ArkData'
import { uniformTypeDescriptor as utd } from '@kit.ArkData'

let plainText = new unifiedDataChannel.PlainText()
plainText.textContent = 'Hello HarmonyOS'
plainText.abstract = 'Greeting'

let unifiedData = new unifiedDataChannel.UnifiedData(plainText)

let summary = unifiedData.getSummary()
```

### API 14+ ContentForm 数据结构

ContentForm 用于跨应用传递内容卡片数据：

```typescript
import { unifiedDataChannel } from '@kit.ArkData'

let contentForm = new unifiedDataChannel.ContentForm()
contentForm.title = 'News Title'
contentForm.content = 'News content summary...'
contentForm.description = 'Brief description'

let unifiedData = new unifiedDataChannel.UnifiedData(contentForm)
```

---

## 数据迁移

### 应用数据备份恢复框架

HarmonyOS 提供应用数据备份恢复框架，通过 `BackupExtensionAbility` 实现应用升级、迁移场景下的数据保留。

### BackupExtensionAbility

```typescript
import { BackupExtensionAbility } from '@kit.ApplicationFrameworkKit'

export default class BackupExtension extends BackupExtensionAbility {
  onBackup() {
    console.info('onBackup invoked')
  }

  onRestore(bundleVersion: string) {
    console.info(`onRestore invoked, bundleVersion: ${bundleVersion}`)
  }
}
```

### module.json5 配置

```json
{
  "extensionAbilities": [
    {
      "name": "BackupExtension",
      "srcEntry": "./ets/backup/BackupExtension.ets",
      "type": "backup",
      "exported": false,
      "metadata": [
        {
          "name": "ohos.extension.backup",
          "resource": "$profile:backup_config"
        }
      ]
    }
  ]
}
```

### 数据迁移场景

| 场景 | 说明 |
|------|------|
| HarmonyOS → HarmonyOS NEXT | APK 应用数据迁移至原生应用，通过备份恢复框架自动处理 |
| 应用升级 | 版本升级后数据结构变更，通过 `onRestore` 中 `bundleVersion` 判断并转换 |
| 跨设备迁移 | 通过分布式能力同步数据 |

### 数据库版本升级示例

```typescript
if (store.version === 0) {
  store.executeSql('CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER)')
  store.version = 1
}
if (store.version === 1) {
  store.executeSql('ALTER TABLE EMPLOYEE ADD COLUMN SALARY REAL')
  store.version = 2
}
if (store.version === 2) {
  store.executeSql('ALTER TABLE EMPLOYEE ADD COLUMN IDENTITY UNLIMITED INT')
  store.version = 3
}
```

---

## 官方参考链接

| 主题 | 链接 |
|------|------|
| ArkData 简介 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-mgmt-overview-V5 |
| 用户首选项 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-persistence-by-preferences-V5 |
| 用户首选项 API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-data-preferences-V5 |
| 关系型数据库 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-persistence-by-rdb-store-V5 |
| 关系型数据库 API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-data-relationalstore-V5 |
| 共享关系型数据库 API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-data-sendablerelationalstore-V5 |
| 键值型数据库 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-persistence-by-kv-store-V5 |
| 数据库备份与恢复 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-backup-and-restore-V5 |
| 跨应用数据共享 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/cross-app-data-share-V5 |
| 标准化数据定义 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/uniform-data-definition-V5 |
| UDMF API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-data-unifieddatachannel-V5 |
| 数据加密 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/data-encryption-V5 |
| 应用数据迁移 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/application-data-migration-V5 |
| 首选项示例代码 | https://gitee.com/harmonyos_samples/preferences |
