# DevEco Service — ohpm-repo 私仓搭建工具

## 概述

ohpm-repo 是一个搭建轻量级 ohpm 私仓服务的工具，与 ohpm 包管理器兼容，按需缓存所有依赖项，加速私有网络中的安装。适用于企业内部三方库私有化管理场景。

## 核心能力

### 私有性
- 发布的三方库均为私有，只能根据配置进行访问
- 支持细粒度的访问控制策略

### 缓存
- 根据需要缓存所有依赖项
- 加快私有网络中的安装速度
- 减少对外部网络的依赖

### 部署模式
- **单点部署**：ohpm-repo 仅部署在一台机器上使用，适合小团队
- **多实例部署**：部署到多台机器中，具有相同的配置内容，共享数据存储空间，适合大规模企业
- 单点部署数据可迁移至多实例部署（参考数据迁移指导）

## npm 包

无独立 npm 包，ohpm-repo 为独立命令行工具，随 DevEco Studio 安装提供。

## 关键命令

| 命令 | 说明 |
|------|------|
| ohpm-repo start | 启动 ohpm-repo 服务 |
| ohpm-repo remove_instance | 移除实例 |

## 权限要求

无 HarmonyOS 应用权限要求，ohpm-repo 为服务端工具。

## 官方链接

- [ohpm-repo 概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-overview)
- [快速开始](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-quickstart)
- [单点部署](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-deploy-single-instance)
- [数据迁移指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-data-migration)
- [ohpm-repo start](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-start)
- [ohpm-repo remove_instance](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-ohpm-repo-remove_instance)
