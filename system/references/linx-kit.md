---
name: Linx Kit
description: 灵犀加速库是一套性能优化开发框架，基于芯片底层架构实现软硬协同优化，通过对线程执行过程中的热点流程进行针对性优化，提升应用与游戏的流畅度和能效表现。
---

# Linx Kit

## 概述

Linx Kit（灵犀加速库）是一套性能优化开发框架，基于芯片底层架构实现软硬协同优化。通过对线程执行过程中的热点流程进行针对性优化，提升应用与游戏的流畅度和能效表现。核心原理在于通过帧间信息或 CPU 簇间信息的复用，利用灵犀 CPU 核进行高效计算，释放灵犀 CPU 核特有计算能力。

## 核心能力

| 能力 | 描述 |
|------|------|
| 游戏性能优化 | 游戏引擎复用帧间及 CPU 簇间数据，充分发挥灵犀 CPU 核算力 |
| 热点加速 | 针对线程执行热点流程进行优化，降低延迟、提升帧率 |
| 软硬协同 | 基于芯片底层架构，复用帧间/簇间信息 |

## 适用场景

- **高帧率游戏**：需要稳定高帧率输出的游戏应用
- **视频播放**：高画质视频解码播放
- **复杂 UI 交互**：重度动画和复杂界面交互场景

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone、Tablet、PC/2in1、TV、Car |
| 硬件要求 | 仅支持具备灵犀 CPU 核的目标设备 |
| 模拟器 | 不支持 |

> 不同设备支持的特性范围有差异，可通过 API 返回的错误码判断。

## 开发指南

官方文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/linx-kit-introduction

### 基础使用流程

```
1. 引入 Linx Kit C API（hotspot-accelerate）
2. 检查设备是否支持灵犀 CPU 核
3. 创建热点加速会话
4. 在游戏/应用热点流程中调用加速接口
5. 利用帧间/簇间信息复用进行高效计算
6. 结束会话释放资源
```

## 相关资源

- [hotspot-accelerate API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-hotspot-accelerate)
- [启用热点加速](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hotspot-accelerate-development)
- [linx_hotspot.h 头文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/capi-linx-hotspot-h)
