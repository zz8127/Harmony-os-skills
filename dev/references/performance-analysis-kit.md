# Performance Analysis Kit — 性能分析

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Performance Analysis Kit 提供应用性能分析能力，包括事件打点（HiAppEvent）、调试信息获取（HiDebug）、性能数据采集（HiPerf）等，帮助开发者定位性能瓶颈和崩溃问题。

---

## HiAppEvent — 事件打点

```typescript
import { hiAppEvent } from '@kit.PerformanceAnalysisKit'

hiAppEvent.write({
  domain: 'my_app',
  name: 'user_click',
  eventType: hiAppEvent.EventType.BEHAVIOR,
  params: {
    button_id: 'submit',
    duration: 150
  }
})
```

### 事件类型

| 类型 | 说明 |
|------|------|
| FAULT | 故障事件 |
| STATISTIC | 统计事件 |
| SECURITY | 安全事件 |
| BEHAVIOR | 行为事件 |

---

## HiDebug — 调试信息

```typescript
import { hidebug } from '@kit.PerformanceAnalysisKit'

let memory = hidebug.getAppMemory()

let cpuUsage = hidebug.getAppCpuUsage()
```

---

## API 23 新增（HarmonyOS 6.1.0）

### HiAppEvent 增强

- 新增 ArkWeb 抛滑触控操作丢帧检测能力
- 支持检测 Web 页面滑动时的丢帧问题

### HiDebug 增强

- 新增添加维测信息接口，开发者可将维测信息添加到崩溃日志中
- 若程序发生崩溃，可在崩溃日志中找到该维测信息，便于定位问题

```typescript
import { hidebug } from '@kit.PerformanceAnalysisKit'

hidebug.setCrashObj('user_id', '12345')
hidebug.setCrashObj('page', 'shopping_cart')
```

### AppFreeze 日志增强

AppFreeze 日志中调用栈的堆栈信息增加线程状态信息，便于分析应用卡死问题。

---

## Kit 导入

```typescript
import { hiAppEvent } from '@kit.PerformanceAnalysisKit'
import { hidebug } from '@kit.PerformanceAnalysisKit'
```

---

## 官方参考

- HiAppEvent 开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hiappevent-guidelines
- HiDebug 开发指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hidebug-guidelines
- AppFreeze 分析：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/appfreeze-guidelines
