# Input Kit（多模输入服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/input-overview

## 概述

Input Kit（多模输入服务）为多种输入设备提供服务，如触控板、触摸屏、鼠标、键盘等。通过对这些输入设备上报驱动事件的归一化处理，确保不同输入设备与用户交互体验统一和流畅。

## 核心能力

### 基础输入事件服务

- 触控板输入事件
- 触摸屏输入事件
- 鼠标输入事件
- 键盘输入事件

### 扩展功能

- 获取输入设备列表
- 改变鼠标光标样式

## 运作机制

多模输入能力作为系统为应用提供的基础服务，通过处理输入设备驱动事件，完成输入事件管理、接收、预处理、分发，最终上报给应用。

## 支持的设备

Phone、Tablet、PC/2in1

## 模拟器支持情况

支持模拟器，但与真机存在部分能力差异。

## 相关 Kit

- IME Kit：输入法服务
- Sensor Service Kit：传感器服务
- Multimodal Awareness Kit：多模态融合感知

## API 参考

| API | 说明 |
|-----|------|
| @ohos.multimodalInput | 多模输入基础能力 |
| @ohos.input_event_client | 输入事件客户端 |
