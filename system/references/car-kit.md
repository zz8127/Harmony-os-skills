# Car Kit

## 概述

Car Kit（车服务）为开发者提供一套便捷接入出行服务的能力。通过集成 Car Kit，可以轻松实现在手机与鸿蒙智行车机之间无缝传递导航信息、通过超级桌面在鸿蒙智行车机上使用手机应用、通过 HiCar 在认证车机上使用手机应用等功能，为用户提供更加良好的出行体验。

Car Kit 处于 HarmonyOS 框架层，作为生态应用和系统应用之间的桥梁，负责转发导航数据变化、系统事件和智慧出行连接状态。

## 核心能力

### 导航流转（鸿蒙智行车辆）

- 手机与车机之间无缝传递导航信息
- 导航信息流转至车机
- 地址流转至车机
- 下车后地图导航自动流转回手机，实现步行导航接续

### 超级桌面（鸿蒙智行车辆）

- 手机应用在鸿蒙座舱车机操作系统上使用
- 获取车机屏幕信息用于 UI 呈现
- 使用车机摄像头优化业务交互

### HiCar 互联（HiCar 认证车辆）

- 移动设备与 HiCar 认证车辆连接
- 获取 HiCar 认证车辆屏幕信息用于 UI 呈现
- 使用 HiCar 认证车辆摄像头优化业务交互

### 实现原理

1. 系统应用向 Car Kit 订阅导航数据变化，生态应用导航数据变化时通知到 Car Kit，Car Kit 转发给系统应用
2. 生态应用向 Car Kit 订阅系统事件，系统应用希望生态应用执行任务时通知到 Car Kit，Car Kit 转发给生态应用
3. 生态应用向 Car Kit 订阅智慧出行连接状态变化，Car Kit 将当前连接状态转发给生态应用

## npm 包名

`@kit.CarKit`

## 关键 API

| API | 说明 |
|---|---|
| 导航类接口 | 提供导航信息、响应系统流转事件 |
| 出行互联类接口 | 获取车机屏幕信息、摄像头信息，监听连接状态 |

## 权限要求

具体权限要求请参考各开发指导文档。

## 约束与限制

- 仅在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）提供服务
- 从 4.1.0(11) 开始支持 Phone 设备
- 从 6.1.0(23) 开始新增支持 Tablet 设备
- 暂不支持模拟器

## 官方链接

- [Car Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/car-introduction)
- [Car Kit 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/car-kit-guide)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/car-preparations)
