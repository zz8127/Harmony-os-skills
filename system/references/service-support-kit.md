---
name: Service Support Kit
description: 服务与支持为企业应用提供设备硬件检测能力，通过对设备的屏幕、电池及主板等核心硬件状态信息进行检测，实现硬件信息快速评估、提升检测效率。
---

# Service Support Kit

## 概述

Service Support Kit（服务与支持）为企业应用提供设备硬件检测能力，通过对设备的屏幕、电池及主板等核心硬件状态信息进行检测，实现高效便捷的设备诊断。核心旨在提升旧机回收过程中的检测效率与客户体验，在门店二手回收场景中作为判断设备硬件状况的关键依据。

## 核心能力

| 能力 | 描述 |
|------|------|
| 屏幕检测 | 检测屏幕硬件状态，识别屏幕异常 |
| 电池检测 | 检测电池健康度和硬件状态 |
| 主板检测 | 检测主板核心硬件信息 |
| 硬件一致性校验 | 校验设备硬件信息一致性 |

## 典型应用场景

1. **门店二手回收**：快速评估设备硬件状况，作为回收定价依据
2. **设备诊断**：硬件信息快速评估，提升检测效率
3. **企业设备管理**：批量设备硬件状态检测

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone、Tablet |
| 模拟器 | 不支持 |

## 开发指南

官方文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-support-introduction

### 基础使用流程

```
1. 初始化 Service Support Kit
2. 调用硬件检测接口
3. 获取屏幕、电池、主板等硬件状态数据
4. 校验硬件一致性
5. 输出检测报告
```

## 相关资源

- [检测设备硬件一致性](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-support-devicedetection)
- [Service Support Kit 指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/service-support-kit)
