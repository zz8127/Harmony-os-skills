# Data Loss Prevention Kit（数据保护服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dlp-overview

## 概述

Data Loss Prevention Kit（数据防泄漏服务，简称 DLP）是系统提供的系统级数据防泄漏解决方案，提供文件权限管理、加密存储、授权访问等能力。

## 核心能力

- **文件权限管理**：数据所有者可基于账号认证对机密文件进行权限配置
- **加密存储**：机密文件通过密文存储
- **授权访问**：支持只读、编辑、拥有者等权限设置

## 运作流程

1. **DLP 文件生成**：文件所有者配置权限 → 策略信息封装 → 云端认证 → 生成 DLP 文件
2. **DLP 文件发送**：通过任何途径分享给目标用户
3. **DLP 文件打开**：授权者打开文件 → 解析凭据 → 云端认证 → 安装沙箱分身 → 安全访问

## 约束与限制

### 支持的设备

本 Kit 适用于 Phone、PC/2in1 设备。

## 模拟器支持情况

本 Kit 暂不支持模拟器。

## 相关 Kit

- Device Certificate Kit：设备证书服务
- Universal Keystore Kit：密钥管理服务
- Asset Store Kit：关键资产存储

## API 参考

| API | 说明 |
|-----|------|
| @ohos.dlpPermission | 数据防泄漏权限管理 |
