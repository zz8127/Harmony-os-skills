# Core File Kit（文件基础服务）

## 概述

Core File Kit 为开发者提供一套访问和管理应用文件和用户文件的能力，帮助用户更高效地管理、查找和备份各类文件。按文件所有者分为应用文件、用户文件和系统文件三类；按存储位置分为本地文件系统和分布式文件系统。

## 核心能力

### 应用文件
- 文件所有者为应用，包括应用安装文件、应用资源文件、应用缓存文件等
- 支持查看、创建、读写、删除、移动、复制、获取属性等操作
- 通过基础文件操作接口 `ohos.file.fs` 实现
- 应用沙箱隔离：每个应用映射出专属"应用沙箱目录"，提供隔离性和安全性

### 用户文件
- 文件所有者为登录终端设备的用户，包括图片、视频、音频、文档等
- 通过用户文件访问框架（File Access Framework）访问
- FilePicker：系统预置应用，提供文件选择和保存能力，无需配置权限
- FileManager：设备开发者可自定义文件管理器（不向三方应用开放）

### 文件分享
- 应用间通过 URI 或 FD（File Descriptor）方式共享文件
- 便携性：简化多应用间切换操作
- 高效性：快速完成文件传输
- 数据一致性：确保传输完整性和一致性
- 安全性：文件授权访问，防止非法获取或篡改

### 应用数据备份恢复
- 应用可接入数据备份恢复框架
- 通过配置文件定制备份恢复行为：是否允许备份恢复、备份哪些数据

### 分布式文件系统
- 提供跨设备的文件访问和拷贝能力
- 文件不一定存储在本地设备，可通过计算机网络与其它分布式设备相连

### 存储空间管理
- 获取当前应用的存储空间大小
- 获取指定文件系统的剩余空间大小和总空间大小

## npm 包

`@kit.CoreFileKit`

## 关键 API

| API | 说明 |
|-----|------|
| ohos.file.fs | 基础文件操作（读写、创建、删除、移动、复制等） |
| ohos.file.picker | 文件选择器（PhotoViewPicker / DocumentViewPicker / AudioViewPicker） |
| ohos.file.statvfs | 文件系统空间信息 |
| ohos.file.backup | 应用数据备份恢复 |
| ohos.file.share | 文件分享 |
| ohos.file.distributedFS | 分布式文件系统 |

## 权限要求

| 权限 | 说明 |
|------|------|
| ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY | 读写下载目录 |
| ohos.permission.READ_WRITE_DESKTOP_DIRECTORY | 读写桌面目录 |
| ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY | 读写文档目录 |
| ohos.permission.FILE_ACCESS_PERSIST | 文件访问持久化权限 |

使用 FilePicker 选择/保存文件无需配置权限。

## 与相关 Kit 的关系

- **Ability Kit**：用户文件访问框架依赖 Ability Kit 提供的 Extension 基础能力，受 Ability Kit 服务调度管理

## 官方链接

- [Core File Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/core-file-kit-intro)
- [应用文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-file)
- [应用沙箱目录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory)
- [选择用户文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/select-user-file)
- [分布式文件系统](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/distributed-fs-overview)
- [ohos.file.fs API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-file-fs)
