# 瀵嗛挜绠＄悊锛圲niversal Keystore Kit锛?
> **閫傜敤鐗堟湰**锛欻armonyOS 6.1 / API 23锛堢ǔ瀹氾級銆傚吋瀹?API 14+銆?
## 姒傝堪

UniversalKeystoreKit锛圚UKS锛夋彁渚涘瘑閽ュ叏鐢熷懡鍛ㄦ湡绠＄悊鑳藉姏锛屽寘鎷瘑閽ョ敓鎴愩€佸鍏?瀵煎嚭銆佺鍚?楠岀銆佸姞瑙ｅ瘑銆佸瘑閽ヨ璇佸拰瀹夊叏瀛樺偍銆傚瘑閽ユ潗鏂欑敱 TEE锛堝彲淇℃墽琛岀幆澧冿級淇濇姢锛屽簲鐢ㄦ棤娉曠洿鎺ヨ幏鍙栨槑鏂囧瘑閽ャ€?
## 瀵嗛挜鐢熸垚

```typescript
import { huks } from '@kit.UniversalKeystoreKit';

let keyAlias = 'my_aes_key';

let properties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_AES_KEY_SIZE_256 },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT |
    huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PKCS7 },
  { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_CBC }
];

let options: huks.HuksOptions = {
  properties: properties,
  inData: new Uint8Array(0)
};

huks.generateKeyItem(keyAlias, options, (err, data) => {
  if (err) {
    console.error('Generate key failed: ' + err.message);
    return;
  }
  console.info('Generate key succeeded.');
});
```

### RSA 瀵嗛挜瀵圭敓鎴?
```typescript
let rsaKeyAlias = 'my_rsa_key';

let rsaProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_RSA },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_RSA_KEY_SIZE_2048 },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN |
    huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY },
  { tag: huks.HuksTag.HUKS_TAG_DIGEST, value: huks.HuksKeyDigest.HUKS_DIGEST_SHA256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PSS }
];

let rsaOptions: huks.HuksOptions = {
  properties: rsaProperties,
  inData: new Uint8Array(0)
};

huks.generateKeyItem(rsaKeyAlias, rsaOptions, (err, data) => {
  if (err) {
    console.error('RSA key generation failed: ' + err.message);
    return;
  }
  console.info('RSA key generation succeeded.');
});
```

## 瀵嗛挜瀵煎叆涓庡鍑?
### 瀵煎叆鍏挜

```typescript
let importKeyAlias = 'imported_rsa_key';

let importProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_RSA },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_RSA_KEY_SIZE_2048 },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY },
  { tag: huks.HuksTag.HUKS_TAG_DIGEST, value: huks.HuksKeyDigest.HUKS_DIGEST_SHA256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PSS }
];

let publicKey = new Uint8Array([0x30, 0x82, 0x01, 0x22]);

let importOptions: huks.HuksOptions = {
  properties: importProperties,
  inData: publicKey
};

huks.importKeyItem(importKeyAlias, importOptions, (err, data) => {
  if (err) {
    console.error('Import key failed: ' + err.message);
    return;
  }
  console.info('Import key succeeded.');
});
```

### 瀵煎嚭鍏挜

```typescript
huks.exportKeyItem(rsaKeyAlias, { properties: [], inData: new Uint8Array(0) }, (err, data) => {
  if (err) {
    console.error('Export key failed: ' + err.message);
    return;
  }
  console.info('Exported public key length: ' + data.outData.length);
});
```

### 瀹夊叏瀵煎叆瀵嗛挜锛堝瘑鏂囧鍏ワ級

```typescript
let secureImportAlias = 'secure_imported_key';

let secureImportProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_AES_KEY_SIZE_256 },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT |
    huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_NONE },
  { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_GCM },
  { tag: huks.HuksTag.HUKS_TAG_UNWRAP_ALGORITHM_SUITE, value: huks.HuksUnwrapSuite.HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING }
];

let secureImportOptions: huks.HuksOptions = {
  properties: secureImportProperties,
  inData: new Uint8Array(0)
};

huks.importWrappedKeyItem(secureImportAlias, 'wrapping_key_alias', secureImportOptions, (err, data) => {
  if (err) {
    console.error('Import wrapped key failed: ' + err.message);
    return;
  }
  console.info('Import wrapped key succeeded.');
});
```

## 绛惧悕涓庨獙绛?
### 绛惧悕

```typescript
let signProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_RSA },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN },
  { tag: huks.HuksTag.HUKS_TAG_DIGEST, value: huks.HuksKeyDigest.HUKS_DIGEST_SHA256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PSS }
];

let signOptions: huks.HuksOptions = {
  properties: signProperties,
  inData: new Uint8Array([0x01, 0x02, 0x03, 0x04])
};

huks.initSession(rsaKeyAlias, signOptions, (err, data) => {
  if (err) {
    console.error('Init sign session failed: ' + err.message);
    return;
  }
  let handle = data.handle;

  huks.finishSession(handle, signOptions, (err, data) => {
    if (err) {
      console.error('Finish sign failed: ' + err.message);
      return;
    }
    console.info('Signature length: ' + data.outData.length);
  });
});
```

### 楠岀

```typescript
let verifyProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_RSA },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY },
  { tag: huks.HuksTag.HUKS_TAG_DIGEST, value: huks.HuksKeyDigest.HUKS_DIGEST_SHA256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PSS }
];

let signatureData = new Uint8Array(256);

let verifyOptions: huks.HuksOptions = {
  properties: verifyProperties,
  inData: new Uint8Array([0x01, 0x02, 0x03, 0x04])
};

huks.initSession(rsaKeyAlias, verifyOptions, (err, data) => {
  if (err) {
    console.error('Init verify session failed: ' + err.message);
    return;
  }
  let handle = data.handle;

  let finishOptions: huks.HuksOptions = {
    properties: verifyProperties,
    inData: signatureData
  };

  huks.finishSession(handle, finishOptions, (err, data) => {
    if (err) {
      console.error('Verify failed: ' + err.message);
      return;
    }
    console.info('Verify succeeded.');
  });
});
```

## 鍔犲瘑涓庤В瀵?
### AES 鍔犲瘑

```typescript
let aesKeyAlias = 'my_aes_key';

let encryptProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_AES_KEY_SIZE_256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PKCS7 },
  { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_CBC },
  { tag: huks.HuksTag.HUKS_TAG_IV, value: new Uint8Array(16) }
];

let plainText = new Uint8Array([0x48, 0x65, 0x6c, 0x6c, 0x6f]);

let encryptOptions: huks.HuksOptions = {
  properties: encryptProperties,
  inData: plainText
};

huks.initSession(aesKeyAlias, encryptOptions, (err, data) => {
  if (err) {
    console.error('Init encrypt session failed: ' + err.message);
    return;
  }
  let handle = data.handle;

  huks.finishSession(handle, encryptOptions, (err, data) => {
    if (err) {
      console.error('Encrypt failed: ' + err.message);
      return;
    }
    console.info('Encrypted data length: ' + data.outData.length);
  });
});
```

### AES 瑙ｅ瘑

```typescript
let decryptProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_AES_KEY_SIZE_256 },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_PKCS7 },
  { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_CBC },
  { tag: huks.HuksTag.HUKS_TAG_IV, value: new Uint8Array(16) }
];

let cipherText = new Uint8Array(32);

let decryptOptions: huks.HuksOptions = {
  properties: decryptProperties,
  inData: cipherText
};

huks.initSession(aesKeyAlias, decryptOptions, (err, data) => {
  if (err) {
    console.error('Init decrypt session failed: ' + err.message);
    return;
  }
  let handle = data.handle;

  huks.finishSession(handle, decryptOptions, (err, data) => {
    if (err) {
      console.error('Decrypt failed: ' + err.message);
      return;
    }
    console.info('Decrypted data length: ' + data.outData.length);
  });
});
```

## 瀵嗛挜璁よ瘉锛圓ttestation锛?
```typescript
let attestKeyAlias = 'attest_key';

let attestProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO, value: new Uint8Array(8) },
  { tag: huks.HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE, value: new Uint8Array(32) },
  { tag: huks.HuksTag.HUKS_TAG_ATTESTATION_ID_VERSION, value: new Uint8Array(4) }
];

let attestOptions: huks.HuksOptions = {
  properties: attestProperties,
  inData: new Uint8Array(0)
};

huks.attestKeyItem(attestKeyAlias, attestOptions, (err, data) => {
  if (err) {
    console.error('Attest key failed: ' + err.message);
    return;
  }
  console.info('Attestation cert chain length: ' + data.certChains.length);
});
```

## 瀵嗛挜鏌ヨ涓庡垹闄?
```typescript
huks.getKeyProperties(keyAlias, { properties: [], inData: new Uint8Array(0) }, (err, data) => {
  if (err) {
    console.error('Key does not exist: ' + err.message);
    return;
  }
  console.info('Key properties: ' + JSON.stringify(data));
});

huks.deleteKeyItem(keyAlias, { properties: [], inData: new Uint8Array(0) }, (err, data) => {
  if (err) {
    console.error('Delete key failed: ' + err.message);
    return;
  }
  console.info('Delete key succeeded.');
});
```

## 瀹夊叏瀛樺偍锛堝瘑閽ヨ闂帶鍒讹級

```typescript
let secureKeyAlias = 'secure_key_with_auth';

let secureProperties: Array<huks.HuksParam> = [
  { tag: huks.HuksTag.HUKS_TAG_ALGORITHM, value: huks.HuksKeyAlg.HUKS_ALG_AES },
  { tag: huks.HuksTag.HUKS_TAG_KEY_SIZE, value: huks.HuksKeySize.HUKS_AES_KEY_SIZE_256 },
  { tag: huks.HuksTag.HUKS_TAG_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT |
    huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT },
  { tag: huks.HuksTag.HUKS_TAG_PADDING, value: huks.HuksKeyPadding.HUKS_PADDING_NONE },
  { tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE, value: huks.HuksCipherMode.HUKS_MODE_GCM },
  { tag: huks.HuksTag.HUKS_TAG_KEY_AUTH_PURPOSE, value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT },
  { tag: huks.HuksTag.HUKS_TAG_USER_AUTH_TYPE, value: huks.HuksUserAuthType.HUKS_USER_AUTH_TYPE_FINGERPRINT },
  { tag: huks.HuksTag.HUKS_TAG_KEY_AUTH_ACCESS_TYPE, value: huks.HuksAuthAccessType.HUKS_AUTH_ACCESS_INVALID_NEW_BIOMETRIC }
];

let secureOptions: huks.HuksOptions = {
  properties: secureProperties,
  inData: new Uint8Array(0)
};

huks.generateKeyItem(secureKeyAlias, secureOptions, (err, data) => {
  if (err) {
    console.error('Generate secure key failed: ' + err.message);
    return;
  }
  console.info('Generate secure key with auth control succeeded.');
});
```

## 鏉冮檺

| 鏉冮檺 | 璇存槑 |
|------|------|
| `ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS` | 璺ㄨ处鎴峰瘑閽ユ搷浣?|

## 群组密钥（API 23 新增）

HUKS 新增群组密钥功能，针对同一开发者开发的多个 HAP 应用提供跨应用密钥共享能力。

适用场景：同一开发者的多个应用需要共享加密数据时，可通过群组密钥实现跨应用密钥访问。

官方指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-group-key-overview

---

## 瀹樻柟鍙傝€?
- HUKS 寮€鍙戞寚瀵硷細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-overview-V5
- 瀵嗛挜鐢熸垚锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-key-generation-V5
- 瀵嗛挜瀵煎叆锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-key-import-V5
- 瀵嗛挜绛惧悕楠岀锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-sign-verify-V5
- 瀵嗛挜鍔犺В瀵嗭細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-encrypt-decrypt-V5
- 瀵嗛挜璁よ瘉锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/huks-key-attestation-V5
- HUKS ArkTS API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-huks-V5