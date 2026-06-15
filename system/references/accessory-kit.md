---
name: Accessory Kit
description: 配件接入服务为合作配件设备及生态企业应用提供关联唤醒、系统服务联动、按需调度与安全授信管理等能力。
---

# Accessory Kit

## 概述

Accessory Kit（配件接入服务）是 HarmonyOS 26.0.0 Beta1 中新增的开发套件，为合作配件设备及生态企业应用提供以下核心能力：

- **关联唤醒**：支持配件与应用的智能关联和唤醒
- **系统服务联动**：与系统服务深度集成，提供统一的接入体验
- **按需调度**：根据场景需求灵活调度资源
- **安全授信管理**：提供安全的设备认证和授权机制

## 主要特性

| 特性 | 描述 |
|------|------|
| 配件发现 | 自动发现周边配件设备 |
| 配对管理 | 配件配对、绑定、解绑流程 |
| 消息通道 | 配件与应用间的消息通信 |
| 能力开放 | 开放配件能力给第三方应用 |
| 安全认证 | 设备身份认证和权限管理 |

## 典型应用场景

1. **智能配件联动**：智能手表、耳机等配件与手机应用联动
2. **IoT 设备接入**：智能家居设备的快速接入
3. **场景化触发**：基于配件状态触发特定场景

## 开发指南

官方文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/accessorykit-introduction

### 基础使用流程

```
1. 初始化 Accessory Kit
2. 扫描发现配件设备
3. 建立连接并认证
4. 注册消息监听
5. 进行数据交互
6. 断开连接
```

## 相关资源

- [Accessory Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/accessorykit-api)
- [Accessory Kit 示例代码](https://developer.huawei.com/consumer/cn/samples/)

## 版本兼容性

| HarmonyOS 版本 | API 版本 | 支持状态 |
|---------------|---------|---------|
| 26.0.0 Beta1 | 26 | 新增 |