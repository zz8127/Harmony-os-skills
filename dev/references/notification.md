# 通知服务（Notification Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Notification Kit（`@kit.NotificationKit`）为开发者提供本地通知发布通道，可将应用产生的通知直接在客户端本地推送给用户。本地通知根据通知类型及发布场景会产生对应的铃声、震动、横幅、锁屏、息屏、通知栏提醒和显示。

**核心能力**：
- 发布文本、进度条等类型通知
- 携带或更新应用通知数字角标
- 取消某条或全部已发布通知
- 查询已发布通知列表
- 查询应用通知开关状态
- 请求用户授权发布通知

**约束限制**：
- 单个应用已发布通知在通知中心留存最多24条
- 通知长度不超过200KB
- 单个应用发布新通知频次不超过每秒10条，更新通知频次不超过每秒20条
- 所有三方应用发布新通知频次累计不超过每秒15条，更新通知频次累计不超过每秒30条

**业务流程**：

```
请求通知授权 → 应用发布通知到通知服务 → 通知展示到通知中心
```

---

## 请求通知授权

应用需要获取用户授权才能发送通知。首次调用 `requestEnableNotification()` 弹窗让用户选择是否允许。用户拒绝后无法再次弹窗，需使用 `openNotificationSettings()` 拉起通知管理半模态弹窗。

### 接口说明

| 接口名 | 说明 |
|--------|------|
| isNotificationEnabled(): Promise\<boolean\> | 查询通知是否授权 |
| requestEnableNotification(context: UIAbilityContext): Promise\<void\> | 请求通知授权（首次弹窗） |
| openNotificationSettings(context: UIAbilityContext): Promise\<void\> | 拉起通知管理弹窗（API 13+） |

### 代码示例

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { common } from '@kit.AbilityKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function requestNotificationPermission(context: common.UIAbilityContext): Promise<void> {
  let enabled = await notificationManager.isNotificationEnabled()
  if (!enabled) {
    try {
      await notificationManager.requestEnableNotification(context)
    } catch (err) {
      let e = err as BusinessError
      if (e.code === 1600004) {
        await notificationManager.openNotificationSettings(context)
      }
    }
  }
}
```

---

## 发布通知

### 创建 NotificationRequest

`NotificationRequest` 是通知的核心数据结构，包含通知ID、内容、渠道类型等。

| 字段 | 类型 | 说明 |
|------|------|------|
| id | number | 通知ID，相同ID+label会覆盖旧通知 |
| label | string | 通知标签（可选） |
| content | NotificationContent | 通知内容 |
| wantAgent | WantAgent | 点击通知的行为意图 |
| actionButtons | NotificationActionButton[] | 通知按钮 |
| notificationSlotType | SlotType | 通知渠道类型 |
| badgeNumber | number | 角标数字 |
| isUnremovable | boolean | 是否可手动移除 |
| isOngoing | boolean | 是否进行中通知 |

### publish / cancel / cancelAll

| 接口名 | 说明 |
|--------|------|
| publish(request: NotificationRequest): Promise\<void\> | 发布通知 |
| cancel(id: number, label?: string): Promise\<void\> | 取消指定通知 |
| cancelAll(): Promise\<void\> | 取消所有通知 |

### 代码示例

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function publishBasicNotification(): Promise<void> {
  let request: notificationManager.NotificationRequest = {
    id: 1,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
      normal: {
        title: '会议提醒',
        text: '下午3点产品评审会议',
        additionalText: '10分钟后'
      }
    }
  }
  try {
    await notificationManager.publish(request)
  } catch (err) {
    let e = err as BusinessError
    console.error(`publish failed: ${e.code}, ${e.message}`)
  }
}

async function cancelNotification(): Promise<void> {
  try {
    await notificationManager.cancel(1)
  } catch (err) {
    let e = err as BusinessError
    console.error(`cancel failed: ${e.code}, ${e.message}`)
  }
}

async function cancelAllNotifications(): Promise<void> {
  try {
    await notificationManager.cancelAll()
  } catch (err) {
    let e = err as BusinessError
    console.error(`cancelAll failed: ${e.code}, ${e.message}`)
  }
}
```

---

## 通知样式

### ContentType 枚举

| 枚举值 | 说明 |
|--------|------|
| NOTIFICATION_CONTENT_BASIC_TEXT | 普通文本通知 |
| NOTIFICATION_CONTENT_LONG_TEXT | 长文本通知 |
| NOTIFICATION_CONTENT_MULTILINE | 多行文本通知 |
| NOTIFICATION_CONTENT_PICTURE | 图片通知 |

### 普通文本通知

由标题（title）、文本内容（text）、附加信息（additionalText）三个字段组成。

```typescript
import { notificationManager } from '@kit.NotificationKit'

let request: notificationManager.NotificationRequest = {
  id: 1,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    normal: {
      title: '新消息',
      text: '您有一条未读消息',
      additionalText: '刚刚'
    }
  }
}
notificationManager.publish(request)
```

### 长文本通知（LongTextNotificationContent）

继承普通文本字段，新增长文本内容（longText）、通知展开标题（longTitle）、内容概要（briefText）。

```typescript
import { notificationManager } from '@kit.NotificationKit'

let request: notificationManager.NotificationRequest = {
  id: 2,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_LONG_TEXT,
    longText: {
      title: '系统公告',
      text: '版本更新通知',
      additionalText: '今日',
      longText: 'HarmonyOS 6.1版本已正式发布，本次更新包含多项性能优化与安全补丁，建议所有用户尽快升级以获得最佳体验。',
      longTitle: '系统公告 - 版本更新',
      briefText: '版本更新通知'
    }
  }
}
notificationManager.publish(request)
```

### 多行文本通知（MultiLineNotificationContent）

继承普通文本字段，新增多行内容（lines）、内容概要（briefText）、展开标题（longTitle）。

```typescript
import { notificationManager } from '@kit.NotificationKit'

let request: notificationManager.NotificationRequest = {
  id: 3,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_MULTILINE,
    multiLine: {
      title: '待办事项',
      text: '今日待办',
      additionalText: '3项',
      briefText: '今日待办',
      longTitle: '今日待办事项列表',
      lines: [
        '09:00 晨会',
        '10:30 代码评审',
        '14:00 技术分享'
      ]
    }
  }
}
notificationManager.publish(request)
```

### 图片通知（PictureNotificationContent）

继承普通文本字段，新增图片内容（picture）、内容概要（briefText）、展开标题（longTitle）。

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { image } from '@kit.ImageKit'

async function publishPictureNotification(pixelMap: image.PixelMap): Promise<void> {
  let request: notificationManager.NotificationRequest = {
    id: 4,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_PICTURE,
      picture: {
        title: '图片分享',
        text: '查看新图片',
        additionalText: '1张',
        briefText: '图片分享',
        longTitle: '图片分享通知',
        picture: pixelMap
      }
    }
  }
  await notificationManager.publish(request)
}
```

---

## 通知渠道（NotificationSlot）

不同通知渠道对应不同的提醒方式。应用可在"设置 > 通知和状态栏"中管理各渠道。

### 渠道类型

| SlotType | 值 | 分类 | 通知中心 | 横幅 | 锁屏 | 铃声/振动 | 状态栏图标 | 自动亮屏 |
|----------|-----|------|---------|------|------|----------|-----------|---------|
| UNKNOWN_TYPE | 0 | 未知 | Y | N | N | N | N | N |
| SOCIAL_COMMUNICATION | 1 | 社交通信 | Y | Y | Y | Y | Y | Y |
| SERVICE_INFORMATION | 2 | 服务提醒 | Y | Y | Y | Y | Y | Y |
| CONTENT_INFORMATION | 3 | 内容资讯 | Y | N | N | N | N | N |
| CUSTOMER_SERVICE | 5 | 客服消息 | Y | N | N | Y | Y | N |
| OTHER_TYPES | 0xFFFF | 其他 | Y | N | N | N | N | N |

### NotificationSlot 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| type | SlotType | 渠道类型 |
| level | SlotLevel | 通知级别 |
| desc | string | 渠道描述 |
| badgeFlag | boolean | 是否显示角标 |
| bypassDnd | boolean | 是否绕过勿扰模式 |
| vibrationEnabled | boolean | 是否振动 |
| sound | string | 通知铃声URI |
| lightEnabled | boolean | 是否呼吸灯 |
| lightColor | number | 呼吸灯颜色 |
| enabled | boolean | 渠道是否启用（只读） |

### SlotLevel 枚举

| 枚举值 | 说明 |
|--------|------|
| LEVEL_NONE | 不发布通知 |
| LEVEL_MIN | 最低级别，通知栏可见，无铃声振动 |
| LEVEL_LOW | 低级别，通知栏可见，无铃声振动 |
| LEVEL_DEFAULT | 默认级别，通知栏可见，有铃声振动 |
| LEVEL_HIGH | 高级别，通知栏可见，有铃声振动，横幅提醒 |

### 接口说明

| 接口名 | 说明 |
|--------|------|
| addSlot(type: SlotType): Promise\<void\> | 创建通知渠道 |
| addSlot(slot: NotificationSlot): Promise\<void\> | 创建自定义通知渠道 |
| getSlot(slotType: SlotType): Promise\<NotificationSlot\> | 获取指定渠道 |
| getSlots(): Promise\<Array\<NotificationSlot\>\> | 获取所有渠道 |
| removeSlot(slotType: SlotType): Promise\<void\> | 删除指定渠道 |
| removeAllSlots(): Promise\<void\> | 删除所有渠道 |

### 代码示例

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function createCustomSlot(): Promise<void> {
  let slot: notificationManager.NotificationSlot = {
    type: notificationManager.SlotType.SOCIAL_COMMUNICATION,
    level: notificationManager.SlotLevel.LEVEL_HIGH,
    desc: '聊天消息通知渠道',
    badgeFlag: true,
    bypassDnd: false,
    vibrationEnabled: true,
    lightEnabled: true,
    lightColor: 0xFF0000
  }
  try {
    await notificationManager.addSlot(slot)
  } catch (err) {
    let e = err as BusinessError
    console.error(`addSlot failed: ${e.code}, ${e.message}`)
  }
}

async function quickCreateSlot(): Promise<void> {
  try {
    await notificationManager.addSlot(notificationManager.SlotType.SERVICE_INFORMATION)
  } catch (err) {
    let e = err as BusinessError
    console.error(`addSlot failed: ${e.code}, ${e.message}`)
  }
}

async function querySlot(): Promise<void> {
  try {
    let slot = await notificationManager.getSlot(notificationManager.SlotType.SOCIAL_COMMUNICATION)
    if (slot) {
      console.info(`slot enabled: ${slot.enabled}, vibration: ${slot.vibrationEnabled}`)
    }
  } catch (err) {
    let e = err as BusinessError
    console.error(`getSlot failed: ${e.code}, ${e.message}`)
  }
}

async function removeSlot(): Promise<void> {
  try {
    await notificationManager.removeSlot(notificationManager.SlotType.SOCIAL_COMMUNICATION)
  } catch (err) {
    let e = err as BusinessError
    console.error(`removeSlot failed: ${e.code}, ${e.message}`)
  }
}
```

**注意**：除了使用 `addSlot()` 创建渠道，还可以在 `NotificationRequest` 中携带 `notificationSlotType` 字段，若对应渠道不存在会自动创建。

---

## 通知订阅

通知订阅能力通过 `@ohos.notificationSubscribe` 模块提供，用于监听通知的接收、取消等事件。**一般仅系统应用可用**，三方应用需申请 `ohos.permission.NOTIFICATION_CONTROLLER` 权限。

### NotificationSubscriber 回调

| 回调方法 | 说明 |
|----------|------|
| onConsume | 收到新通知回调 |
| onCancel | 通知取消回调 |
| onUpdate | 通知更新回调 |
| onConnect | 订阅成功回调 |
| onDisconnect | 取消订阅回调 |

### 接口说明

| 接口名 | 说明 |
|--------|------|
| subscribe(subscriber: NotificationSubscriber, info?: NotificationSubscribeInfo): Promise\<void\> | 订阅通知 |
| unsubscribe(subscriber: NotificationSubscriber): Promise\<void\> | 取消订阅通知 |

### 代码示例

```typescript
import notificationSubscribe from '@ohos.notificationSubscribe'
import { BusinessError } from '@kit.BasicServicesKit'

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onConsume: (data: notificationSubscribe.SubscribeCallbackData) => {
    console.info(`onConsume: id=${data.request.id}, title=${data.request.content?.normal?.title}`)
  },
  onCancel: (data: notificationSubscribe.SubscribeCallbackData) => {
    console.info(`onCancel: id=${data.request.id}`)
  },
  onUpdate: (data: notificationSubscribe.SubscribeCallbackData) => {
    console.info(`onUpdate: id=${data.request.id}`)
  },
  onConnect: () => {
    console.info('onConnect: subscribe success')
  },
  onDisconnect: () => {
    console.info('onDisconnect: unsubscribe success')
  }
}

async function subscribeNotification(): Promise<void> {
  try {
    await notificationSubscribe.subscribe(subscriber)
  } catch (err) {
    let e = err as BusinessError
    console.error(`subscribe failed: ${e.code}, ${e.message}`)
  }
}

async function unsubscribeNotification(): Promise<void> {
  try {
    await notificationSubscribe.unsubscribe(subscriber)
  } catch (err) {
    let e = err as BusinessError
    console.error(`unsubscribe failed: ${e.code}, ${e.message}`)
  }
}
```

---

## WantAgent — 通知点击行为意图

WantAgent 是 Ability Kit 提供的行为意图封装机制，可将 WantAgent 携带至通知中，用户点击通知或通知按钮时触发对应行为。

### 运行机制

```
应用 → getWantAgent() 创建 WantAgent → 封装至 NotificationRequest → 发布通知
用户点击通知 → 系统触发 WantAgent → 拉起 UIAbility / 发布公共事件
```

### OperationType 枚举

| 枚举值 | 说明 |
|--------|------|
| START_ABILITY | 拉起UIAbility |
| START_ABILITIES | 拉起多个UIAbility |
| START_SERVICE_EXTENSION | 启动ServiceExtension |
| SEND_COMMON_EVENT | 发送公共事件 |

### 代码示例：点击通知拉起 UIAbility

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { wantAgent, WantAgent } from '@kit.AbilityKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function publishNotificationWithWantAgent(): Promise<void> {
  let wantAgentInfo: wantAgent.WantAgentInfo = {
    wants: [
      {
        deviceId: '',
        bundleName: 'com.example.myapp',
        abilityName: 'EntryAbility',
        action: '',
        entities: [],
        uri: '',
        parameters: {}
      }
    ],
    actionType: wantAgent.OperationType.START_ABILITY,
    requestCode: 0,
    actionFlags: [wantAgent.WantAgentFlags.CONSTANT_FLAG]
  }

  let wantAgentObj: WantAgent = await wantAgent.getWantAgent(wantAgentInfo)

  let request: notificationManager.NotificationRequest = {
    id: 10,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
      normal: {
        title: '订单更新',
        text: '您的订单已发货，点击查看详情',
        additionalText: '物流通知'
      }
    },
    wantAgent: wantAgentObj
  }

  try {
    await notificationManager.publish(request)
  } catch (err) {
    let e = err as BusinessError
    console.error(`publish failed: ${e.code}, ${e.message}`)
  }
}
```

### 代码示例：通知按钮触发公共事件

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { wantAgent, WantAgent } from '@kit.AbilityKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function publishNotificationWithButton(): Promise<void> {
  let wantAgentInfo: wantAgent.WantAgentInfo = {
    wants: [
      {
        action: 'com.example.myapp.MARK_READ',
        parameters: {}
      }
    ],
    actionType: wantAgent.OperationType.SEND_COMMON_EVENT,
    requestCode: 0,
    actionFlags: [wantAgent.WantAgentFlags.CONSTANT_FLAG]
  }

  let wantAgentObj: WantAgent = await wantAgent.getWantAgent(wantAgentInfo)

  let actionButton: notificationManager.NotificationActionButton = {
    title: '标记已读',
    wantAgent: wantAgentObj
  }

  let request: notificationManager.NotificationRequest = {
    id: 11,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
      normal: {
        title: '新消息',
        text: '您有3条未读消息',
        additionalText: '即时通讯'
      }
    },
    actionButtons: [actionButton]
  }

  try {
    await notificationManager.publish(request)
  } catch (err) {
    let e = err as BusinessError
    console.error(`publish failed: ${e.code}, ${e.message}`)
  }
}
```

---

## 实况窗通知（Live View）

实况窗通知用于展示录音、录屏、音视频播放、计时、通话等长时任务的实时进展。此类通知不会持久化存储，生命周期与通知发布方一致。

**注意**：实况窗通知仅对系统应用开放，三方应用需通过 Live View Kit 接入。

### NotificationSystemLiveViewContent（API 11+）

| 属性 | 类型 | 说明 |
|------|------|------|
| title | string | 通知标题 |
| text | string | 通知文本 |
| capsule | NotificationCapsule | 胶囊态内容 |
| button | NotificationButton | 按钮 |
| time | NotificationTime | 时间信息 |
| progress | NotificationProgress | 进度信息 |

### 代码示例

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function publishLiveViewNotification(): Promise<void> {
  let request: notificationManager.NotificationRequest = {
    id: 20,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_SYSTEM_LIVE_VIEW,
      systemLiveView: {
        title: '导航中',
        text: '距离目的地2.5公里',
        capsule: {
          title: '导航',
          icon: '',
          backgroundColor: 0xFF007DFF,
          content: '2.5公里'
        },
        progress: {
          maxValue: 100,
          currentValue: 75,
          isPercentage: true
        },
        time: {
          initialTime: Date.now(),
          isCountDown: false,
          isShowInChronometer: true
        }
      }
    },
    isOngoing: true,
    isUnremovable: true
  }

  try {
    await notificationManager.publish(request)
  } catch (err) {
    let e = err as BusinessError
    console.error(`publish live view failed: ${e.code}, ${e.message}`)
  }
}
```

---

## 进度条通知

进度条通知用于展示下载、上传等进度类场景。

### 代码示例

```typescript
import { notificationManager } from '@kit.NotificationKit'
import { BusinessError } from '@kit.BasicServicesKit'

async function publishProgressNotification(): Promise<void> {
  let request: notificationManager.NotificationRequest = {
    id: 30,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
      normal: {
        title: '文件下载',
        text: '正在下载...',
        additionalText: '50%'
      }
    },
    template: {
      name: 'downloadTemplate',
      data: {
        progressValue: '50',
        progressMaxValue: '100'
      }
    }
  }

  try {
    await notificationManager.publish(request)
  } catch (err) {
    let e = err as BusinessError
    console.error(`publish failed: ${e.code}, ${e.message}`)
  }
}
```

---

## 通知角标

| 接口名 | 说明 |
|--------|------|
| setBadgeNumber(number: number): Promise\<void\> | 设置角标数字（API 10+） |
| getBadgeNumber(): Promise\<number\> | 获取角标数字（API 22+） |

```typescript
import { notificationManager } from '@kit.NotificationKit'

async function setBadge(count: number): Promise<void> {
  await notificationManager.setBadgeNumber(count)
}
```

---

## 权限

### 通知授权机制

应用通知能力默认关闭，需通过 `requestEnableNotification()` 请求用户授权。该接口无需在 `module.json5` 中声明权限。

### 系统权限

| 权限名 | 授权方式 | APL | 说明 |
|--------|---------|-----|------|
| ohos.permission.NOTIFICATION_CONTROLLER | system_grant | system_core | 通知控制权限（仅系统应用） |
| ohos.permission.PUBLISH_AGENT_REMINDER | system_grant | system_basic | 后台代理提醒发布权限 |

### 通知启用检查

```typescript
import { notificationManager } from '@kit.NotificationKit'

async function checkNotificationEnabled(): Promise<boolean> {
  return await notificationManager.isNotificationEnabled()
}
```

---

## 通知更新

发布与已存在通知相同 ID 的 `NotificationRequest` 即可更新通知内容。

```typescript
import { notificationManager } from '@kit.NotificationKit'

async function updateNotification(id: number, progress: number): Promise<void> {
  let request: notificationManager.NotificationRequest = {
    id: id,
    content: {
      notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
      normal: {
        title: '文件下载',
        text: `正在下载... ${progress}%`,
        additionalText: `${progress}%`
      }
    }
  }
  await notificationManager.publish(request)
}
```

## API 23 新增能力

### 通知优先显示

NotificationRequest 新增 `priorityNotificationType` 属性，支持设置通知优先显示。

### 重叠图标

NotificationRequest 新增 `overlayIcon` 属性，支持设置重叠图标。

### 横幅和锁屏显示控制

NotificationFlags 新增属性，支持应用调整通知是否在横幅和锁屏界面显示。

---

## 官方参考链接

| 文档 | 链接 |
|------|------|
| Notification Kit 简介 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-overview |
| 请求通知授权 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-enable |
| 发布文本类型通知 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/text-notification |
| 发布进度条类型通知 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/progress-bar-notification |
| 为通知添加行为意图 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-with-wantagent |
| 管理通知渠道 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-slot |
| 管理通知角标 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-badge |
| 取消通知 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-cancel |
| 更新通知 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-update |
| 跨设备协同通知 | https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/notification-distributed |
| @ohos.notificationManager API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationmanager |
| @ohos.notificationSubscribe API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-notificationsubscribe |
| @ohos.app.ability.wantAgent API | https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-app-ability-wantagent |
| NotificationRequest 数据结构 | https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inner-notification-notificationrequest |
| 官方示例代码 | https://gitcode.com/HarmonyOS_Samples/guide-snippets/tree/master/Notification-Kit |
