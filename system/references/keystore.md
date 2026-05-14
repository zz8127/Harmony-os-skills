# Universal Keystore Kit (HUKS)

## 概述

Universal Keystore Kit（密钥管理服务，简称HUKS）向业务/应用提供各类密钥的统一安全操作能力，包括密钥管理（密钥生成/销毁、密钥导入、密钥证明、密钥协商、密钥派生）及密钥使用（加密/解密、签名/验签、访问控制）等功能。

HUKS管理的密钥可以由业务/应用导入或调用HUKS接口生成。HUKS提供密钥访问控制能力，确保存储在HUKS中的密钥被合法正确地访问。

## 整体架构

HUKS模块分为三大部分：

- SDK：提供密钥管理接口供开发者调用，支持ArkTS和C API
- HUKS服务层：实现密钥会话管理及存储管理
- HUKS核心层：承载核心功能，包括密钥密码学运算、明文密钥加解密、密钥访问控制

对于具备安全环境（TEE）的系统/设备，HUKS核心层运行在安全环境内，密钥明文仅在安全环境中访问，不会传递出安全环境。

## 核心能力

### 密钥生成

| 功能 | 说明 |
|---|---|
| 密钥生成 | 随机生成密钥，全生命周期内明文仅在安全环境中访问 |
| 密钥导入 | 将外部生成的密钥导入HUKS进行管理 |

### 密钥使用

| 功能 | 说明 |
|---|---|
| 加密/解密 | 使用密钥将数据加密为密文，或解密为明文 |
| 签名/验签 | 认证消息内容及发送者身份真实性 |
| 密钥协商 | 两个或多个实体共同建立会话密钥 |
| 密钥派生 | 从现有密钥派生一个或多个新密钥 |
| 访问控制 | 确保密钥不会被越权访问 |

### 密钥删除

| 功能 | 说明 |
|---|---|
| 密钥删除 | 安全地删除存储在HUKS中的密钥数据 |

### 密钥证明

| 功能 | 说明 |
|---|---|
| 密钥证明 | 为非对称密钥对中的公钥签发证书，证明密钥合法性 |

## npm 包名

@ohos.security.huks

## 关键 API

| API | 说明 |
|---|---|
| huks.generateKeyItem() | 生成密钥 |
| huks.importKeyItem() | 导入明文密钥 |
| huks.importWrappedKeyItem() | 导入加密包装的密钥 |
| huks.exportKeyItem() | 导出公钥 |
| huks.deleteKeyItem() | 删除密钥 |
| huks.encrypt() | 加密 |
| huks.decrypt() | 解密 |
| huks.sign() | 签名 |
| huks.verify() | 验签 |
| huks.agreeKey() | 密钥协商 |
| huks.deriveKeyItem() | 密钥派生 |
| huks.attestKeyItem() | 密钥证明 |
| huks.initSession() | 初始化密钥会话 |
| huks.updateSession() | 更新密钥会话数据 |
| huks.finishSession() | 结束密钥会话 |

## 权限要求

HUKS本身不需要额外权限声明，但基于用户身份认证的密钥访问控制依赖于User Authentication Kit。

## 与相关Kit的关系

- User Authentication Kit（用户身份认证）：提供基于用户身份认证的密钥访问控制
- Crypto Architecture Kit（加解密算法库框架）：提供轻量级加解密能力

## 官方链接

- HUKS简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-overview
- HUKS API参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-huks
- 密钥生成算法规格：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-key-generation-overview
- 加密/解密算法规格：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-encryption-decryption-overview
