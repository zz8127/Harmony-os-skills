# File Manager Service Kit — 文件管理服务

> **适用版本**：HarmonyOS 5.1.0(18)+。兼容 API 18+。

## 概述

File Manager Service Kit（文件管理服务）为开发者提供文件管理相关能力，开发者通过 File Manager Service Kit 完成文件删除到回收站、获取文件图标、解析文件快捷方式等功能，满足用户对文件管理的多样性诉求。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 删除文件到回收站 | 删除公共目录的文件到回收站，支持恢复 |
| 获取文件图标 | 根据文件类型获取对应的文件图标 |
| 解析文件快捷方式 | 根据快捷方式文件解析出对应原文件的 URI |

---

## npm 包名

`@kit.FileManagerServiceKit`

---

## 关键 API

| API | 说明 |
|-----|------|
| `fileManagerService` | 文件管理服务主模块 |
| `deleteToTrash` | 删除文件到回收站 |
| `getFileIcon` | 根据文件类型获取文件图标 |
| `resolveShortcut` | 解析快捷方式文件获取原文件 URI |

---

## 权限要求

| 权限 | 说明 |
|------|------|
| `ohos.permission.FILE_ACCESS_MANAGER` | 文件访问管理权限（系统授权） |

---

## 约束与限制

| 项目 | 说明 |
|------|------|
| 支持设备 | 仅适用于手机、平板和 PC/2in1 |
| 支持地区 | 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外） |
| 模拟器 | 从 5.1.0(18) 版本开始支持模拟器运行调试 |

---

## 官方链接

- [File Manager Service Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/filemanagerservice-introduction)
- [删除文件到回收站](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/filemanagerservice-deletetotrash)
- [fileManagerService API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/filemanagerservice-arkts-filemanagerservice)
- [示例代码](https://gitcode.com/harmonyos_samples/file_manager_service_kit_samplecode_deletetotrash_arkts)
