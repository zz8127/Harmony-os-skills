# 电话服务（Telephony Kit）

> HarmonyOS 6.1 / API 23

## 概述

电话服务（Telephony Kit）提供通话管理、SIM 卡信息、网络状态和联系人等能力，通过 `@kit.TelephonyKit` 引入。API 23 新增 VCard 联系人导入导出功能。

## call 模块

拨打电话和查询通话状态。

```typescript
import { call } from '@kit.TelephonyKit';
import { BusinessError } from '@kit.BasicServicesKit';

async function makeCall(phoneNumber: string): Promise<void> {
  try {
    await call.makeCall(phoneNumber);
  } catch (error) {
    const e = error as BusinessError;
    console.error(`拨号失败: ${e.code} - ${e.message}`);
  }
}

async function checkHasCall(): Promise<boolean> {
  return call.hasCall();
}

async function getCallState(): Promise<call.CallState> {
  return call.getCallState();
}
```

监听通话状态变化：

```typescript
import { call } from '@kit.TelephonyKit';

function onCallStateChange(): void {
  call.on('callStateChange', { slotId: 0 }, (data: call.CallStateChangeResult) => {
    console.info(`通话状态: ${data.state}`);
    console.info(`来电号码: ${data.accountNumber}`);
  });
}

function offCallStateChange(): void {
  call.off('callStateChange');
}
```

## VCard 模块（API 23）

API 23 新增 VCard 联系人导入导出能力。

```typescript
import { vCard } from '@kit.TelephonyKit';

async function exportContacts(): Promise<string> {
  const vCardData = await vCard.exportToFile('/data/storage/el2/base/files/contacts.vcf');
  return vCardData;
}

async function importContacts(filePath: string): Promise<number> {
  const importedCount = await vCard.importFromFile(filePath);
  console.info(`导入联系人数量: ${importedCount}`);
  return importedCount;
}
```

VCard 数据构造：

```typescript
import { vCard } from '@kit.TelephonyKit';

async function createVCardEntry(): Promise<void> {
  const entry: vCard.VCardEntry = {
    name: { familyName: '张', givenName: '三' },
    phoneNumbers: [{ number: '13800138000', type: vCard.PhoneType.CELL }],
    emails: [{ address: 'zhangsan@example.com', type: vCard.EmailType.HOME }],
    organization: '华为'
  };
  await vCard.addEntry(entry);
}
```

## sim 模块

获取 SIM 卡信息。

```typescript
import { sim } from '@kit.TelephonyKit';

async function getSimInfo(): Promise<void> {
  const isActive = await sim.isSimActive(0);
  console.info(`SIM 卡激活: ${isActive}`);

  const operator = await sim.getOperatorName(0);
  console.info(`运营商: ${operator}`);

  const countryCode = await sim.getIsoCountryCodeForSim(0);
  console.info(`国家代码: ${countryCode}`);
}

async function getSimState(): Promise<sim.SimState> {
  return sim.getSimState(0);
}
```

## radio 模块

获取网络注册状态和信号强度。

```typescript
import { radio } from '@kit.TelephonyKit';

async function getNetworkState(): Promise<void> {
  const state = await radio.getNetworkState(0);
  console.info(`注册状态: ${state.regState}`);
  console.info(`网络类型: ${state.cfgTech}`);
  console.info(`运营商: ${state.longOperatorName}`);
}

async function getSignalInformation(): Promise<void> {
  const signals = await radio.getSignalInformation(0);
  for (const signal of signals) {
    console.info(`信号类型: ${signal.signalType}, 等级: ${signal.signalLevel}`);
  }
}
```

监听网络状态变化：

```typescript
import { radio } from '@kit.TelephonyKit';

function onNetworkStateChange(): void {
  radio.on('networkStateChange', { slotId: 0 }, (data: radio.NetworkState) => {
    console.info(`网络状态变化: ${data.regState}`);
  });
}
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.MAKE_CALL` | 拨打电话权限 |
| `ohos.permission.READ_CONTACTS` | 读取联系人权限 |
| `ohos.permission.WRITE_CONTACTS` | 写入联系人权限 |
| `ohos.permission.GET_TELEPHONY_STATE` | 获取电话状态权限 |

在 `module.json5` 中声明：

```json
{
  "requestPermissions": [
    { "name": "ohos.permission.MAKE_CALL" },
    { "name": "ohos.permission.READ_CONTACTS" },
    { "name": "ohos.permission.WRITE_CONTACTS" },
    { "name": "ohos.permission.GET_TELEPHONY_STATE" }
  ]
}
```

## 官方参考

- [Telephony Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/telephony-kit-overview-0000001774121546)
- [Telephony Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/call-0000001774121542)
