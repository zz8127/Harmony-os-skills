# 安全类 Kit 合集

本文件汇总 HarmonyOS 安全类 Kit，包括 Data Loss Prevention Kit、Device Certificate Kit、Online Authentication Kit、User Authentication Kit。

---

## 一、Data Loss Prevention Kit（数据防泄漏服务）

### 概述

数据防泄漏服务（Data Loss Prevention，简称 DLP）是系统级的数据防泄漏解决方案，提供文件权限管理、加密存储、授权访问等能力。数据所有者可基于账号认证对机密文件配置权限（只读、编辑、拥有者），机密文件通过密文存储，在支持 DLP 机制的设备上通过端云协调进行认证授权。

DLP 是系统级别的，应用开发者只需做少量适配甚至无需适配即可获得完整的数据防泄漏保护。

### 核心能力

- **DLP 权限管理部件**：权限管理底层服务，负责沙箱应用创建和凭据管理交互
- **DLP 管理应用部件**：实现权限在本地的设置、检验和拦截功能
- **云端对接模块**（需开发者自行搭建）：将 DLP 文件证书发往云端完成基于账号的鉴权、证书生成及解密

### 关键 API

| API | 说明 |
|---|---|
| `@ohos.dlpPermission` | 数据防泄漏 ArkTS API |
| `DlpPermissionApi` | 数据防泄漏 C/C++ API |

### 权限要求

- `ohos.permission.ACCESS_DLP`

### 约束与限制

- 暂不支持模拟器
- 云端对接模块需开发者自行搭建

### 官方链接

- [数据防泄漏服务简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dlp-overview)
- [数据防泄漏服务开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dlp-guidelines)

---

## 二、Device Certificate Kit（设备证书服务）

### 概述

Device Certificate Kit 面向应用开发者提供证书算法库和证书管理能力。

### 核心能力

#### 证书算法库

- 证书、证书扩展域段、证书吊销列表（CRL）的解析及校验
- 证书链校验
- 屏蔽不同三方算法库差异，统一 API 接口

#### 证书管理

- 应用证书凭据的安装、获取、使用及删除
- 用户 CA 证书的安装、获取及删除
- 拉起证书管理应用界面对 CA 证书、凭据进行管理
- 证书全生命周期（安装、存储、使用和销毁）管理

### npm 包名

`@kit.DeviceCertificateKit`

### 关键 API

| API | 说明 |
|---|---|
| 证书算法库框架 API | 证书解析、校验、CRL 处理 |
| 证书管理 API | 凭据和 CA 证书的安装、获取、删除 |

### 权限要求

具体权限请参考各开发指导文档。

### 约束与限制

- 不具备生成或签发证书及证书吊销列表的能力
- 证书算法库依赖 Crypto Architecture Kit
- 证书管理依赖 Universal Keystore Kit
- 支持模拟器

### 官方链接

- [Device Certificate Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-certificate-kit-intro)
- [证书算法库框架](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/certificate-framework)
- [证书管理概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/certmanager-overview)

---

## 三、Online Authentication Kit（在线认证服务）

### 概述

Online Authentication Kit 遵循 FIDO、FIDO2、IIFAA 和 SOTER 标准免密认证规范，提供免密身份认证的移动端能力。用户应用接入后可使用生物特征（指纹、3D 人脸）代替密码，实现免密登录、免密支付等业务场景。

### 核心能力

#### FIDO

国际主流免密认证标准，广泛应用于各大银行、证券、金融 APP。

#### IFAA

IIFAA 互联网可信认证联盟本地免密技术规范，支持免密登录、免密支付。

#### SOTER

生物认证平台和标准，已广泛应用于微信小程序/公众号、指纹支付等场景。

#### 通行密钥（Passkey）

基于 FIDO2 标准协议实现的登录方式，支持：
- 通行密钥注册：使用人脸、指纹、PIN 码创建通行密钥
- 本地免密认证：使用通行密钥在本设备上免密认证
- 跨设备扫码认证：使用已注册通行密钥的移动设备作为漫游认证器

### npm 包名

`@kit.OnlineAuthenticationKit`

### 关键 API

| API | 说明 |
|---|---|
| FIDO API | FIDO 免密身份认证 |
| IFAA API | IFAA 免密身份认证 |
| SOTER API | SOTER 免密身份认证 |
| FIDO2/Passkey API | 通行密钥注册与认证 |

### 权限要求

- 需部署相应服务端
- 设备需支持 ATL4 级别的认证可信等级
- 使用时需联网

### 约束与限制

- 仅在中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅适用于 Phone、PC/2in1、Tablet
- 暂不支持模拟器

### 官方链接

- [Online Authentication Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/onlineauthentication-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/onlineauthentication-preparation)

---

## 四、User Authentication Kit（用户认证服务）

### 概述

User Authentication Kit 提供基于用户在设备本地注册的锁屏口令、人脸和指纹来认证用户身份的能力。提供系统级用户身份认证功能，以及多设备统一的、集多种认证方式于一体的系统级用户身份认证控件。

### 核心能力

- **归一化认证接口**：屏蔽不同认证因子差异，同一套接口提供人脸、指纹、锁屏口令组合认证
- **感知认证可信等级差异**：支持指定期望的认证可信等级（ATL1~ATL4）
- **业务自定义认证方式**：支持带导航键的认证界面，切换业务自定义认证界面
- **短时间内复用认证结果**：支持复用锁屏认证结果或任意应用身份认证结果（最长 5min）
- **系统级用户身份认证界面**：支持自定义标题和导航键文字，自适应屏幕状态
- **感知注册凭据变化**：从认证成功结果获取用户凭据状态

### 认证可信等级

| 等级 | 映射规则 | 典型场景 |
|---|---|---|
| ATL4 | ACL≥3, ASL≥2 | 小额支付 |
| ATL3 | ACL≥3, ASL≥1 或 ACL≥2, ASL≥2 | 设备解锁、应用登录 |
| ATL2 | ACL≥2, ASL≥1 或 ACL≥1, ASL≥2 | 维持设备解锁状态 |
| ATL1 | ACL=1, ASL=1 | 业务风控、精准推荐 |

### npm 包名

`@kit.UserAuthenticationKit`

### 关键 API

| API | 说明 |
|---|---|
| 用户认证 API | 发起用户身份认证 |
| 嵌入式用户身份认证控件 | 自定义认证 UI |

### 权限要求

- `ohos.permission.ACCESS_BIOMETRIC`（生物认证）

### 约束与限制

- 三方应用必须使用系统自带的身份认证控件
- 不允许三方应用在后台发起身份认证请求
- 支持模拟器

### 官方链接

- [User Authentication Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-authentication-overview)
- [用户身份认证开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/user-authentication-dev)
