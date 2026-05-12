# 应用服务示例（App Service）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## Push Kit（推送服务）

```typescript
import push from '@hms.push';

/// 初始化
push.init(getContext(this));

// 获取 Push Token
push.getToken((err, token) => {
  if (!err) {
    console.info('Push Token：' + token);
    // 将 token 发送给应用服务器
  }
});

// 订阅推送消息
push.on('pushMsg', (msg) => {
  console.info('收到推送：' + JSON.stringify(msg));
});

// 订阅点击消息
push.on('notificationClicked', (msg) => {
  console.info('点击了推送通知');
});
```

---

## 应用内支付（IAP）

```typescript
import iap from '@kit.IAP';

// 创建支付客户端
let iapClient = iap.createIapClient();

// 获取商品信息
let products = await iapClient.getProductInfo({
  productIds: ['product_001', 'product_002']
});

// 创建订单
let order = await iapClient.createOrder({
  productId: 'product_001',
  bizType: 0 // consumable（消耗型）
});

// 发起支付
let payResult = await iapClient.startIapActivity(order);
```

---

## AppGallery Connect（AGC）

### 云函数

```typescript
import cloud from '@kit.CloudFoundation';

// 初始化云开发
cloud.initialize({
  eventCb: (event) => {
    console.info('云函数事件：' + event.type);
  }
});

// 调用云函数
let result = await cloud.call({
  name: 'myFunction',
  params: { key: 'value' }
});
console.info('云函数返回：' + JSON.stringify(result));
```

---

## 统一扫码服务

### 基础扫码（Scan Kit）

> ⚠️ **API 签名待核实**：以下 `openScanActivity` / `analyzeBarcode` API 名称请以官方文档为准。

```typescript
import scan from '@kit.ScanKit';

// 启动扫码
let scanResult = await scan.openScanActivity();
console.info('扫码结果：' + scanResult.result);

// 解析条码
let barcode = scan.analyzeBarcode(imageSource);
console.info('条码内容：' + barcode);
```

---

## AGC 云数据库

> ⚠️ **API 名称待核实**：`objectPool` 可能不是正确的模块名，请以官方文档为准。

```typescript
import objectPool from '@kit.CloudFoundation';

// 插入记录
let record = {
  name: 'test',
  value: 123
};
await objectPool.insert('myCollection', record);

// 查询
let results = await objectPool.query('myCollection', {
  where: { name: 'test' }
});
```

---

## 官方参考

- Push Kit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit
- 应用内支付：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/iap-kit
- 云函数：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudfunction-introduction-0000001200786205
- 统一扫码：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-kit
