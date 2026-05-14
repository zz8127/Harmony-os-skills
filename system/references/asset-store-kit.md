# Asset Store Kit

## 概述

Asset Store Kit（关键资产存储服务，简称 ASSET）提供用户短敏感数据的安全存储及管理功能。短敏感数据包括密码类（账号/密码）、Token 类（应用凭据）以及其他关键明文（如银行卡号）等长度较短的敏感信息。

关键资产的安全存储依赖底层通用密钥库系统，加/解密操作及访问控制校验均在安全环境（如可信执行环境）中完成，即使系统被攻破也能保证用户敏感数据不发生泄露。加/解密使用 AES256-GCM 算法。

## 核心能力

### 访问控制

- **基于属主的访问控制**：所有关键资产受属主访问控制保护，只允许关键资产被其属主访问。属主身份由 ASSET 从系统服务中获取，即使业务身份被仿冒也无法获取其他业务数据。
- **基于群组的访问控制**：同一开发者开发的多个应用可配置为同一群组，设置群组共享后群组内多个应用可互通访问数据。群组信息由开发者 ID 和群组 ID 组成。
- **基于锁屏状态的访问控制**：三种保护等级（安全性递增）：
  - 开机后可访问
  - 首次解锁后可访问（默认）
  - 屏幕处于解锁状态时可访问
- **基于锁屏密码设置状态的访问控制**：用户设置了锁屏密码后才允许访问。
- **基于用户认证的访问控制**：用户身份认证通过后允许访问，支持指纹、人脸、PIN 码，认证有效期最长 10 分钟。

### 数据管理

- 关键资产以密文形式存储在 ASSET 数据库中，以业务身份 + 别名作为唯一索引
- 预留 12 个关键资产自定义属性（DATA_LABEL 开头），支持 JSON 拼接扩展
- DATA_LABEL_CRITICAL 开头的属性受完整性保护，写入后不支持更新
- 批量查询建议每次不超过 40 条

## npm 包名

`@kit.AssetStoreKit`

## 关键 API

| API | 说明 |
|---|---|
| `@ohos.security.asset` | 关键资产存储服务 ArkTS API |
| `asset.add` | 新增关键资产 |
| `asset.get` | 查询关键资产 |
| `asset.update` | 更新关键资产 |
| `asset.remove` | 删除关键资产 |
| `asset.query` | 批量查询关键资产 |
| C/C++ Asset API | 关键资产存储服务 Native API |

## 权限要求

无需额外权限申请，访问控制由 ASSET 系统内部管理。

## 约束与限制

- 轻量级智能穿戴设备暂不支持
- 每条关键资产别名需唯一
- 单条关键资产不超过 1KB，超长数据请使用通用密钥库系统或加解密算法库框架
- 不支持沙箱应用、应用分身存储或访问群组数据
- IS_PERSISTENT 为 True 的关键资产不允许设置为群组共享
- 应用卸载时清除数据（IS_PERSISTENT 为 true 的数据保留）
- 支持模拟器

## 官方链接

- [Asset Store Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/asset-store-kit-overview)
- [Asset Store Kit 开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/asset-store-kit)
- [@ohos.security.asset 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-asset)
