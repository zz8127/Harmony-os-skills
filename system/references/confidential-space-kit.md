---
name: Confidential Space Kit
description: 机密空间服务提供在机密空间内部运行数据应用、处理隐私数据的能力，支持应用与系统、应用与应用在空间内安全地共享数据，防止隐私信息外泄。
---

# Confidential Space Kit

## 概述

Confidential Space Kit（机密空间服务）为应用提供在对外隔离的计算环境中运行数据应用的系统能力。数据应用是机密空间内的独立程序，可使用应用从空间外发送的数据或系统/其他应用引入空间的数据，但从空间向外发送的数据量被严格管控，从而避免用户隐私泄漏。

## 核心能力

| 能力 | 描述 |
|------|------|
| 隐私计算隔离 | 在机密空间内运行独立的数据应用，与外部环境隔离 |
| 安全数据共享 | 支持应用与系统、应用与应用在空间内安全共享数据 |
| 出口数据管控 | 严格管控从空间向外的数据传输，防止隐私外泄 |
| 自定义程序逻辑 | 开发者可自行编写程序逻辑放入机密空间内计算 |

## 典型应用场景

1. **风控场景**：多方用户数据联合风控计算，原始数据不出域
2. **反诈场景**：在不暴露用户隐私的前提下进行反诈数据分析
3. **隐私安全计算**：涉及多方敏感数据的协同计算

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持国家/地区 | 仅中国境内（香港、澳门、台湾除外） |
| 支持设备 | Phone、Tablet、PC/2in1 |
| 模拟器 | 不支持 |

## 开发指南

官方文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/confidentialspace-introduction

### 基础使用流程

```
1. 初始化 Confidential Space Kit
2. 将数据应用部署到机密空间
3. 从空间外向机密空间发送数据
4. 机密空间内数据应用执行计算逻辑
5. 计算结果回传至空间外应用（受出口管控）
```

## 相关资源

- [@hms.security.confidentialSpace API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/confidentialspace-confidentialspace)
- [运行数据应用处理数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/confidentialspace-calling)
- [Confidential Space Kit 术语](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/confidentialspace-glossary)
