# Network Boost Kit + Remote Communication Kit

本文件汇总网络加速服务与远场通信服务。

---

## 一、Network Boost Kit（网络加速服务）

### 概述

Network Boost Kit 提供网络加速能力以及网络感知、网络质量预测等能力，通过软、硬、芯、端、管、云等全方位的协同解决方案实现网络资源的调优和加速，构筑更可靠、更流畅、更高速的上网体验。

### 核心能力

- 网络加速
- 网络感知
- 网络质量预测
- 连接迁移通知
- 应用传输体验反馈（QoE）
- 多网发起和释放
- 迁移模式设置

### npm 包名

`@kit.NetworkBoostKit`

### 关键 API

| API | 说明 |
|---|---|
| `NetworkBoost` (C/C++) | 网络加速 Native API |
| `network_boost.h` | C API 头文件 |
| `NetworkBoost_NetworkQos` | 网络质量服务结构体 |
| 连接迁移通知 API | 网络切换回调 |
| 应用传输体验反馈 API | QoE 上报 |
| 多网发起/释放 API | 多路径网络管理 |

### 权限要求

- `ohos.permission.GET_NETWORK_INFO`

### 约束与限制

- 仅适用于 Phone、Tablet 和 PC/2in1 设备
- 仅支持 Wi-Fi 和 Cellular 网络，不支持有线网络、蓝牙等
- 暂不支持模拟器

### 官方链接

- [Network Boost Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/networkboost-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/networkboost-preparations)

---

## 二、Remote Communication Kit（远场通信服务）

### 概述

Remote Communication Kit 提供请求网络数据的功能，包含 HTTP 请求能力和 URPC 高性能 RPC 通信库。与 Network Kit 提供的标准 HTTP 能力不同，Remote Communication Kit 构建了场景化 API，强调易用性。URPC 具有抗弱网传输、多径传输（蜂窝网络和 Wi-Fi）等特性。

### 核心能力

#### HTTP 请求能力

- 支持 GET、POST、PUT、DELETE、OPTIONS、HEAD、PATCH 等请求方法
- 设置会话中 URL 的基地址
- 取消自动重定向
- 拦截请求和响应
- 取消请求（发送前/发送中/接收后）
- 响应缓存
- 设置响应数据类型（string、object、ArrayBuffer）
- 自定义证书校验
- 忽略 SSL 校验
- 自定义 DNS 解析
- 捕获详细跟踪信息
- 获取 HTTP 请求时间数据

#### URPC 高性能 RPC 通信库

- 远程函数调用能力
- 抗弱网传输
- 多径传输（蜂窝网络和 Wi-Fi）

### npm 包名

`@kit.RemoteCommunicationKit`

### 关键 API

| API | 说明 |
|---|---|
| `rcp` (ArkTS) | 远场通信场景化 HTTP API |
| `rcp.h` (C/C++) | 远场通信 Native API |
| URPC API | 高性能 RPC 通信 |

### 权限要求

- `ohos.permission.INTERNET`

### 约束与限制

- 支持 Phone、2in1、Tablet、Wearable 设备
- 从 5.1.1(19) 开始新增支持 TV 设备
- 暂不支持 Lite Wearable 设备
- 支持模拟器（但模拟器不支持 URPC）

### 官方链接

- [Remote Communication Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/remote-communication-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/remote-communication-preparations)
