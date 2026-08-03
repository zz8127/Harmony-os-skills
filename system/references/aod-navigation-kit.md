---
name: AOD Navigation Kit
description: 熄屏导航服务提供应用接入熄屏导航的能力，在保障导航实时性的同时有效控制设备功耗，支持轨迹、里程等关键导航信息在设备熄屏界面无需解锁即可便捷查看。
---

# AOD Navigation Kit

## 概述

AOD Navigation Kit（熄屏导航服务）提供应用接入熄屏导航的能力，在保障导航实时性的同时有效控制设备功耗。支持轨迹、里程等关键导航信息在设备熄屏界面（AOD，Always On Display）无需解锁即可便捷查看，为户外导航类应用提供低功耗长续航解决方案。

## 核心能力

| 能力 | 描述 |
|------|------|
| 熄屏地图绘制 | 在熄屏显示页面绘制离线地图、预设轨迹线、实时轨迹线及关键导航信息 |
| 低功耗数据代理 | 代理计算里程、步数、步频、全程耗时、运动耗时、累计爬升/下降、速度、配速等数据项 |
| 语音播报下沉 | 里程播报、时间播报、偏航事件、GPS 定位、累计爬升/下降、速度、标记点播报 |

## 接入方式

### 方式一：熄屏导航状态下应用休眠

- 应用进入休眠，由 AOD 模块代理导航业务并进行数据显示
- 功耗收益约 **50%**（对比亮屏导航）
- 能力约束：不支持联网、无法连接 wearable 设备、仅提供固定范围数据项代理
- 亮屏后 AOD 将熄屏期间代理产生的导航数据回传给应用合并

### 方式二：熄屏导航状态下应用保活

- 应用不进入休眠，熄屏导航数据仍来源于应用
- 功耗收益约 **20%**（对比亮屏导航）
- 无能力约束：可联网、可连接 wearable 设备（步数、心率等）
- AOD 模块仅进行熄屏界面数据项显示

## 亮点

1. 低功耗导航代理，户外场景功耗优化约 50%
2. 熄屏界面实时显示导航路线、轨迹、里程、耗时，无需解锁

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone |
| 模拟器 | 不支持 |

## 开发指南

官方文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aodnavigation-introduction

### 基础使用流程

```
1. 申请权限并初始化 AOD Navigation Kit
2. 设备熄屏前，将亮屏期间导航数据下发给 AOD Navigation Kit
3. 选择接入方式（休眠代理 / 应用保活）
4. 熄屏期间 AOD 模块代理导航 / 应用定时刷新数据
5. 设备亮屏后退出熄屏导航
6. 接收回传数据并合并（休眠模式）
```

## 相关资源

- [aodNaviManager API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/aodnavigation-aodnavimanager)
- [接入熄屏导航](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aodnavigation-development-guidance)
- [AOD Navigation Kit 术语](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aodnavigation-glossary)
