# 认证服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 概述

AGC 认证服务提供多种登录方式的统一管理，支持匿名、邮箱、手机、华为账号及第三方登录。

---

## 支持的登录方式

| 方式 | 说明 | 配置要求 |
|------|------|---------|
| 匿名登录 | 无需用户信息，自动生成临时账号 | 开启匿名认证 |
| 邮箱账号 | 邮箱+密码注册/登录 | 开启邮箱认证 |
| 手机账号 | 手机号+验证码登录 | 开启手机认证 |
| 华为账号 | 一键华为账号登录 | 开启华为账号认证 |
| 第三方登录 | 微博/QQ/微信/Google/Facebook 等 | 配置第三方 AppID |

---

## 端侧代码

### 初始化

```typescript
import { AGConnectAuth } from '@kit.CloudFoundation';

// 获取认证实例
let auth = AGConnectAuth.getInstance();
```

### 匿名登录

```typescript
let result = await auth.signInAnonymously();
let user = result.getUser();
console.info('匿名用户 UID：' + user.getUid());
```

### 华为账号登录

```typescript
import { HuaweiIdAuthProvider } from '@kit.CloudFoundation';

let credential = HuaweiIdAuthProvider.credentialWithToken(huaweiIdToken);
let result = await auth.signIn(credential);
```

### 手机号登录

```typescript
import { PhoneAuthProvider } from '@kit.CloudFoundation';

// 请求验证码
let verifyCode = await PhoneAuthProvider.requestVerifyCode('+86', '13800138000');

// 验证码登录
let credential = PhoneAuthProvider.credentialWithVerifyCode(
  '+86', '13800138000', verifyCode, '123456'
);
let result = await auth.signIn(credential);
```

---

## 用户管理

| 操作 | 方法 |
|------|------|
| 获取当前用户 | `auth.getCurrentUser()` |
| 退出登录 | `auth.signOut()` |
| 删除用户 | `auth.deleteUser()` |
| 修改密码 | `user.updatePassword(newPassword)` |
| 绑定邮箱 | `user.link(EmailAuthProvider.credential(email, password))` |
| 解绑邮箱 | `user.unlink(EmailAuthProvider.PROVIDER_ID)` |

---

## 官方参考

- 认证服务：https://developer.huawei.com/consumer/cn/doc/agc-help/auth-service-introduction-0000001059260977
