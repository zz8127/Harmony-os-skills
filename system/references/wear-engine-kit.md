# Wear Engine Kit

## 概述

Wear Engine Kit（穿戴服务）面向手机和穿戴设备的应用与服务开发者，提供华为穿戴设备开放能力。开发者通过调用 Wear Engine 开放能力，可实现手机上的生态应用与服务给华为穿戴设备发消息、发通知、传输数据并获取穿戴设备状态、读取传感器数据等，也可实现华为穿戴设备上的生态应用与服务给手机发消息、传输数据等。

Wear Engine 将手机上的生态应用和服务延展到智能穿戴设备，也将智能穿戴的设备能力开放给手机应用，实现手机与穿戴设备能力共享。

## 核心能力

### 1. 获取穿戴设备基础信息（设备基础能力）

- 开放范围：个人开发者、企业开发者
- 手机侧应用：获取已配对穿戴设备列表并选定设备，查询与订阅穿戴设备连接状态、电量、充电状态等

### 2. 应用间消息通信（设备基础能力）

- 开放范围：个人开发者、企业开发者
- 手机侧应用：支持双向传输消息与文件（图片、音乐等）
- 轻量级智能穿戴设备侧应用：支持双向传输消息与文件
- 智能穿戴设备侧应用：支持双向传输消息与文件

### 3. 穿戴设备模板化通知

- 开放范围：个人开发者、企业开发者
- 手机侧应用：发送模板化通知到穿戴设备

### 4. 获取穿戴用户状态

- 开放范围：企业开发者
- 手机侧应用：获取穿戴设备运动传感器数据，支持通过打开/关闭命令控制获取

### 5. 运动传感器（穿戴传感器能力）

- 开放范围：仅限企业开发者中的专业研究机构
- 手机侧应用：获取穿戴设备人体传感器数据

### 6. 人体传感器（穿戴传感器能力）

- 开放范围：仅限企业开发者中的专业研究机构
- 手机侧应用：获取穿戴设备人体传感器数据和状态控制

### 7. 设备标识符

- 开放范围：仅限企业开发者中的合作企业
- 手机侧应用：获取穿戴设备序列号（SN）

### 业务优势

- **便捷管理**：基于穿戴设备连接和状态的实时感知能力，实现多设备协同
- **实时提醒**：重要通知实现腕上提醒、零距离触达
- **新交互**：为手机应用带来全新的"腕上交互"，如音乐播放控制、导航提示等

## npm 包名

`@kit.WearEngineKit`

## 关键 API

| API | 说明 |
|---|---|
| `wearEngine` | 穿戴设备能力开放 API |
| 设备基础信息 API | 获取设备列表、连接状态、电量等 |
| 消息通信 API | 双向消息与文件传输 |
| 模板化通知 API | 发送模板化通知 |
| 用户状态 API | 获取穿戴用户状态 |
| 传感器 API | 获取运动/人体传感器数据 |
| 设备标识符 API | 获取穿戴设备 SN |

## 权限要求

具体权限请参考各开发指导文档，不同能力开放范围不同（个人开发者/企业开发者/专业研究机构/合作企业）。

## 约束与限制

- 适用于 Phone 和 Tablet 设备
- 从 5.1.0(18) 版本开始支持 Wearable
- Phone、Tablet 设备仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 暂不支持模拟器

## 官方链接

- [Wear Engine Kit 业务简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/we-business_introduction)
- [Wear Engine Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wearengine_introduction)
- [场景介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scene_introduction)
- [申请接入 Wear Engine 服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wearengine_apply)
- [wearEngine API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/wearengine_api)
