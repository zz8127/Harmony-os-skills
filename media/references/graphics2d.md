# ArkGraphics 2D

## 概述

ArkGraphics 2D（方舟2D图形服务）主要提供图形绘制与显示相关的能力。开发者可以基于一套统一的图形接口进行应用开发，使应用开发更简单、高效。

## 核心能力

### 图像效果处理

提供图像处理基本能力，包括亮度调节、模糊化、灰度调节、智能取色等。

对应API：@ohos.effectKit（图像效果）

### 色彩管理

提供管理抽象化色域对象的基础能力，包括色域创建、色域基础属性获取等。

对应API：
- @ohos.graphics.colorSpaceManager（色彩管理）
- @ohos.graphics.sendableColorSpaceManager（可共享的色彩管理）

### 可变帧率

提供针对不同形式内容指定帧率的能力，可用于开发者自绘制内容。

对应指南：可变帧率简介

### HDR高动态显示

提供高动态显示相关能力。

对应API：@ohos.graphics.hdrCapability（HDR能力）

### 自绘制（Drawing模块）

提供自绘制能力，开发者可自定义绘制实现UI效果，包括基础形状、文本、图片等。

对应API：@ohos.graphics.drawing（绘制模块）

### Native图形能力

提供图形绘制与显示相关的Native能力，包括：

- NativeWindow：原生窗口管理
- NativeBuffer：原生缓冲区管理
- NativeImage：原生图像管理
- NativeVsync：原生垂直同步
- Drawing（Native）：Native绘制模块

## 使用场景

- 图像效果处理：使用effectKit模块实现图像效果处理，提升用户浏览体验
- 设置图像色域：根据设计需求设置色域信息，实现广色域效果的绘制和显示
- 定制帧率场景：根据不同内容和需要定制帧率，如不同游戏场景设置不同帧率，平衡体验与功耗
- 自绘制场景：使用Drawing等模块实现ArkUI组件外的自定义组件或自定义UI效果

## 亮点特征

- 同个窗口支持多个帧率：为同个窗口不同内容定制不同绘制帧率，独立运行
- 帧率动态配置：支持三方框架根据UI场景动态请求绘制帧率，兼顾流畅体验与功耗
- 录制回放机制：支持录制命令缓存，对绘制指令回放，提升UI绘制跟手性
- 多种渲染后端：一次开发支持多种渲染绘制后端，降低多端适配成本

## npm 包名

@ohos.effectKit（图像效果）
@ohos.graphics.colorSpaceManager（色彩管理）
@ohos.graphics.drawing（绘制模块）
@ohos.graphics.hdrCapability（HDR能力）

## 关键 API

| API | 说明 |
|---|---|
| effectKit.createEffect() | 创建图像效果处理源 |
| effectKit.createBlur() | 创建模糊效果 |
| colorSpaceManager.create() | 创建色域对象 |
| drawing.Canvas | 画布对象，承载绘制操作 |
| drawing.Pen | 画笔对象，描述绘制轮廓样式 |
| drawing.Brush | 画刷对象，描述填充样式 |
| drawing.Path | 路径对象，描述几何形状 |
| drawing.Typeface | 字体对象 |
| drawing.Image | 图片对象 |

## 权限要求

ArkGraphics 2D不需要额外权限声明。

## 官方链接

- ArkGraphics 2D简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics2d-introduction
- 图形绘制与显示开发概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphic-drawing-overview
- Drawing模块API参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-apis-graphics-drawing
- effectKit API参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-effectkit
- 可变帧率简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/displaysync-overview
