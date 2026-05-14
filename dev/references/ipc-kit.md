# IPC Kit

## 概述

IPC Kit（进程间通信服务）提供设备内和设备间的跨进程通信能力。IPC使用Binder驱动，适用于设备内的跨进程通信；RPC使用软总线驱动，适用于跨设备的跨进程通信。

## 核心能力

### IPC（进程间通信）

- 设备内的跨进程通信
- 典型使用场景：后台服务，通过IPC机制提供单设备跨进程接口调用与数据传递能力

### RPC（远程过程调用）

- 设备间的跨进程通信
- 典型使用场景：多端协同，通过RPC机制提供跨设备远端接口调用与数据传递能力

### Client-Server 模型

- Client进程获取Server进程的代理（Proxy），通过Proxy读写数据和发起请求
- Stub处理请求并应答结果，实现进程间通信
- Proxy和Stub提供一组由服务/业务自定义的接口

## npm 包名

`@kit.IPCKit`

## 关键 API

| API | 说明 |
|---|---|
| @ohos.rpc | RPC通信核心模块，提供跨进程通信能力 |
| rpc.IRemoteObject | 远程对象接口，用于跨进程通信 |
| rpc.RemoteObject | 远程对象基类（Stub端） |
| rpc.Proxy | 远程代理类（Client端） |
| rpc.MessageSequence | 消息序列化，用于数据读写 |
| rpc.MessageParcel | 消息包裹（旧接口） |
| rpc.Ashmem | 匿名共享内存，用于大数据传输 |

## 基本概念

| 缩写 | 全称 | 说明 |
|---|---|---|
| IPC | Inter Process Communication | 设备内的进程间通信 |
| RPC | Remote Procedure Call | 设备间的进程间通信 |
| Client | 客户端 | 请求服务的一端，称为代理（Proxy） |
| Server | 服务端 | 提供服务的一端，称为Stub |

## 权限要求

无特殊权限要求，但跨设备通信需设备在同一组网内。

## 约束与限制

- 单个设备上跨进程通信时，传输的数据量最大为200KB，超过可使用匿名共享内存（Ashmem）
- 不支持在RPC中订阅匿名Stub对象的死亡通知
- 不支持把跨设备的Proxy对象回传到该Proxy对象指向的Stub对象所在的设备
- 指向远端设备Stub的Proxy对象不能在本设备内二次跨进程传递
- 支持模拟器

## 官方链接

- [IPC Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ipc-rpc-overview)
- [IPC与RPC通信开发指导(ArkTS)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ipc-rpc-development-guideline)
- [IPC与RPC通信开发指导(C/C++)](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ipc-capi-development-guideline)
- [@ohos.rpc API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-rpc)
