# 变现服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 应用内支付（IAP）

### 概述

通过华为支付系统实现应用内商品购买，支持消耗型/非消耗型/订阅型商品。

### 商品类型

| 类型 | 说明 | 典型场景 |
|------|------|---------|
| 消耗型 | 购买后消耗，可重复购买 | 虚拟币/游戏道具 |
| 非消耗型 | 一次购买永久拥有 | 去广告/解锁功能 |
| 订阅型 | 周期性扣费 | 会员/订阅内容 |

### 端侧代码

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
  bizType: 0  // 0=消耗型
});

// 发起支付
let payResult = await iapClient.startIapActivity(order);

// 消耗购买（消耗型商品需确认消耗）
await iapClient.consumePurchase({
  purchaseToken: payResult.purchaseToken
});
```

### 订阅管理

| 操作 | 说明 |
|------|------|
| 订阅 | 用户选择订阅计划并付款 |
| 续订 | 到期自动续订 |
| 取消订阅 | 用户主动取消，到期后不再续费 |
| 宽限期 | 支付失败后的重试期 |
| 账号保留 | 支付失败后暂停服务但保留数据 |

### 服务端验证

支付成功后，应在服务端通过 Purchase Token 验证购买有效性，防止伪造。

```
GET https://subscr-drcn.iap.cloud.huawei.com/v2/orders/{purchaseToken}
Authorization: Bearer {access_token}
```

---

## 广告服务（Ads Kit）

### 概述

集成华为广告 SDK 实现应用内广告变现。

### 广告类型

| 类型 | 说明 | 适用场景 |
|------|------|---------|
| Banner 广告 | 页面顶部/底部横幅 | 资讯类应用 |
| 插屏广告 | 全屏弹窗 | 页面切换时 |
| 激励广告 | 看广告获奖励 | 获取虚拟币/道具 |
| 原生广告 | 自定义样式 | 信息流融入 |
| 开屏广告 | 应用启动全屏 | 冷启动时 |

### 端侧代码

```typescript
import ads from '@kit.AdsKit';

// 创建激励广告
let interstitialAd = ads.createInterstitialAd({
  adUnitId: 'testb4zuon2pey'  // 测试广告位
});

// 监听广告事件
interstitialAd.onLoad(() => { console.info('广告加载完成'); });
interstitialAd.onError((err) => { console.error('广告错误：' + err); });
interstitialAd.onClose(() => { console.info('广告关闭'); });

// 加载并展示广告
await interstitialAd.load();
interstitialAd.show();
```

### 广告合规

- 必须声明 `ohos.permission.ADVERTISEMENT` 权限
- 不得诱导用户点击广告
- 激励广告需明确告知奖励内容
- 儿童应用需使用儿童广告标签

---

## 付费下载

### 概述

应用在 AppGallery 以付费方式提供下载，用户购买后方可安装使用。

### 适用场景

- 付费工具类应用
- 付费内容类应用
- 专业软件

---

## 联运服务

### 概述

与华为渠道联运，通过华为的流量和运营能力帮助应用获取用户和收入。

---

## 官方参考

- 应用内支付：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/iap-kit
- 广告服务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-kit
- 付费下载：https://developer.huawei.com/consumer/cn/doc/app/agc-help-paidapp-0000001140063597
