---
name: Enterprise Foundation Kit
description: 企业办公服务面向企业应用提供组织生产力开发能力，当前开放企业场景下的应用沙箱数据与用户数据的备份和还原，支撑教学、办公等场景的批量部署。
---

# Enterprise Foundation Kit

## 概述

Enterprise Foundation Kit（企业办公服务）面向企业应用，提供组织生产力开发能力，助力企业开发者高效构建安全合规的企业应用。从 API 26.0.1 起开放首项能力：企业场景下的数据备份与还原。

典型场景：企业 MDM 应用（如教学场景下对教学环境进行备份和批量还原的应用）在待备份设备端备份应用沙箱数据和用户数据，通过网络或存储介质复制到待还原设备，再在待还原设备端执行还原，实现快速批量部署。

## 核心能力

| 能力 | 描述 |
|------|------|
| 用户数据备份 | 查询待备份用户数据大小、备份用户数据、还原用户数据 |
| 应用沙箱数据备份 | 查询可备份应用列表、查询待备份应用沙箱数据大小、备份与还原应用沙箱数据 |
| 进度与取消 | 备份/还原过程通过进度回调上报进度，支持取消备份或还原操作 |

## npm 包名

`@kit.EnterpriseFoundationKit`

- 业务模块：`@hms.pcService.enterpriseDeployRestore`（`enterpriseDeployRestore`）
- 系统能力：`SystemCapability.PCService.EnterpriseDeployRestore`

## 关键 API

| API | 说明 |
|-----|------|
| `getUserBackupDataSize()` | 获取待备份用户数据量大小（Promise） |
| `backupUserData(dest, progressCallback)` | 备份用户数据（Promise） |
| `restoreUserData(src, progressCallback, options)` | 还原用户数据（Promise） |
| `getAllowedBackupAndRestoreBundleList()` | 获取可备份或还原的应用信息列表（`BundleInfo[]`） |
| `getBundlesBackupDataSize(bundleList)` | 获取待备份应用沙箱数据量大小（Promise） |
| `backupBundles(bundleList, dest, progressCallback)` | 备份应用沙箱数据（Promise） |
| `restoreBundles(bundleList, src, progressCallback)` | 还原应用沙箱数据（Promise） |
| `cancelBackupRestore()` | 取消备份或还原操作（Promise） |

数据结构：`BundleInfo`（bundleName / versionCode / versionName）、`BackupRestoreProgressInfo`（备份或还原进度信息）、`BackupRestoreProgressCallback`、`RestoreUserDataOptions`。

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持国家/地区 | 仅中国境内（香港特别行政区、澳门特别行政区、中国台湾除外） |
| 支持设备 | 仅 PC/2in1 |
| 模拟器 | 不支持 |
| 模型约束 | 仅支持 Stage 模型 |
| 权限 | `ohos.permission.ENTERPRISE_MANAGE_BACKUP`（受限开放，仅企业普通应用与企业 MDM 应用可接入） |
| 默认路径 | 备份/还原目标路径需由应用自行管理，建议放在应用沙箱或企业指定目录 |

## 版本变更

| 版本 | 变更 |
|------|------|
| 26.0.1 Beta1（2026-11-10） | **全新 Kit**：新增企业办公服务，开放企业场景下的数据备份与还原能力（用户数据、应用沙箱数据的备份/还原、进度回调与取消） |

## 官方链接

- [Enterprise Foundation Kit 简介](https://developer.huawei.com/consumer/cn/doc/doccenter-capabilities/enterprises-foundation-introduction)
- [企业场景下的数据备份与还原](https://developer.huawei.com/consumer/cn/doc/doccenter-capabilities/enterprise-deploy-restore)
- [API 参考（enterprise-foundation）](https://developer.huawei.com/consumer/cn/doc/doccenter-references/api/enterprise-foundation)
