# Account Kit — 华为账号服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Account Kit（华为账号服务）提供简单、快速、安全的登录功能，让用户快捷地使用华为账号登录应用。用户授权后，Account Kit 可提供头像、昵称、手机号码等信息，帮助应用更了解用户。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 华为账号一键登录 | 获取手机号授权并完成登录，帮助应用建立用户体系或与现有用户体系对接 |
| 静默登录 | 已授权用户静默完成登录，无需再次交互 |
| 获取头像昵称 | 获取用户头像和昵称等基本开放信息 |
| 快速验证手机号 | 获取用户手机号信息 |
| 获取收货地址 | 获取用户已保存的收货地址 |
| 获取发票抬头 | 获取用户发票抬头信息 |
| 获取风险等级 | 获取用户风险等级信息 |
| 获取实名年龄段 | 获取用户实名认证的年龄段信息 |
| 未成年人模式 | 获取未成年人模式开启状态及年龄段信息，支持家长验证和引导开关 |

---

## 亮点特征

### 一键登录

- **便捷性**：一键完成登录和手机号授权，无需额外操作
- **全场景**：Phone、Tablet、PC/2in1、TV 设备登录体验一致，保障用户数据资产跨端延续
- **效率高**：无需单独集成 SDK，减少开发和运营成本

### 未成年人模式

- **便捷性**：统一管控入口，仅需一次设置，应用联动生效
- **全面守护**：仅允许访问适龄应用、增强隐私保护、限制设备使用时长等

---

## 基本概念

| 概念 | 说明 |
|------|------|
| OpenID | 应用维度用户标识符，华为账号用户在应用/元服务的唯一标识，不同应用获取的 OpenID 不同 |
| UnionID | 开发者维度用户标识符，同一开发者账号下所有应用获取的 UnionID 相同 |
| GroupUnionID | 关联主体账号组维度用户标识符，组内所有开发者应用获取的 GroupUnionID 相同 |
| permission | 数据或接口权限，判断应用是否能获取对应数据或调用对应接口 |
| scopes | scope 列表，用于获取用户数据（如 profile、quickLoginAnonymousPhone） |
| Authorization Code | 授权码，登录成功后返回，可换取 Access Token、Refresh Token、ID Token |
| Access Token | 访问凭证，访问被权限管控资源的应用级凭证 |
| ID Token | 用户身份凭证，OIDC 协议扩展，包含用户信息 |

---

## npm 包名

`@kit.AccountKit`

---

## 关键 API

| API | 说明 |
|-----|------|
| `@hms.core.authentication.HuaweiIDProvider` | 华为账号认证提供者 |
| `authentication` | 应用统一认证服务，支持登录和授权 |
| `HuaweiIdButton` | 登录按钮组件 |
| `LoginPanel` | 登录面板组件 |
| `getUserInfo` | 获取用户信息接口 |

---

## 权限要求

| 权限 | 说明 |
|------|------|
| `ohos.permission.GET_NETWORK_INFO` | 获取网络信息（系统授权） |

部分能力需在 AppGallery Connect 中配置 Client ID 和签名证书指纹。

---

## 设备支持

| 能力 | 支持设备 |
|------|----------|
| 获取头像昵称 | Phone、Tablet、PC/2in1、Wearable、TV |
| 获取手机号 | Phone、Tablet、PC/2in1、Wearable、TV |
| 获取收货地址 | Phone、Tablet、PC/2in1 |
| 获取发票抬头 | Phone、Tablet、PC/2in1 |
| 获取风险等级 | Phone、Tablet、PC/2in1、Wearable、TV |
| 获取实名年龄段 | Phone、Tablet、PC/2in1、Wearable、TV |
| 未成年人模式 | Phone、Tablet、PC/2in1、TV |
| 登录按钮组件 | Phone、Tablet、PC/2in1、TV |
| 登录面板组件 | Phone、Tablet、PC/2in1、TV |

---

## 约束与限制

- 模拟器仅支持 authentication 的登录和授权能力以及 HuaweiIdButton 登录组件
- OpenID 和 UnionID 严格区分大小写
- 需在 AppGallery Connect 中配置应用信息

---

## 官方链接

- [Account Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-introduction)
- [华为账号一键登录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-phone-unionid-login)
- [静默登录](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-silent-login)
- [获取头像昵称](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-get-avatar-nickname)
- [未成年人模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/account-overview-minorsprotection)
- [示例代码](https://gitcode.com/HarmonyOS_Samples/accountkit-samplecode-clientdemo-arkts)
