# 加密框架（Crypto Architecture Kit）

> HarmonyOS 6.1 / API 23

## 概述

加密框架（Crypto Architecture Kit）提供对称加密、非对称加密、哈希、HMAC、密钥协商等密码学能力，通过 `@kit.CryptoArchitectureKit` 引入。API 23 新增从私钥获取公钥接口。

## 对称加密（AES/CBC/PKCS7）

使用 AES-CBC 模式进行对称加解密。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function aesEncrypt(plainText: string, key: cryptoFramework.SymKey, iv: Uint8Array): Promise<cryptoFramework.DataBlob> {
  const cipher = cryptoFramework.createCipher('AES128|CBC|PKCS7');
  const ivParamsSpec = cryptoFramework.createIvParamsSpec(iv);
  await cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, key, ivParamsSpec);
  const input: cryptoFramework.DataBlob = { data: new Uint8Array(Buffer.from(plainText, 'utf-8')) };
  return cipher.doFinal(input);
}

async function aesDecrypt(cipherData: cryptoFramework.DataBlob, key: cryptoFramework.SymKey, iv: Uint8Array): Promise<string> {
  const cipher = cryptoFramework.createCipher('AES128|CBC|PKCS7');
  const ivParamsSpec = cryptoFramework.createIvParamsSpec(iv);
  await cipher.init(cryptoFramework.CryptoMode.DECRYPT_MODE, key, ivParamsSpec);
  const result = await cipher.doFinal(cipherData);
  return Buffer.from(result.data).toString('utf-8');
}

async function generateAesKey(): Promise<cryptoFramework.SymKey> {
  const generator = cryptoFramework.createSymKeyGenerator('AES128');
  return generator.generateSymKey();
}
```

## 非对称加密（RSA）

使用 RSA 进行非对称加解密。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function generateRsaKeyPair(): Promise<cryptoFramework.KeyPair> {
  const generator = cryptoFramework.createAsyKeyGenerator('RSA1024|PRIMES_2');
  return generator.generateKeyPair();
}

async function rsaEncrypt(plainText: string, publicKey: cryptoFramework.PubKey): Promise<cryptoFramework.DataBlob> {
  const cipher = cryptoFramework.createCipher('RSA1024|PKCS1');
  await cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, publicKey, null);
  const input: cryptoFramework.DataBlob = { data: new Uint8Array(Buffer.from(plainText, 'utf-8')) };
  return cipher.doFinal(input);
}

async function rsaDecrypt(cipherData: cryptoFramework.DataBlob, privateKey: cryptoFramework.PriKey): Promise<string> {
  const cipher = cryptoFramework.createCipher('RSA1024|PKCS1');
  await cipher.init(cryptoFramework.CryptoMode.DECRYPT_MODE, privateKey, null);
  const result = await cipher.doFinal(cipherData);
  return Buffer.from(result.data).toString('utf-8');
}
```

RSA 签名与验签：

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function rsaSign(data: Uint8Array, privateKey: cryptoFramework.PriKey): Promise<cryptoFramework.DataBlob> {
  const signer = cryptoFramework.createSign('RSA1024|PKCS1|SHA256');
  await signer.init(privateKey);
  const input: cryptoFramework.DataBlob = { data };
  return signer.sign(input);
}

async function rsaVerify(data: Uint8Array, signature: cryptoFramework.DataBlob, publicKey: cryptoFramework.PubKey): Promise<boolean> {
  const verifier = cryptoFramework.createVerify('RSA1024|PKCS1|SHA256');
  await verifier.init(publicKey);
  const input: cryptoFramework.DataBlob = { data };
  return verifier.verify(input, signature);
}
```

## 哈希（SHA-256 / MD5）

计算消息摘要。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function sha256Digest(data: Uint8Array): Promise<Uint8Array> {
  const md = cryptoFramework.createMd('SHA256');
  await md.update({ data });
  const result = await md.digest();
  return result.data;
}

async function md5Digest(data: Uint8Array): Promise<Uint8Array> {
  const md = cryptoFramework.createMd('MD5');
  await md.update({ data });
  const result = await md.digest();
  return result.data;
}

function bytesToHex(bytes: Uint8Array): string {
  return Array.from(bytes).map(b => b.toString(16).padStart(2, '0')).join('');
}
```

## HMAC

基于哈希的消息认证码。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function computeHmac(key: cryptoFramework.SymKey, data: Uint8Array): Promise<Uint8Array> {
  const mac = cryptoFramework.createMac('SHA256');
  await mac.init(key);
  await mac.update({ data });
  const result = await mac.doFinal();
  return result.data;
}

async function generateHmacKey(): Promise<cryptoFramework.SymKey> {
  const generator = cryptoFramework.createSymKeyGenerator('HMAC|SHA256');
  return generator.generateSymKey();
}
```

## 密钥协商（ECDH）

使用 ECDH 进行密钥协商。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function ecdhKeyAgreement(): Promise<cryptoFramework.DataBlob> {
  const generator = cryptoFramework.createAsyKeyGenerator('ECC256');
  const keyPairA = await generator.generateKeyPair();
  const keyPairB = await generator.generateKeyPair();

  const keyAgreement = cryptoFramework.createKeyAgreement('ECC256');
  const sharedSecret = await keyAgreement.generateSecret(keyPairA.priKey, keyPairB.pubKey);
  return sharedSecret;
}
```

## 从私钥获取公钥（API 23）

API 23 新增从私钥直接获取对应公钥的接口。

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function getPubKeyFromPriKey(privateKey: cryptoFramework.PriKey): Promise<cryptoFramework.PubKey> {
  return cryptoFramework.getPubKey(privateKey);
}
```

完整密钥恢复流程：

```typescript
import { cryptoFramework } from '@kit.CryptoArchitectureKit';

async function keyRecoveryFlow(): Promise<void> {
  const generator = cryptoFramework.createAsyKeyGenerator('RSA2048|PRIMES_2');
  const keyPair = await generator.generateKeyPair();

  const priKeyData = keyPair.priKey.getEncoded();
  const restoredPriKey = await generator.convertKey({
    data: priKeyData.data
  }, null);

  const recoveredPubKey = await cryptoFramework.getPubKey(restoredPriKey.priKey);
  console.info(`公钥算法: ${recoveredPubKey.algName}`);
}
```

## 权限

| 权限 | 说明 |
|------|------|
| 无特殊权限 | 加密框架无需额外权限 |

## 官方参考

- [Crypto Architecture Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/crypto-architecture-kit-overview-0000001774121542)
- [Crypto Architecture Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cryptoframework-0000001774121538)
