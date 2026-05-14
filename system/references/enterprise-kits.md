# 企业管理类 Kit 合集

本文件汇总 HarmonyOS 企业管理类 Kit，包括 MDM Kit、Enterprise Data Guard Kit、Desktop Extension Kit、Enterprise Space Kit、Screen Time Guard Kit。

---

## 一、MDM Kit（企业设备管理服务）

### 概述

MDM Kit 为企业 MDM（Mobile Device Management）应用提供设备管理 API，用于管理并保护公司设备上的数据和应用程序。企业 MDM 应用可通过集中管理、远程配置和监控保障设备和数据的安全性和稳定性，广泛应用于企业和政府机构。

### 核心能力

- 设备管理应用程序框架
- 基本设备管理能力
- 扩展的企业设备管理能力（HarmonyOS NEXT 设备）
- 通过 EnterpriseAdminExtensionAbility 调用 MDM Kit 接口

### npm 包名

`@kit.MDMKit`

### 关键 API

| API | 说明 |
|---|---|
| `EnterpriseAdminExtensionAbility` | 设备管理扩展能力 |
| `@ohos.enterprise.deviceManagement` | 企业设备管理 |
| `@ohos.enterprise.usbManager` | USB 管理 |
| 其他企业管控 API | 网络管控、应用管控、策略管理等 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- SDK 版本为 5.0.0（API 12）及以上
- 仅支持 Stage 模型
- 仅支持 HarmonyOS NEXT 设备
- 支持模拟器（与真机存在差异）

### 官方链接

- [MDM Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mdm-kit-intro)
- [MDM Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mdm-kit-guide)

---

## 二、Enterprise Data Guard Kit（企业数据保护服务）

### 概述

Enterprise Data Guard Kit 为企业安全管控类 MDM 应用提供关键信息资产（KIA）文件的识别、外发管控以及企业恢复密钥的管理能力，支撑企业构建完整的数据防泄漏解决方案，实现企业数据资产可知、可控、可追溯。

### 核心能力

- **文件分级管控**：文件扫描和分级标识、管控策略配置、文件外发管控、水印保护
- **恢复密钥管理**：企业恢复密钥的管理能力

### npm 包名

`@kit.EnterpriseDataGuardKit`

### 关键 API

| API | 说明 |
|---|---|
| 文件扫描 API | 启动文件扫描任务 |
| 文件分级标识 API | 设置文件属性标签 |
| 文件外发管控 API | 管控文件外发权限 |
| 恢复密钥 API | 企业恢复密钥管理 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅支持 PC/2in1（华为擎云系列）
- 文件扫描仅限于默认路径范围内的子目录
- 暂不支持模拟器

### 官方链接

- [Enterprise Data Guard Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataguard-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataguard-preparations)

---

## 三、Desktop Extension Kit（桌面拓展服务）

### 概述

Desktop Extension Kit 提供系统级统一的操作入口，支持应用快捷功能接入桌面。应用启动时或运行过程中，可通过本模块提供的接口接入状态栏和快捷栏，进行快捷操作。

### 核心能力

- 应用接入状态栏
- 应用接入快捷栏
- 快捷操作入口

### npm 包名

`@kit.DesktopExtensionKit`

### 关键 API

| API | 说明 |
|---|---|
| 状态栏接入 API | 应用接入系统状态栏 |
| 快捷栏接入 API | 应用接入系统快捷栏 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅适用于 PC/2in1 设备
- 暂不支持模拟器

### 官方链接

- [Desktop Extension Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/statusbar-extension-introduction)
- [应用接入状态栏](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/statusbar-extension-guide)
- [应用接入快捷栏](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/desktop-quickbar-extension-guide)

---

## 四、Enterprise Space Kit（企业数字空间服务）

### 概述

Enterprise Space Kit 为企业 MDM 应用提供空间管控、空间互传管控 API，用于企业空间灵活配置管理、空间互传文件发送策略管控。广泛应用于政府机构、大型科技企业、央国企、商业银行等"一机两用"、"一企多网"场景。

### 核心能力

- **空间互传管控**：设置空间数据外发审批信息、获取审批内容，管理空间文件外发事件
- **空间管理**：创建工作空间、移除工作空间、订阅空间事件、下发空间管理策略

### npm 包名

`@kit.EnterpriseSpaceKit`

### 关键 API

| API | 说明 |
|---|---|
| 空间互传 API | 空间数据外发审批与管控 |
| 空间管理 API | 创建/移除工作空间、订阅空间事件 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅支持 PC/2in1（华为擎云系列）
- 企业数字空间使能后，后台空间的公共目录数据可能无法访问
- 暂不支持模拟器

### 官方链接

- [Enterprise Space Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/enterprisespace-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/enterprisespace-preparations)

---

## 五、Screen Time Guard Kit（屏幕时间守护服务）

### 概述

Screen Time Guard Kit 在应用安全隐私保护前提下，为开发者提供屏幕使用时间管控、应用使用限制等开放能力，满足不同用户对时间管理多样化诉求。

### 核心能力

- **用户授权管理**：请求用户授权访问、取消授权访问、授权情况查询
- **应用选择页**：拉起半模态页面，用户可勾选想管理的应用
- **守护策略管理**：添加、修改、查询、删除、启动和停止时间策略
  - 起止时间策略：设定生效开始和结束时间
  - 总时长策略：限定时间长度内禁用或可用
  - 共享时长策略：限定应用总共使用时长
- **应用访问限制**：对选定应用进行立即生效的允许/禁止管理

### 基本概念

- **token**：被管控应用的唯一标识，不包含应用自身信息，保障隐私安全
- **guard strategy**：守护策略，分为起止时间策略、总时长策略和共享时长策略
- **管控范围**：所有应用都可被管控，除系统内置允许清单应用、管控发起应用本身、已授权管控应用和健康使用设备

### npm 包名

`@kit.ScreenTimeGuardKit`

### 关键 API

| API | 说明 |
|---|---|
| 用户授权管理 API | 请求/取消/查询授权 |
| 应用选择页 API | 拉起应用选择半模态页面 |
| 守护策略管理 API | 策略 CRUD 及启停 |
| 应用访问限制 API | 允许/禁止应用访问 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- 仅支持 Phone、Tablet
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅支持主空间调用，不支持隐私空间
- 不支持调用方的分身应用接入
- 支持模拟器（与真机存在差异）

### 官方链接

- [Screen Time Guard Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/screentimeguard-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/screentimeguard-preparations)
