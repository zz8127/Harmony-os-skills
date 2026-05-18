# Remote Communication Kit（远场通信服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/remote-communication-introduction

## 概述

Remote Communication Kit（远场通信服务）提供请求网络数据的功能，包含 HTTP 请求能力和 URPC 高性能 RPC 通信库。

## 核心能力

### HTTP 请求能力

构建场景化 HTTP 通信能力，强调易用性。

### URPC（Unified Remote Procedure Call）

实现远程函数调用能力，具有抗弱网传输、多径传输等特性。

## 支持的 HTTP 请求场景

| 场景 | 说明 |
|------|------|
| 发送 PATCH 请求 | 以 PATCH 方式请求 |
| 设置基地址 | 会话中 URL 的基地址自动拼接 |
| 取消自动重定向 | 取消 HTTP 请求的自动重定向 |
| 拦截请求和响应 | 在请求后或响应前进行拦截 |
| 取消请求 | 发送前/中/后取消请求 |
| 响应缓存 | 优先读取缓存 |
| 自定义证书校验 | 自定义客户端和服务端证书校验 |
| 忽略 SSL 校验 | 不验证服务器 SSL 证书 |
| 自定义 DNS 解析 | 自定义 DNS 服务器或静态 DNS 规则 |
| 捕获跟踪信息 | 获取详细的请求跟踪信息 |
| 获取时间数据 | 获取 HTTP 请求各阶段时间信息 |

## 支持的设备

Phone、2in1、Tablet、Wearable、TV（从 5.1.1 开始）

## 约束与限制

暂不支持 Lite Wearable 设备。

## 模拟器支持情况

支持模拟器，但 URPC 能力不支持模拟器。

## 相关 Kit

- Network Kit：标准 HTTP 能力

## API 参考

| API | 说明 |
|-----|------|
| @ohos.remoteCommunication | 远场通信能力 |
