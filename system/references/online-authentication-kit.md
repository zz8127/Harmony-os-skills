# Online Authentication Kit（在线认证服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/onlineauthentication-introduction

## 概述

Online Authentication Kit（在线认证服务）遵循 FIDO、FIDO2、IIFAA 和 SOTER 标准免密认证规范，提供免密身份认证的移动端能力。

## 支持的标准

### FIDO

国际主流免密认证标准，广泛应用于金融、证券等 APP。

### FIDO2 / 通行密钥（Passkey）

基于 FIDO2 标准协议实现的简单又安全的登录方式，支持指纹、人脸或手机解锁 PIN 码。

### IIFAA

互联网可信认证联盟免密技术规范，支持免密登录、免密支付等业务场景。

### SOTER

生物认证平台，已广泛应用于微信小程序/公众号、指纹支付等业务场景。

## 核心能力

### 免密身份认证

- **开通**：开通指纹/3D 人脸免密身份认证
- **认证**：使用指纹/3D 人脸进行免密身份认证
- **注销**：注销已开通的免密身份认证

### 通行密钥

- **注册**：使用身份认证特征创建应用或网页的通行密钥
- **本地免密认证**：使用通行密钥进行本地免密认证
- **跨设备扫码认证**：使用移动设备作为漫游认证器扫码认证

## 约束与限制

### 支持的国家和地区

中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。

### 支持的设备

Phone、PC/2in1、Tablet

### 能力使用限制

- 开发者应用需要部署相应的服务端
- 设备需要支持相应的生物特征（ATL4 级别认证可信等级）
- 移动端设备需要处于联网状态

## 模拟器支持情况

本 Kit 暂不支持模拟器。

## 相关 Kit

- User Authentication Kit：用户认证
- Universal Keystore Kit：密钥管理

## API 参考

| API | 说明 |
|-----|------|
| @ohos.fido | FIDO 免密认证 |
| @ohos.ifaa | IIFAA 免密认证 |
| @ohos.soter | SOTER 免密认证 |
| @ohos.passkey | 通行密钥认证 |
