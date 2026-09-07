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
import { security } from '@kit.DeviceSecurityKit';

// 检测设备是否 root/越狱
let isSecure = await security.isDeviceSecure();

// 检测调试模式
let isDebug = await security.isDebugMode();
```

## API 26 新增（HarmonyOS 26.0.0）

### Release 阶段新增（Beta2 后）

- **图片内容证真能力**：用于图片内容真实性验证，防止 AI 生成/篡改图片欺骗：
  - 图片内容证真签名检测 API：检测图片中是否存在内容证真签名
  - 图片内容证真验证 API：验证图片中内容证真签名
  - 图片内容证真签名信息提取 API：从验签数据中提取签名信息

### Beta2 阶段新增（已包含在 Release 中）

- **审计事件扩展**：新增设备开关机、音频接口插拔、视频接口插拔、账户管理等通知类审计事件；新增应用进程执行、文件读结束的阻断类审计事件
- **审计策略增强**：新增支持审计阻断类事件设置默认超时阻断策略、全量查询阻断类/通知类客户端信息

## 官方参考

- DeviceSecurityKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/device-security-overview-V5
