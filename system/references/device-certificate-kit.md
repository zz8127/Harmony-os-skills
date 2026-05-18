# Device Certificate Kit（设备证书服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-certificate-kit-intro

## 概述

Device Certificate Kit（设备证书服务）面向应用开发者，提供了证书算法库和证书管理的能力。

## 核心能力

### 证书算法库

提供接口用于解析和验证数字证书：

- 证书、证书扩展域段、证书吊销列表的解析及校验
- 证书链的校验能力

**常见场景**：应用对服务端证书或用户输入的证书进行解析和校验。

### 证书管理

提供系统级证书管理能力：

- 应用证书凭据的安装、获取、使用及删除
- 用户 CA 证书的安装、获取及删除
- 拉起证书管理应用界面对 CA 证书、凭据进行管理

**常见场景**：

- 业务安装应用证书凭据，用于网络链接双向认证
- 业务安装用户 CA 证书，校验对端身份

## 与相关 Kit 的关系

- 依赖 Crypto Architecture Kit 进行加解密
- 依赖 Universal Keystore Kit 管理密钥

## 约束与限制

Device Certificate Kit 不具备生成或签发证书及证书吊销列表的能力。

## 模拟器支持情况

本 Kit 支持模拟器。

## API 参考

| API | 说明 |
|-----|------|
| @ohos.deviceCertificate | 证书算法库 |
| @ohos.certManager | 证书管理 |
