# Health Service Kit — 运动健康服务

> **适用版本**：HarmonyOS 6.0.2(22)+。兼容 API 22+。

## 概述

Health Service Kit（运动健康服务）是为华为生态应用打造的基于华为账号和用户授权的运动健康数据开放平台。在获取用户授权后，开发者可以使用 Health Service Kit 提供的开放能力获取运动健康数据，基于多种类型数据构建运动健康领域应用与服务，为用户打造丰富、便捷、专业的运动健康场景体验。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 数据开放 | 支持丰富的健康数据类型和专业运动数据类型，如步数、心率等 |
| 服务开放 | 运动联动服务开放能力，支持穿戴设备和生态设备的运动联动与实时数据回传（待后续支持） |
| 模型开放 | 在基础运动健康数据之上进行最大摄氧量、训练负荷等数据分析的模型开放能力（待后续支持） |
| 数据平台 | 提供数据平台，助力开发者存储运动和健康类的数据 |
| 数据安全隐私合规 | 遵从适用法律法规，对隐私进行管理，进行个人数据全生命周期管理 |

---

## 应用服务生态

### 华为应用

- **华为运动健康 App**：提供专业运动记录与减脂塑形等训练课程，结合科学睡眠及健康服务
- **智慧生活 App**：华为 IoT 智能设备统一管理平台，实现智能设备互联互通

### 生态应用

- 运动&健身、医疗研究、保险等生态应用基于华为智能运动健康设备+华为运动健康数据平台，构建专业的场景化用户体验

---

## npm 包名

`@kit.HealthServiceKit`

---

## 关键 API

| API | 说明 |
|-----|------|
| `healthService` | 运动健康服务主模块 |
| 数据读取 API | 读取步数、心率等运动健康数据 |
| 数据写入 API | 写入运动健康数据到平台 |
| 运动联动 API | 穿戴设备运动联动与实时数据回传 |

---

## 权限要求

| 权限 | 说明 |
|------|------|
| 运动健康数据读取权限 | 需用户授权后获取 |
| 运动健康数据写入权限 | 需用户授权后获取 |
| 华为账号登录 | 基于华为账号体系 |

需在 AppGallery Connect 中申请运动健康服务并完成审核。

---

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持设备 | 仅适用于 Phone、Tablet、Wearable |
| 支持地区 | 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外） |
| 模拟器 | 从 6.0.2(22) 版本开始支持模拟器开发 |

### 模拟器差异

- 不支持 Wearable 应用开发
- 不支持运动健康联动服务、实时三环数据、手动同步数据
- 不支持运动健康 App 相关能力
- 默认开启隐私授权

---

## 官方链接

- [Health Service Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/health-service-kit-ability)
- [接入流程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/health-application-access)
- [申请运动健康服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/health-apply)
- [HUAWEI Health Service Kit 服务使用协议](https://developer.huawei.com/consumer/cn/doc/app/70941808)
