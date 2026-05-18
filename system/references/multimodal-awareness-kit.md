# Multimodal Awareness Kit（多模态融合感知服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/multimodalawareness-kit-intro

## 概述

多模态融合感知是利用设备上的多种传感器数据（如加速度计和陀螺仪等）来识别活动、状态和姿态等信息，例如判断设备是否处于静止状态。

## 核心能力

- **设备状态识别**：静止、运动、姿态等状态检测
- **活动识别**：行走、跑步、静止等活动识别
- **场景感知**：基于多传感器融合的智能感知

## 运作机制

应用向系统发起订阅服务，系统实时将设备状态结果上报给应用，业务场景结束时主动取消订阅。

## 约束与限制

- 需要用户申请相关权限
- 设备需要支持对应能力所需的传感器

## 支持的设备

Phone、Tablet、PC/2in1、Wearable

## 模拟器支持情况

支持模拟器，但与真机存在部分能力差异。

## 相关 Kit

- Sensor Service Kit：传感器服务
- Input Kit：多模输入服务

## API 参考

| API | 说明 |
|-----|------|
| @ohos.multimodalAwareness | 多模态融合感知 |
