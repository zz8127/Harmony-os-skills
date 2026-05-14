# NearLink Kit

## 概述

NearLink Kit（星闪服务）提供一种低功耗、高速率的短距离通信服务，支持星闪设备之间的连接、数据交互。中心设备可以通过扫描发现外围设备并发起连接，外围设备可以通过发送广播的方式被中心设备发现，连接后可进行数据传输。

## 核心能力

### 中心设备能力

- 扫描发现外围设备
- 发起连接
- 数据传输

### 外围设备能力

- 发送广播被中心设备发现
- 与中心设备连接
- 数据传输

### 典型使用场景

- 中心设备与星闪鼠标配对连接，使用鼠标作为输入控制中心设备
- 中心设备与星闪手写笔配对连接，使用手写笔作为输入操作中心设备

## npm 包名

`@kit.NearLinkKit`

## 关键 API

| API | 说明 |
|---|---|
| 星闪中心设备 API | 扫描、连接、数据传输 |
| 星闪外围设备 API | 广播、连接、数据传输 |

## 权限要求

具体权限请参考各开发指导文档。

## 约束与限制

- 适用于 Phone、PC/2in1、TV、Tablet 和 Wearable 设备
- 暂不支持模拟器

## 官方链接

- [NearLink Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nearlink-introduction)
- [NearLink Kit 术语](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nearlink-terminology)
- [使用星闪传输数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nearlink-start-data-transfer)
