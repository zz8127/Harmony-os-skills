# ArkTS

## 概述

ArkTS 是 HarmonyOS 应用开发的官方高级语言，基于 TypeScript 生态扩展，保持了 TS 的基本风格，同时通过规范定义强化开发期静态检查和分析，提升代码健壮性、程序执行稳定性和性能。ArkTS 同时支持与 TS/JavaScript 高效互操作。

方舟编译运行时（ArkCompiler）支持 ArkTS、TS 和 JS 的编译运行，分为 ArkTS 编译工具链和 ArkTS 运行时两部分：
- ArkTS 编译工具链：将高级语言编译为方舟字节码文件（\*.abc）
- ArkTS 运行时：在设备侧运行字节码文件，执行程序逻辑

## 核心能力

### 声明式 UI 范式
- 基于 ArkUI 框架的声明式 UI 开发范式
- 组件化开发模型，支持自定义组件扩展
- 状态管理：@State、@Prop、@Link、@Provide、@Consume 等装饰器

### 状态管理
- 本地状态管理：@State、@Prop、@Link
- 全局状态管理：@Provide / @Consume、AppStorage、PersistentStorage
- 跨组件通信：@Watch、@Builder、@Extend

### 渲染控制
- 条件渲染：if/else
- 循环渲染：ForEach、LazyForEach
- 数据懒加载：LazyForEach 配合 IDataSource 实现

### 基础类库与容器类库
- 高精度浮点运算（Decimal）
- 二进制 Buffer
- XML 生成、解析与转换
- 多种容器库（ArrayList、HashMap、TreeMap 等）

### 并发编程
- **TaskPool**：多线程并发任务池，支持任务调度、取消、优先级设置
- **Worker**：独立线程的并发模型，支持长时间运行任务
- **Sendable**：支持对象在并发实例间的引用传递，提升并发通信性能

### TS/JS 互操作
- 支持 ArkTS 与 TS/JavaScript 高效互操作
- 适配规则参考：从 TypeScript 到 ArkTS 的适配规则

## npm 包

无独立 npm 包，ArkTS 是语言层面能力，随 HarmonyOS SDK 内置。

## 关键 API

| API | 说明 |
|-----|------|
| @State | 组件内状态管理 |
| @Prop | 单向数据同步 |
| @Link | 双向数据同步 |
| @Provide / @Consume | 跨层级数据同步 |
| @Watch | 状态变量变化监听 |
| @Builder | 轻量 UI 复用机制 |
| ForEach | 循环渲染 |
| LazyForEach | 数据懒加载渲染 |
| TaskPool | 多线程任务池 |
| Worker | 独立线程并发 |

## 权限要求

无额外权限要求，ArkTS 为语言层能力。

## 模拟器支持

- 支持 Simulator，但与真机存在部分能力差异
- ArkTS 基础库与 ArkTS 并发暂不支持模拟器

## 官方链接

- [ArkTS 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-overview)
- [ArkTS 基础类库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-utils)
- [从 TypeScript 到 ArkTS 适配规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)
- [TaskPool 并发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/taskpool-introduction)
- [Worker 并发](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/worker-introduction)
