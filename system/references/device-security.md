# 设备安全

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 生物识别

```typescript
import { userIAM } from '@kit.UserIAM.Kit';

// 检查生物识别可用性
let authTrustLevel = userIAM.getAuthTrustLevel();

// 生物认证（指纹/面部）
let authResult = await userIAM.userAuth.auth(
  { challenge: new Uint8Array([1, 2, 3]) },
  {
    authType: [userIAM.userAuth.AuthType.BIOMETRIC_ANY],
    authTrustLevel: userIAM.userAuth.AuthTrustLevel.ATL3
  }
);
```

## 防窥保护（API 23 新增）

`DeviceSecurityKit` 新增防窥保护能力，当检测到旁人注视屏幕时自动隐藏应用内容：

```typescript
import { dlpp } from '@kit.DeviceSecurityKit';

// 设置防窥保护
let config = {
  enable: true,
  sensitivity: 'HIGH'
};
dlpp.setPeepProtect(config);
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/devicesecurity-dlpantipeep

## 安全检测

```typescript
import { security from '@kit.DeviceSecurityKit';

// 检测设备是否 root/越狱
let isSecure = await security.isDeviceSecure();

// 检测调试模式
let isDebug = await security.isDebugMode();
```

## 官方参考

- DeviceSecurityKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-security-overview-V5
