# MDM Kit（企业设备管理服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/mdm-kit-intro

## 概述

MDM Kit（企业设备管理服务）为企业 MDM（Mobile Device Management）应用提供设备管理 API，用于管理并保护公司设备上的数据和应用程序。

## 业务场景

### 企业派发设备场景（COPE）

企业统一购买设备并分发给员工使用，设备所属权属于企业，企业进行统一管理。

### 自带设备办公场景（BYOD）

企业允许员工携带自有设备接入办公环境，用于企业办公或外来访客访问场景。

## 核心能力

- 集中管理设备配置
- 远程配置策略
- 监控设备状态
- 保障设备和数据安全

## 实现原理

设备管理应用通过 EnterpriseAdminExtensionAbility 调用 MDM Kit 中的接口，实现管理设备的意图。

## 约束与限制

- SDK 版本为 5.0.0（API 12）及以上
- 仅支持 Stage 模型
- 仅支持 HarmonyOS NEXT 设备

## 模拟器支持情况

本 Kit 支持模拟器。

## 相关 Kit

- Enterprise Data Guard Kit：企业数据保护
- Enterprise Space Kit：企业数字空间
- Enterprise Threat Protection Kit：企业威胁防护

## API 参考

| API | 说明 |
|-----|------|
| @ohos.enterpriseDeviceManagement | 企业设备管理 |
| @ohos.enterpriseAdminExtension | 企业管理员扩展能力 |

## 26.0.1 Beta1 新增（2026-11-10）

> 26.0.1 是 26.0.0 的增量版本，仅供尝鲜；Beta 版 DevEco Studio 开发的应用不能上架应用市场。

### 系统管理

- **网络打印机白名单策略**：新增基于 IP 的网络打印机白名单策略管理，支持以设备视角或用户视角进行添加、删除、查询
- **精确定时器管理**：支持定时器的创建、启动、停止、销毁，适用于企业设备需精确定时执行任务的场景

### 安全管理

- **锁屏弱密码库设置**：支持设置锁屏弱密码校验的弱密码库，设置弱密码库后，用户无法在设置锁屏密码时使用库中包含的弱密码

### 应用管理

- **待机资源豁免**：支持为指定应用申请待机资源豁免，申请成功后应用在设备进入待机模式时可继续使用被豁免资源（如网络访问）
- **添加卡片到桌面**：支持将指定卡片添加到当前用户的桌面
