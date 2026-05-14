# Function Flow Runtime Kit

## 概述

Function Flow Runtime Kit（任务并发调度服务，简称 FFRT）是一种并发编程框架，旨在简化并发编程和任务调度的复杂性。FFRT 采用基于任务的调度方式，开发者只需关注任务及其依赖关系，无需处理底层线程和计算资源。FFRT 采用基于协程的任务执行方式，提高任务并行度、提升线程利用率并充分利用多核平台计算资源，保证系统对所有资源的集约化管理，解决系统线程资源滥用问题。

## 核心能力

### Task-Based 特性

以任务方式组织应用程序表达，运行时以任务粒度执行调度：
- 任务之间可直接指定依赖关系，也可通过数据对象表达依赖
- 任务支持嵌套，形成父子任务关系
- 多任务支持同步（等待、锁、条件变量等）
- 任务目标颗粒度最小为 100us 量级

### Queue-Enabled 特性

利用任务队列约束任务执行顺序和并发度：
- **串行队列**：确保任务按提交顺序依次执行，适用于保持特定执行顺序的任务流
- **并发队列**：允许多个任务同时执行，提高并发性能；可通过约束整体并发度避免过度并发

### Graph-Driven 特性

通过构建任务依赖图管理任务间依赖关系，实现复杂任务流的高效调度：
- **任务依赖（Task Dependence）**：直接描述任务间依赖关系生成任务依赖图
- **数据依赖（Data Flow）**：通过数据的生产者和消费者关系表达依赖

### 线程编程模型 vs 任务编程模型对比

| 对比项 | 线程编程模型 | 任务编程模型 |
|---|---|---|
| 并行度挖掘 | 程序员创建多线程分配任务 | 编译器/语言配合静态分解任务及依赖 |
| 线程创建 | 程序员负责，可能滥用 | FFRT 运行时负责线程池管理 |
| 负载均衡 | 静态映射，可能不均 | 运行时动态调度，减轻不均 |
| 调度开销 | 内核态调度，开销大 | 用户态协程调度，更轻量 |
| 依赖表达 | 运行时同步操作，增加切换 | 创建时显式表达，不满足不调度 |

## npm 包名

`@kit.FfrtKit`

## 关键 API

| API | 说明 |
|---|---|
| FFRT C/C++ API | 任务提交、依赖管理、队列操作、同步原语 |
| `ffrt::submit` | 提交任务 |
| `ffrt::submit_h` | 提交任务并获取句柄 |
| `ffrt::wait` | 等待任务完成 |
| `ffrt::mutex` | FFRT 互斥锁 |
| `ffrt::condition_variable` | FFRT 条件变量 |
| 串行队列 API | 创建和管理串行队列 |
| 并发队列 API | 创建和管理并发队列 |

## 权限要求

无额外权限要求。

## 约束与限制

- 任务颗粒度影响性能，过小增加调度开销，过大降低并行度
- 目标颗粒度最小为 100us 量级
- 支持模拟器

## 官方链接

- [FFRT 概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ffrt-overview)
- [FFRT 并发范式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ffrt-concurrency-paradigm)
- [FFRT Kit 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ffrt-kit)
