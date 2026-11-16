# Performance Analysis Kit — 性能分析

> **适用版本**：HarmonyOS 26.0.0 / API 26（Release，2026-08-29，底座 OpenHarmony 7.0）；兼容 HarmonyOS 6.1.1 / API 24（Release）及更低版本。兼容 API 14+。

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

## API 26 新增（HarmonyOS 26.0.0）

### Release 阶段新增（Beta2 后）

- **JS Crash 检测增强**：新增支持 NativeModuleErrorInfo，可记录最早的 20 条 so 加载失败信息，便于崩溃问题定位

### Beta2 阶段新增（已包含在 Release 中）

- **HiDebug 内存导出监听器**：新增支持注册内存导出监听器，用于导出应用内存快照

## 26.0.1 Beta1 新增（2026-11-10）

> 26.0.1 为 26.0.0 的增量版本（Beta1，2026-11-10），仅供尝鲜；知识库基线仍为 HarmonyOS 26.0.0 / API 26（Release）。

### HiDebug C API 增强

- **hiprofiler 资源采集混合类型**：新增混合类型采集，涵盖 Global Handle 对象调用栈、堆快照、映射文件打包
- **2D 资源采集开放场景**：StartProfiler 新增异步嵌套层数、每层异步栈深配置参数
- **DMABUF 资源类型**：资源采集新增 DMABUF 资源类型，支撑应用自行采集 DMA 内存分配栈
- **分配释放栈消减去重**：支持分配栈与释放栈消减去重，减少采集量、降低性能开销

### external_log 日志管理

- **日志管理者注册接口**：新增 external_log 日志管理者注册接口，故障日志沙箱目录容量达到阈值时可通知应用清理删除 external_log 文件

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
