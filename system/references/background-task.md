# 后台任务（Background Tasks Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Background Tasks Kit（`@kit.BackgroundTasksKit`）提供受约束的后台任务能力，允许应用在退到后台后继续运行有限时间。

后台任务分为四类：

| 类型 | 典型时长 | 适用场景 |
|------|---------|---------|
| 短时任务 | 最长 3 分钟 | 临时数据处理、文件保存 |
| 长时任务 | 持续运行（需前台通知） | 音乐播放、导航、运动追踪 |
| 延迟任务 | 系统调度（非实时） | 数据同步、日志上传 |
| 代理提醒 | 系统代理触发 | 定时提醒、日历提醒、闹钟 |

## 短时任务

### 约束

- 单次申请最长 **3 分钟**，到期后系统强制挂起
- 每日配额有限，用尽后无法申请
- 必须是用户可感知的操作

### 申请短时任务

```typescript
import { backgroundTaskManager } from '@kit.BackgroundTasksKit';

let delayInfo: backgroundTaskManager.DelaySuspendInfo;
delayInfo = backgroundTaskManager.requestSuspendDelay('SaveData', () => {
  console.info('Suspend delay expired');
});
console.info('requestId: ' + delayInfo.requestId);
```

### 取消短时任务

```typescript
backgroundTaskManager.cancelSuspendDelay(delayInfo.requestId);
```

## 长时任务

长时任务允许应用在后台持续运行，但必须关联一个持续显示的前台通知。

### 支持的类型

| 类型 | 常量 | 说明 |
|------|------|------|
| 数据传输 | `BackgroundMode.DATA_TRANSFER` | 网络下载/上传 |
| 音频播放 | `BackgroundMode.AUDIO_PLAYBACK` | 音乐、语音播放 |
| 音频录制 | `BackgroundMode.AUDIO_RECORDING` | 录音、语音识别 |
| 位置追踪 | `BackgroundMode.LOCATION` | 导航、运动追踪 |
| 蓝牙交互 | `BackgroundMode.BLUETOOTH_INTERACTION` | 蓝牙设备通信 |
| 多设备互联 | `BackgroundMode.MULTIDEVICE_CONNECTION` | 分布式业务 |
| 任务保持 | `BackgroundMode.TASK_KEEPING` | 持续计算任务 |

### module.json5 配置

```json
{
  "module": {
    "abilities": [
      {
        "name": "EntryAbility",
        "backgroundModes": ["audioPlayback", "location"]
      }
    ]
  }
}
```

### 申请长时任务

```typescript
import { backgroundTaskManager } from '@kit.BackgroundTasksKit';
import { notificationManager } from '@kit.NotificationKit';
import { wantAgent } from '@kit.AbilityKit';

let wantAgentObj = await wantAgent.getWantAgent({
  wants: [{ bundleName: 'com.example.app', abilityName: 'EntryAbility' }],
  requestCode: 0,
  wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
});

await notificationManager.publish({
  id: 1,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    normal: { title: 'Music Playing', text: 'App is playing music in background' }
  },
  wantAgent: wantAgentObj
});

backgroundTaskManager.startBackgroundRunning(
  globalThis.context,
  backgroundTaskManager.BackgroundMode.AUDIO_PLAYBACK,
  wantAgentObj
);
```

### API 14+ 新接口

```typescript
let taskId: number = await backgroundTaskManager.requestContinuousTask({
  bgMode: backgroundTaskManager.BackgroundMode.AUDIO_PLAYBACK,
  wantAgent: wantAgentObj,
  taskTitle: 'Music Playing',
  taskDesc: 'App is playing music in background'
});
backgroundTaskManager.cancelContinuousTask(taskId);
```

## 延迟任务

延迟任务（WorkScheduler）由系统统一调度，在满足条件时执行。

### 注册延迟任务

```typescript
import { workScheduler } from '@kit.BackgroundTasksKit';

let workInfo: workScheduler.WorkInfo = {
  workId: 1,
  networkType: workScheduler.NetworkType.NETWORK_TYPE_WIFI,
  isCharging: true,
  isRepeat: true,
  repeatCycleTime: 1800000,
  isPersisted: true,
  bundleName: 'com.example.app',
  abilityName: 'WorkSchedulerAbility'
};
workScheduler.registerWork(workInfo);
```

### 延迟任务回调

```typescript
import { WorkSchedulerExtensionAbility } from '@kit.BackgroundTasksKit';

export default class WorkSchedulerAbility extends WorkSchedulerExtensionAbility {
  onWorkStart(workInfo: workScheduler.WorkInfo) {
    console.info('onWorkStart: ' + workInfo.workId);
  }
  onWorkStop(workInfo: workScheduler.WorkInfo) {
    console.info('onWorkStop: ' + workInfo.workId);
  }
}
```

## 代理提醒

代理提醒由系统代理发布，应用无需在后台运行即可触发提醒。

### 发布定时器提醒

```typescript
import { reminderAgentManager } from '@kit.ReminderAgentKit';

let timerRequest: reminderAgentManager.ReminderRequestTimer = {
  reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_TIMER,
  triggerTimeInSeconds: 300,
  title: 'Timer',
  content: '5 minutes elapsed',
  wantAgent: wantAgentObj
};
let reminderId = await reminderAgentManager.publishReminder(timerRequest);
```

### 发布日历提醒

```typescript
let calendarRequest: reminderAgentManager.ReminderRequestCalendar = {
  reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_CALENDAR,
  dateTime: { year: 2026, month: 6, day: 15, hour: 9, minute: 0 },
  repeatDays: [1, 15],
  title: 'Meeting',
  content: 'Team weekly meeting',
  wantAgent: wantAgentObj
};
reminderAgentManager.publishReminder(calendarRequest);
```

### 发布闹钟提醒

```typescript
let alarmRequest: reminderAgentManager.ReminderRequestAlarm = {
  reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_ALARM,
  hour: 7,
  minute: 30,
  daysOfWeek: [1, 2, 3, 4, 5],
  title: 'Wake Up',
  content: 'Time to get up',
  wantAgent: wantAgentObj
};
reminderAgentManager.publishReminder(alarmRequest);
```

### 取消提醒

```typescript
reminderAgentManager.cancelReminder(reminderId);
reminderAgentManager.cancelAllReminders();
```

## 权限

| 权限 | 说明 | 授权方式 |
|------|------|---------|
| `ohos.permission.KEEP_BACKGROUND_RUNNING` | 长时任务后台运行 | system_grant |
| `ohos.permission.PUBLISH_AGENT_REMINDER` | 代理提醒发布 | system_grant |

---

## 官方参考

- 后台任务概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/background-task-overview-V5
- 短时任务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-suspend-delay-V5
- 长时任务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/request-continuous-task-V5
- 延迟任务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/work-scheduler-V5
- 代理提醒：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reminder-agent-manager-V5
