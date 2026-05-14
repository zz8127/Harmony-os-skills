# HarmonyOS 应用开发导读

## 概述

HarmonyOS应用开发文档用于指导开发者通过HarmonyOS SDK提供的开放能力完成应用开发。从API 11（HarmonyOS NEXT Developer Preview1）开始，SDK以Kit维度提供丰富、完备的开放能力，涵盖六大领域。

## 开发范式

HarmonyOS采用声明式开发范式，核心语言为ArkTS（基于TypeScript扩展），UI框架为ArkUI（方舟UI框架）。应用模型基于Stage模型，以UIAbility为基本单元管理应用生命周期。

## 技术架构全景

HarmonyOS SDK开放能力按六大领域组织：

### 应用框架

- Ability Kit（程序框架服务）：UIAbility、ServiceExtensionAbility等应用模型能力
- ArkUI（方舟UI框架）：声明式UI开发框架，提供丰富的组件和动画能力

### 系统

- Universal Keystore Kit（密钥管理服务）：密钥全生命周期安全操作
- Network Kit（网络服务）：HTTP、WebSocket、Socket等网络通信能力
- Distributed Service Kit（分布式管理服务）：分布式设备管理、硬件管理、键鼠穿越

### 媒体

- Audio Kit（音频服务）：音频播放、录制、音量管理等
- Media Library Kit（媒体文件管理服务）：媒体资源访问与管理

### 图形

- ArkGraphics 2D（方舟2D图形服务）：2D图形绘制与显示
- Graphics Accelerate Kit（图形加速服务）：图形渲染加速

### 应用服务

- Game Service Kit（游戏服务）：游戏场景专属能力
- Location Kit（位置服务）：定位与地理围栏

### AI

- Intents Kit（意图框架服务）：意图识别与分发
- CANN Kit（CANN异构计算框架服务）：AI推理加速

## 应用模型

Stage模型是HarmonyOS推荐的应用模型，核心概念：

- UIAbility：应用界面的入口，管理界面生命周期
- ServiceExtensionAbility：后台服务扩展
- AbilityStage：HAP的加载阶段回调
- Context：应用上下文环境

## 开发工具

DevEco Studio是HarmonyOS应用开发的推荐IDE，提供：

- 工程创建与管理
- 应用签名
- 应用调试与预览
- 应用安装运行
- 性能分析（Profiler）

## API参考

API参考提供各Kit开放能力的全量组件和接口说明文档，帮助开发者快速查找指定接口的详细描述和调用方法。

## 官方链接

- 应用开发导读：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-guide
- API参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/development-intro-api
- 知识地图：https://developer.huawei.com/consumer/cn/app/knowledge-map/
