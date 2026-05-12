# 权限与安全

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 权限分类

### 按授权方式分类

| 类型 | 说明 | 授权时机 |
|------|------|---------|
| system_grant | 系统授权 | 安装时自动授予 |
| user_grant | 用户授权 | 运行时动态申请 |

### 按APL等级分类

| APL等级 | 说明 | 第三方应用 |
|---------|------|-----------|
| normal | 普通权限 | 可直接申请 |
| system_basic | 基础系统权限 | 需申请签名证书 |
| system_core | 核心系统权限 | 仅系统应用可用 |

---

## system_grant 权限

| 权限名 | 说明 |
|--------|------|
| ohos.permission.INTERNET | 网络请求 |
| ohos.permission.GET_NETWORK_INFO | 获取网络信息 |
| ohos.permission.GET_WIFI_INFO | 获取WiFi信息 |
| ohos.permission.GYROSCOPE | 陀螺仪传感器 |
| ohos.permission.ACCELEROMETER | 加速度传感器 |
| ohos.permission.ACCESS_NOTIFICATION_POLICY | 通知策略 |

配置示例：

```json
{
  "requestPermissions": [
    {
      "name": "ohos.permission.INTERNET",
      "usedScene": {
        "abilities": ["EntryAbility"],
        "when": "always"
      }
    }
  ]
}
```

---

## user_grant 权限

| 权限名 | 说明 |
|--------|------|
| ohos.permission.LOCATION | 精确位置 |
| ohos.permission.CAMERA | 相机 |
| ohos.permission.MICROPHONE | 麦克风 |
| ohos.permission.READ_CONTACTS | 读取联系人 |
| ohos.permission.WRITE_CONTACTS | 写入联系人 |
| ohos.permission.READ_CALENDAR | 读取日历 |
| ohos.permission.READ_MEDIA_IMAGES | 读取图片 |
| ohos.permission.READ_MEDIA_VIDEO | 读取视频 |
| ohos.permission.READ_MEDIA_AUDIO | 读取音频 |

---

## 权限声明规范

### module.json5配置

```json
{
  "module": {
    "requestPermissions": [
      {
        "name": "ohos.permission.CAMERA",
        "reason": "$string:camera_reason",
        "usedScene": {
          "abilities": ["EntryAbility"],
          "when": "inuse"
        }
      }
    ]
  }
}
```

**重要**：
- `reason`字段必须使用`$string:xxx`格式引用字符串资源
- reason内容需多语种适配（国际化）
- reason内容上架审核时会展示给用户

---

## 动态申请权限（user_grant）

```typescript
import abilityAccessCtrl from '@ohos.abilityAccessCtrl'
import bundleManager from '@ohos.bundle.bundleManager'
import common from '@ohos.app.ability.common'

async function checkPermission(permission: string): Promise<boolean> {
  let atManager = abilityAccessCtrl.createAtManager()
  let bundleInfo = bundleManager.getBundleInfoForSelfSync(
    bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION
  )
  let grantStatus = atManager.checkGrantAskPermission(
    bundleInfo.appInfo.accessTokenId,
    permission
  )
  return grantStatus === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED
}

async function requestPermission(permissions: string[]): Promise<void> {
  let atManager = abilityAccessCtrl.createAtManager()
  let context = getContext(this) as common.UIAbilityContext
  let result = await atManager.requestPermissionsOnUser(context, permissions)

  for (let i = 0; i < permissions.length; i++) {
    if (result.authResults[i] === abilityAccessCtrl.GrantStatus.PERMISSION_GRANTED) {
      console.info(`Permission ${permissions[i]} granted`)
    }
  }
}
```

---

## 应用安全

### 代码混淆

Release模式编译时自动混淆代码。

### 敏感数据保护

- **AppStorage**：应用级数据存储，进程隔离
- **加解密**：使用 `@ohos.security.cryptoFramework` 进行数据加解密

### 安全编码规范

1. **禁止硬编码密钥**：密钥存储在AGC的加密配置中
2. **网络请求使用HTTPS**：禁止使用HTTP明文传输
3. **输入校验**：对所有外部输入进行校验
4. **日志脱敏**：生产环境日志不输出敏感信息
