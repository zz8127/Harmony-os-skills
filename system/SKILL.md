---
name: harmonyos-system
description: |
  HarmonyOS 系统能力开发规范。涉及设备硬件和基础系统服务的开发指南。
  触发场景：开发涉及蓝牙、Wi-Fi、NFC、定位、传感器、电源管理、网络、后台任务、文件管理等系统能力时。
  包含：蓝牙(BLE/BR-EDR)、Wi-Fi、位置服务(LocationKit)、传感器(SensorServiceKit)、NFC、设备标识、电源管理、网络开发(NetworkKit)、后台任务(BackgroundTasksKit)、文件管理(CoreFileKit)等系统能力。
---

# HarmonyOS 系统能力

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 快速导航

| 分栏 | 文档 | 说明 |
|------|------|------|
| 短距通信 | [蓝牙BLE](references/ble.md) | 低功耗蓝牙扫描/广播/连接 |
| 短距通信 | [蓝牙设置](references/bluetooth-bredr.md) | 传统蓝牙BR/EDR开关/配对/状态 |
| 网络 | [Wi-Fi](references/wifi.md) | Wi-Fi扫描/连接/事件订阅 |
| 网络 | [NFC](references/nfc.md) | NFC读卡/写卡/NDEF |
| 位置 | [位置服务](references/location.md) | GNSS/Wi-Fi/蓝牙定位、地理围栏 |
| 传感器 | [传感器](references/sensor.md) | 加速度/陀螺仪/计步/环境光等 |
| 电源 | [电源管理](references/power.md) | 休眠/亮灭屏/充电状态 |
| 安全 | [设备安全](references/device-security.md) | 安全区域/生物识别/安全检测 |
| 设备 | [设备标识](references/device-info.md) | 设备标识/网络信息 |
| 网络 | [网络开发](references/network.md) | HTTP/RCP/WebSocket/网络状态 |
| 后台 | [后台任务](references/background-task.md) | 短时/长时/延迟任务/代理提醒 |
| 文件 | [文件管理](references/file-management.md) | 应用沙箱/文件读写/FilePicker |
| 基础服务 | [基础服务](references/basic-services.md) | 窗口管理/剪贴板/屏幕亮度 |
| 安全 | [密钥管理](references/keystore.md) | HUKS密钥/证书/加解密 |
| 分布式 | [分布式能力](references/distributed.md) | 设备迁移/跨设备剪贴板/数据同步 |
| 安全 | [关键资产存储](references/asset-store-kit.md) | 关键资产安全存储/加密管理 |
| 车载 | [车服务](references/car-kit.md) | 车机出行/HiCar互联/导航流转 |
| 安全 | [安全类Kit](references/security-kits.md) | DLP/设备证书/在线认证/用户认证 |
| 并发 | [并发调度](references/ffrt-kit.md) | FFRT数据依赖异步并发任务 |
| 输入 | [多模输入+融合感知](references/input-multimodal-kit.md) | 多输入设备/传感器融合感知 |
| 通信 | [星闪](references/nearlink-kit.md) | NearLink低功耗高速短距通信 |
| 网络 | [网络加速+远场通信](references/network-boost-remote-kit.md) | 网络加速/感知/HTTP/RPC |
| 企业 | [企业管理Kit](references/enterprise-kits.md) | MDM/数据保护/状态栏/空间管控/屏幕时间 |
| 驱动 | [驱动开发](references/driver-kit.md) | 外设驱动/DriverExtension/USB/HID |
| 穿戴 | [穿戴服务](references/wear-engine-kit.md) | 华为穿戴设备开放能力 |
| 地图 | [地图服务](references/map-kit.md) | MapKit：地图/标记/导航 |
| 扫码 | [扫码服务](references/scan-kit.md) | ScanKit：扫码/码识别/直达服务 |
| 分享 | [分享服务](references/share-kit.md) | ShareKit：系统分享面板 |
| 通信 | [电话蜂窝](references/telephony-kit.md) | TelephonyKit：电话/蜂窝通信 |
| 安全 | [加密框架](references/crypto-architecture.md) | CryptoArchitectureKit：加解密/签名 |
| 协同 | [协同服务](references/service-collaboration-kit.md) | ServiceCollaborationKit：跨设备协同/跨端拍照/文档扫描 |
| 测试 | [应用测试](references/test-kit.md) | TestKit：单元测试/UITest/白盒性能 |
| 安全 | [企业威胁防护](references/enterprise-threat-protection-kit.md) | EnterpriseThreatProtectionKit：文件扫描/隔离/恢复/删除 |
| 算法 | [算法加速](references/fast-kit.md) | FASTKit：高阶数据结构/规划求解/数字信号处理 |
| 健康 | [运动健康](references/health-service-kit.md) | HealthServiceKit：步数/心率/运动联动/训练负荷 |
| 天气 | [天气服务](references/weather-service-kit.md) | WeatherServiceKit：天气预报/降水/预警/指数 |

---

## 核心 API Kit

| Kit 名称 | npm 包 | 说明 |
|---------|-------|------|
| ConnectivityKit | `@kit.ConnectivityKit` | 蓝牙、Wi-Fi、NFC、网络连接 |
| LocationKit | `@kit.LocationKit` | 定位服务 |
| SensorServiceKit | `@kit.SensorServiceKit` | 传感器 |
| AccountKit | `@kit.AccountKit` | 华为账号 |
| NetworkKit | `@kit.NetworkKit` | HTTP、WebSocket、网络状态 |
| BackgroundTasksKit | `@kit.BackgroundTasksKit` | 后台任务管理 |
| CoreFileKit | `@kit.CoreFileKit` | 文件管理、应用沙箱 |
| BasicServicesKit | `@kit.BasicServicesKit` | 窗口、剪贴板、系统属性 |
| UniversalKeystoreKit | `@kit.UniversalKeystoreKit` | 密钥管理、加解密 |
| DistributedKit | `@kit.DistributedKit` | 设备发现、迁移、数据同步 |
| MapKit | `@kit.MapKit` | 地图、标记、导航 |
| ScanKit | `@kit.ScanKit` | 扫码、码识别 |
| ShareKit | `@kit.ShareKit` | 系统分享面板 |
| TelephonyKit | `@kit.TelephonyKit` | 电话、蜂窝 |
| CryptoArchitectureKit | `@kit.CryptoArchitectureKit` | 加密框架 |
| AssetStoreKit | `@kit.AssetStoreKit` | 关键资产安全存储 |
| CarKit | `@kit.CarKit` | 车服务 |
| FfrtKit | `@kit.FfrtKit` | 并发调度 |
| NearLinkKit | `@kit.NearLinkKit` | 星闪通信 |
| DriverDevelopmentKit | `@kit.DriverDevelopmentKit` | 驱动开发 |
| WearEngineKit | `@kit.WearEngineKit` | 穿戴设备 |
| ServiceCollaborationKit | `@kit.ServiceCollaborationKit` | 跨设备协同 |
| TestKit | `@kit.TestKit` | 应用测试框架 |
| EnterpriseThreatProtectionKit | `@kit.EnterpriseThreatProtectionKit` | 企业威胁防护 |
| FASTKit | `@kit.FASTKit` | 算法加速 |
| HealthServiceKit | `@kit.HealthServiceKit` | 运动健康数据 |
| WeatherServiceKit | `@kit.WeatherServiceKit` | 天气数据服务 |

---

## 权限总览

| 能力 | 权限名 |
|------|--------|
| 蓝牙 | `ohos.permission.ACCESS_BLUETOOTH` |
| 定位 | `ohos.permission.LOCATION` |
| 传感器 | `ohos.permission.ACCELEROMETER` 等 |
| Wi-Fi | `ohos.permission.GET_WIFI_INFO` |
| NFC | `ohos.permission.NFC_TAG` |
| 网络 | `ohos.permission.INTERNET` |
| 后台任务 | `ohos.permission.KEEP_BACKGROUND_RUNNING` |

> 注意：从 HarmonyOS NEXT 起，部分权限从 user-grant 改为 system-grant，具体以官方文档为准。

---

## API 24 Beta1 变更追踪（2026-04-30）

| Kit | 变更 |
|-----|------|
| Performance Analysis Kit | 资源采集和崩溃日志分析增强 |
| Enterprise Threat Protection Kit | **全新 Kit** — 企业威胁防护服务 |

---

## 官方参考

- ConnectivityKit（短距通信）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/bluetooth-overview
- LocationKit（位置服务）：https://developer.huawei.com/consumer/cn/doc/atomic-ascf/develop-location-retrieval
- SensorServiceKit（传感器）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/sensor-V5
- Wi-Fi：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wifi-overview-V5
- 设备标识：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-identifier-V14
- NetworkKit（网络服务）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/http-request-overview-V5
- BackgroundTasksKit（后台任务）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/background-task-overview-V5
- CoreFileKit（文件管理）：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit-intro
