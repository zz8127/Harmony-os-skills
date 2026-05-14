# Distributed Service Kit

## 概述

Distributed Service Kit（分布式管理服务）实现了分布式设备管理、分布式硬件管理、分布式键鼠穿越、分布式组件管理等能力。该Kit是分布式业务的入口功能，只有完成认证后的设备之间才可以进行分布式业务。

## 核心能力

### 分布式设备管理

- 周边设备发现
- 设备认证
- 设备信息查询
- 设备状态监听

分布式设备管理作为系统基础服务，需要应用在业务场景中向系统主动发起请求，完成设备间的发现、认证、查询、监听等功能。

### 分布式硬件管理

- 跨设备硬件资源访问
- 分布式相机、扫描、图库等硬件能力共享

### 分布式键鼠穿越

- 跨设备键鼠共享
- 支持平板或2in1设备间键鼠操作

### 跨设备连接UIAbility

设备间登录同账号并组网成功后，应用可以跨设备拉起同应用的UIAbility，实现信息、字节流、图片和传输流的交互。

## 自由流转

在HarmonyOS中，跨多设备的分布式操作统称为流转，分为跨端迁移和多端协同两种场景。

### 跨端迁移

当使用情境发生变化时，用户可以选择新设备继续当前任务，原设备可按需退出。在应用开发层面，A端运行的UIAbility迁移到B端，B端继续任务，A端可按需退出。

| 特性 | 说明 |
|---|---|
| 应用接续 | 在另一个设备的同一个应用中快速切换，无缝衔接上一个设备的应用体验 |

### 多端协同

多个设备作为整体，提供比单设备更高效、沉浸的体验。多端上的不同UIAbility/ServiceExtensionAbility同时运行或交替运行实现完整业务。

| 特性 | 说明 |
|---|---|
| 跨设备拖拽 | 支持平板或2in1设备间拖拽文件、文本 |
| 跨设备剪贴板 | A设备复制文本，B设备粘贴 |
| 跨设备互通 | 跨设备相机、扫描、图库访问 |
| 投屏 | 扩展屏模式投播，双屏协作 |
| 投播 | 音频/视频投放到其他HarmonyOS设备播放 |
| 隔空传送 | 通过"一抓一放"实现跨端传输 |
| 碰一碰分享 | 碰一碰发起跨端分享，传输图片、共享Wi-Fi等 |

## npm 包名

@ohos.distributedDeviceManager（分布式设备管理）
@ohos.distributedHardwareManager（分布式硬件管理）

## 关键 API

| API | 说明 |
|---|---|
| deviceManager.createDeviceManager() | 创建设备管理实例 |
| DeviceManager.discoverNewDevices() | 发现周边设备 |
| DeviceManager.authenticateDevice() | 设备认证 |
| DeviceManager.getTrustedDeviceList() | 获取可信设备列表 |
| UIAbility.onContinue() | 跨端迁移回调 |
| UIAbility.onConnect() | 多端协同连接回调 |

## 权限要求

- ohos.permission.DISTRIBUTED_DATASYNC：分布式数据同步
- ohos.permission.ACCESS_SERVICE_DM：分布式设备管理访问
- 使用分布式设备管理需要用户进行相关权限申请

## 官方链接

- Distributed Service Kit简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributedservice-kit-intro
- 自由流转概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-overview
- 分布式设备管理开发指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/devicemanager-guidelines
- 跨设备连接UIAbility：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/abilityconnectmanager-guidelines
