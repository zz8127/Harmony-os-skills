# 搴旂敤鏋舵瀯涓庤川閲?
> **閫傜敤鐗堟湰**锛欻armonyOS 6.1 / API 23锛堢ǔ瀹氾級銆傚吋瀹?API 14+銆?
## 姒傝堪

鏈枃妗ｆ兜鐩栦袱閮ㄥ垎鍐呭锛?*搴旂敤鏋舵瀯**锛堝垎灞傛灦鏋勩€佹ā鍧楀寲璁捐銆佸苟鍙戣璁°€丄OP 璁捐锛夊拰**搴旂敤璐ㄩ噺**锛堟€ц兘浼樺寲銆佸姛鑰椾紭鍖栥€佸畨鍏ㄧ紪鐮併€丏FX锛夛紝甯姪寮€鍙戣€呮瀯寤哄彲缁存姢銆侀珮鎬ц兘銆佸畨鍏ㄧ殑 HarmonyOS 搴旂敤銆?
---

# 绗竴閮ㄥ垎锛氬簲鐢ㄦ灦鏋?
## 鍒嗗眰鏋舵瀯锛圲I / Domain / Data锛?
### 涓夊眰鏋舵瀯姒傝

```
鈹屸攢鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹?鈹?     UI Layer           鈹? 鈫?ArkUI 椤甸潰/缁勪欢銆乂iewModel
鈹溾攢鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹?鈹?     Domain Layer       鈹? 鈫?涓氬姟閫昏緫銆佺敤渚嬶紙UseCase锛?鈹溾攢鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹?鈹?     Data Layer         鈹? 鈫?鏁版嵁浠撳簱銆佺綉缁滆姹傘€佹湰鍦板瓨鍌?鈹斺攢鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹€鈹?```

### UI 灞?
```typescript
@Entry
@Component
struct UserListPage {
  @State userList: User[] = [];
  private viewModel: UserListViewModel = new UserListViewModel();

  aboutToAppear() {
    this.viewModel.loadUsers().then(users => {
      this.userList = users;
    });
  }

  build() {
    List() {
      ForEach(this.userList, (user: User) => {
        ListItem() {
          UserItem({ user: user })
        }
      }, (user: User) => user.id.toString())
    }
  }
}
```

### Domain 灞?
```typescript
export class GetUsersUseCase {
  private userRepository: UserRepository;

  constructor(repository: UserRepository) {
    this.userRepository = repository;
  }

  execute(): Promise<User[]> {
    return this.userRepository.getUsers();
  }
}
```

### Data 灞?
```typescript
import { http } from '@kit.NetworkKit';

export interface UserRepository {
  getUsers(): Promise<User[]>;
}

export class UserRepositoryImpl implements UserRepository {
  async getUsers(): Promise<User[]> {
    let response = await http.request('https://api.example.com/users', {
      method: http.RequestMethod.GET,
      header: { 'Content-Type': 'application/json' }
    });
    return JSON.parse(response.result as string) as User[];
  }
}
```

## 妯″潡鍖栬璁★紙HAR / HSP锛?
### HAR锛堥潤鎬佸叡浜寘锛?
```json5
// oh-package.json5锛圚AR 妯″潡锛?{
  "name": "shared-utils",
  "version": "1.0.0",
  "main": "Index.ets"
}
```

```typescript
// Index.ets锛圚AR 瀵煎嚭锛?export { StringUtils } from './src/main/ets/utils/StringUtils';
export { DateUtils } from './src/main/ets/utils/DateUtils';
```

### HSP锛堝姩鎬佸叡浜寘锛?
```json5
// oh-package.json5锛圚SP 妯″潡锛?{
  "name": "feature-payment",
  "version": "1.0.0",
  "main": "Index.ets"
}
```

```typescript
// Index.ets锛圚SP 瀵煎嚭锛?export { PaymentPage } from './src/main/ets/pages/PaymentPage';
export { PaymentService } from './src/main/ets/service/PaymentService';
```

### 妯″潡寮曠敤

```json5
// oh-package.json5锛堜富妯″潡锛?{
  "dependencies": {
    "shared-utils": "file:../shared_utils",
    "feature-payment": "file:../feature_payment"
  }
}
```

## 骞跺彂璁捐

### TaskPool锛堢嚎绋嬫睜锛?
```typescript
import { taskpool } from '@kit.ArkTS';

@Concurrent
function computeHeavyTask(data: number[]): number {
  let sum = 0;
  for (let i = 0; i < data.length; i++) {
    sum += data[i] * data[i];
  }
  return sum;
}

let task = new taskpool.Task(computeHeavyTask, [1, 2, 3, 4, 5]);

taskpool.execute(task).then((result: number) => {
  console.info('Task result: ' + result);
}).catch((err: Error) => {
  console.error('Task failed: ' + err.message);
});
```

### Worker锛堢嫭绔嬬嚎绋嬶級

```typescript
// 涓荤嚎绋?import { worker } from '@kit.ArkTS';

let workerInstance = new worker.ThreadWorker('entry/ets/workers/DataWorker.ets');

workerInstance.onmessage = (event: MessageEvents) => {
  console.info('Worker result: ' + event.data);
};

workerInstance.postMessage({ action: 'process', payload: [1, 2, 3] });

workerInstance.terminate();
```

```typescript
// DataWorker.ets
import { worker, MessageEvents } from '@kit.ArkTS';

let workerHandler = worker.workerHandler;

workerHandler.onmessage = (event: MessageEvents) => {
  let data = event.data.payload as number[];
  let result = data.reduce((sum, val) => sum + val * val, 0);
  workerHandler.postMessage(result);
};
```

### TaskPool vs Worker 閫夋嫨

| 鐗规€?| TaskPool | Worker |
|------|----------|--------|
| 绾跨▼绠＄悊 | 鑷姩绠＄悊 | 鎵嬪姩鍒涘缓/閿€姣?|
| 浠诲姟鏁伴噺 | 鏀寔澶氫换鍔℃帓闃?| 鍗曚换鍔′覆琛?|
| 鐢熷懡鍛ㄦ湡 | 闅忎换鍔＄粨鏉?| 闇€鎵嬪姩 terminate |
| 閫傜敤鍦烘櫙 | 鐭椂璁＄畻浠诲姟 | 闀挎椂杩愯浠诲姟 |

## AOP 璁捐

```typescript
import { Aspect } from '@kit.ArkTS';

class PerformanceAspect {
  @Aspect.before('com.example.myapp.UserService.login')
  beforeLogin() {
    console.info('[AOP] Before login - start timing');
  }

  @Aspect.after('com.example.myapp.UserService.login')
  afterLogin() {
    console.info('[AOP] After login - end timing');
  }

  @Aspect.around('com.example.myapp.UserService.login')
  aroundLogin(joinPoint: Aspect.JoinPoint) {
    console.info('[AOP] Around - before proceed');
    let result = joinPoint.proceed();
    console.info('[AOP] Around - after proceed');
    return result;
  }
}
```

---

# 绗簩閮ㄥ垎锛氬簲鐢ㄨ川閲?
## 鎬ц兘浼樺寲

### 鎳掑姞杞斤紙LazyForEach锛?
```typescript
class MyDataSource implements IDataSource {
  private dataList: string[] = [];

  totalCount(): number {
    return this.dataList.length;
  }

  getData(index: number): string {
    return this.dataList[index];
  }

  registerDataChangeListener(listener: DataChangeListener): void {}
  unregisterDataChangeListener(listener: DataChangeListener): void {}
}

@Entry
@Component
struct LazyLoadPage {
  private dataSource: MyDataSource = new MyDataSource();

  build() {
    List() {
      LazyForEach(this.dataSource, (item: string) => {
        ListItem() {
          Text(item).height(80)
        }
      }, (item: string) => item)
    }
    .cachedCount(5)
  }
}
```

### 缁勪欢澶嶇敤锛園Reusable锛?
```typescript
@Reusable
@Component
struct ReusableItem {
  @State title: string = '';

  aboutToReuse(params: Record<string, Object>) {
    this.title = params.title as string;
  }

  build() {
    Row() {
      Text(this.title)
    }
    .height(60)
  }
}
```

### 鐘舵€佺鐞嗕紭鍖?
```typescript
@ObservedV2
class UserInfo {
  @Trace name: string = '';
  @Trace age: number = 0;
}

@Entry
@ComponentV2
struct StateOptPage {
  @Local user: UserInfo = new UserInfo();

  build() {
    Column() {
      Text(this.user.name)
      Button('Update Name')
        .onClick(() => {
          this.user.name = 'New Name';
        })
    }
  }
}
```

### 鎸夐渶鍔犺浇

```typescript
import { router } from '@kit.ArkUI';

Button('Go to Detail')
  .onClick(() => {
    router.pushUrl({
      url: 'pages/DetailPage'
    });
  });
```

## 鍔熻€椾紭鍖?
### 鍚庡彴浠诲姟绠＄悊

```typescript
import { backgroundTaskManager } from '@kit.BackgroundTasksKit';

let bgMode: backgroundTaskManager.BackgroundMode = backgroundTaskManager.BackgroundMode.DATA_TRANSFER;

backgroundTaskManager.requestSuspendDelay('DataSync', () => {
  console.info('Suspend delay callback.');
});
```

### 闀挎椂浠诲姟

```typescript
import { backgroundTaskManager } from '@kit.BackgroundTasksKit';
import { wantAgent } from '@kit.AbilityKit';

let wantAgentInfo: wantAgent.WantAgentInfo = {
  wants: [{ bundleName: 'com.example.myapp', abilityName: 'EntryAbility' }],
  requestCode: 0,
  wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

let agent = await wantAgent.getWantAgent(wantAgentInfo);

backgroundTaskManager.startBackgroundRunning(getContext(this),
  backgroundTaskManager.BackgroundMode.LOCATION, agent);
```

### 鍋滄闀挎椂浠诲姟

```typescript
backgroundTaskManager.stopBackgroundRunning(getContext(this));
```

### 纭欢璧勬簮绠＄悊

```typescript
import { sensor } from '@kit.SensorServiceKit';

aboutToAppear() {
  sensor.on(sensor.SensorId.ACCELEROMETER, (data) => {
    console.info('Accelerometer: ' + data.x);
  });
}

aboutToDisappear() {
  sensor.off(sensor.SensorId.ACCELEROMETER);
}
```

## 瀹夊叏缂栫爜

### 杈撳叆鏍￠獙

```typescript
function validateInput(input: string): boolean {
  if (!input || input.trim().length === 0) {
    return false;
  }
  let pattern = /^[a-zA-Z0-9_@.]+$/;
  return pattern.test(input);
}

function sanitizeHtml(html: string): string {
  return html.replace(/<[^>]*>/g, '');
}
```

### 鏁版嵁鍔犲瘑

```typescript
import { huks } from '@kit.UniversalKeystoreKit';

async function encryptData(plainText: string): Promise<Uint8Array> {
  let encoder = new util.TextEncoder();
  let data = encoder.encodeInto(plainText);

  let encryptProperties: Array<huks.HuksParam> = [
    { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
    { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT },
    { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PKCS7 },
    { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_CBC },
    { tag: huks.HuksTag.HUKS_TAG_IV, value: new Uint8Array(16) }
  ];

  let options: huks.HuksOptions = { properties: encryptProperties, inData: data };
  let initResult = await huks.initSession('my_aes_key', options);
  let finishResult = await huks.finishSession(initResult.handle, options);
  return finishResult.outData;
}
```

### 浠ｇ爜娣锋穯

```json5
// build-profile.json5
{
  "app": {
    "products": [
      {
        "name": "default",
        "signingConfig": "default",
        "obfuscation": {
          "enable": true,
          "rules": {
            "rename": true,
            "removeLog": true,
            "removeComments": true
          }
        }
      }
    ]
  }
}
```

## DFX锛堝彲瑙傛祴鎬э級

### HiLog锛堟棩蹇楋級

```typescript
import { hilog } from '@kit.PerformanceAnalysisKit';

let DOMAIN = 0x0001;
let TAG = 'MyApp';

hilog.info(DOMAIN, TAG, 'Application started.');
hilog.debug(DOMAIN, TAG, 'Debug value: %{public}d', 42);
hilog.warn(DOMAIN, TAG, 'Warning: low memory');
hilog.error(DOMAIN, TAG, 'Error: network timeout');

hilog.info(DOMAIN, TAG, 'Private data: %{private}s', 'sensitive_info');
hilog.info(DOMAIN, TAG, 'Public data: %{public}s', 'visible_info');
```

### HiAppEvent锛堝簲鐢ㄤ簨浠舵墦鐐癸級

```typescript
import { hiAppEvent } from '@kit.PerformanceAnalysisKit';

hiAppEvent.write({
  domain: 'my_app',
  name: 'user_login',
  eventType: hiAppEvent.EventType.BEHAVIOR,
  params: {
    user_id: '12345',
    login_method: 'password',
    result: 'success'
  }
});

hiAppEvent.configure({
  disable: false,
  maxStorage: '10M'
});
```

### HiChecker锛堝紑鍙戞湡妫€娴嬶級

```typescript
import { hichecker } from '@kit.PerformanceAnalysisKit';

hichecker.addRule(hichecker.RULE_CHECK_ABILITY_CHAIN_CONNECT);
hichecker.addRule(hichecker.RULE_CHECK_COMPONENT_SECURE);

hichecker.on('checkerEvent', (rule: number, detailInfo: string) => {
  console.warn('HiChecker violation: ' + detailInfo);
});

hichecker.removeRule(hichecker.RULE_CHECK_ABILITY_CHAIN_CONNECT);
```

## 鏉冮檺

鏈弬鑰冩枃妗ｆ秹鍙婄殑鑳藉姏鎵€闇€鏉冮檺宸插湪鍚?Kit 涓撳睘鍙傝€冩枃浠朵腑鍒楀嚭銆?
---

## 瀹樻柟鍙傝€?
- 搴旂敤鏋舵瀯璁捐锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-application-architecture-V5
- HAR/HSP 寮€鍙戯細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/har-package-V5
- TaskPool 骞跺彂锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/taskpool-V5
- Worker 骞跺彂锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/worker-V5
- 鎬ц兘浼樺寲锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-performance-V5
- 鍔熻€椾紭鍖栵細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-usage-statistics-V5
- 瀹夊叏缂栫爜锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/security-overview-V5
- HiLog锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-hilog-V5
- HiAppEvent锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-hiappevent-V5
- HiChecker锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-hichecker-V5