# NFC

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

NFC（Near Field Communication）工作在 13.56MHz 频段，传输距离 10cm 以内。HarmonyOS 支持 NFC 读卡、写卡、NDEF 格式处理。

## NFC 标签类型

| 类型 | 说明 |
|------|------|
| NFC-Forum Type 1/2/3/4 | 常见 NFC 标签 |
| NDEF | NFC Data Exchange Format（标准数据格式） |
| NFC-V | 支持 ISO15693 协议 |

## NDEF 读写

```typescript
import { nfcManager from '@kit.ConnectivityKit';

// 检查 NFC 是否可用
let isNfcAvailable = nfcManager.isNfcAvailable();
let isNfcEnabled = nfcManager.isNfcEnabled();

// 读取 NDEF 标签
async function readNdef() {
  let tagInfo = await nfcManager.getNfcTagInfo();
  if (tagInfo && tagInfo.ndefMsg) {
    tagInfo.ndefMsg.forEach(msg => {
      console.info('NDEF: ' + JSON.stringify(msg));
    });
  }
}

// 写入 NDEF 记录
async function writeNdef() {
  let ndefMsg: nfcManager.NdefMessage = {
    records: [
      {
        tnf: nfcManager.NfcTagTnf.NFC_TNF_WELL_KNOWN,
        type: [0x54],  // 'T' for Text
        payload: [0x02, 0x65, 0x6E, 0x48, 0x65, 0x6C, 0x6C, 0x6F]  // "enHello"
      }
    ]
  };
  await nfcManager.writeNdefMessage(ndefMsg);
}
```

## NFC 权限

```json
"requestPermissions": [
  { "name": "ohos.permission.NFC_TAG" },
  { "name": "ohos.permission.NFC_CARD_EMULATION" }
]
```

---

## API 23 新增（HarmonyOS 6.1.0）

### NFC Tag 读卡事件订阅增强

新增 `tagon23` 接口，支持带有卡在位状态周期性检测的 NFC Tag 读卡事件订阅能力。

```typescript
import { tag } from '@kit.ConnectivityKit'

// API 23+: 带卡在位检测的Tag读卡事件订阅
tag.on('tagOn', {
  periodicDetection: true
})
```

---

## 官方参考

- NFC 开发概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nfc-overview-V5
