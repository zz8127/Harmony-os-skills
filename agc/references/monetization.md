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

Ads Kit（广告服务）依托华为终端平台与数据能力，提供流量变现服务和开放匿名设备标识服务。帮助开发者解决流量变现难题，同时为广告主提供个性化营销活动或商业广告。

### 流量变现服务

鲸鸿动能流量变现服务是广告服务依托华为终端平台与数据能力提供的 App 流量变现服务，可在 App 中获取并向用户展示高价值广告内容，从中获得广告收益。

### 广告类型

| 类型 | 展示形式 | 适用场景 |
|------|---------|---------|
| 横幅广告 | 图片 | 以通知栏或矩形固定展示在应用内页面顶部/中部/底部，适合用户停留较久或访问频繁的页面 |
| 原生广告 | 图片、视频 | 界面内插入广告，与媒体内容无缝融合 |
| 激励广告 | 视频 | 游戏通关、复活、获取道具、积分、继续机会、人物技能升级时展示 |
| 插屏广告 | 图片、视频 | 游戏或流媒体开启、暂停、过关、跳转、加载、退出时弹出 |
| 开屏广告 | 图片、视频 | 打开 App 时以开屏形式全屏展现，展示时长 3s-5s，展示完毕后自动关闭 |
| 贴片广告 | 图片、视频 | 前贴（播放前）/ 中贴（播放中）/ 后贴（播放结束后） |

### 开放匿名设备标识服务

| 场景 | 使用对象 | 说明 |
|------|---------|------|
| 基于 OAID 的个性化广告 | 广告平台 | 基于 OAID 向用户提供个性化广告，提升转化效果 |
| 基于 OAID 进行变现 | 开发者 | 接入广告平台即可在华为手机上进行个性化广告展示和流量变现 |
| 基于 OAID 的转化归因分析 | 三方监测平台 | 分析广告曝光、点击事件和后向转化交互事件，进行归因分析 |

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

### 支持设备

| 能力 | 支持设备 |
|------|---------|
| 流量变现服务 | Phone、Tablet、PC/2in1 |
| 开放匿名设备标识服务 | Phone、Tablet、PC/2in1、TV |

### 广告合规

- 必须声明 `ohos.permission.ADVERTISEMENT` 权限
- 不得诱导用户点击广告
- 激励广告需明确告知奖励内容
- 儿童应用需使用儿童广告标签
- 流量变现服务仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 与华为联运的游戏应用禁止接入鲸鸿动能平台以外的其他广告平台

---

## Payment Kit（鸿蒙支付服务）

### 概述

Payment Kit 提供方便、安全和快捷的支付方式，助力开发者在商户应用/元服务中快速实现支付功能。支持实体商品或服务的购买，还提供用户身份验证服务、数字人民币支付能力和营销服务。

### 支付场景

| 场景 | 说明 |
|------|------|
| 商城购物 | 用户在商户应用/元服务选购商品后直接完成下单和支付 |
| 免密代扣 | 用户签约后，后续购买时商户可直接发起代扣，减少操作步骤 |
| 数字人民币支付 | 通过拉起数字人民币收银台完成订单支付 |
| 用户身份验证 | 实名信息验证/授权、人脸核身实人验证 |
| 营销服务 | 领券和选券组件，用户可在组件内领取和使用平台券 |

### 商户模型

| 商户模型 | 说明 |
|---------|------|
| 直连商户 | 直接与华为支付对接，使用鸿蒙支付服务的经营主体 |
| 平台类商户 | 为商户交易场景提供支付、结算解决方案，面向线上撮合和管理的平台 |
| 服务商 | 为商户提供开户申请、支付接入、技术开发等综合解决方案机构 |

### 支付能力

| 支付能力 | 支持的商户 | 说明 |
|---------|-----------|------|
| 基础支付 | 直连商户、平台类商户、服务商 | 用户选购商品后完成订单创建与支付 |
| 合单支付 | 平台类商户 | 将不同商户的多个订单合并到同一订单完成支付 |
| 支付并签约 | 直连商户、服务商 | 支付完成后与商户签订协议，完成后续自动扣款 |
| 签约代扣 | 直连商户、服务商 | 商户主动发起签约，完成相关业务自动扣款 |
| 数字人民币支付 | 运营机构或受理服务机构入网的商户 | 通过数字人民币完成支付 |

### 约束与限制

- Payment Kit 仅支持实物商品和服务（酒店服务、出行服务、充值缴费服务）的支付
- 暂不支持虚拟商品（电子虚拟人物形象、游戏中的关卡/货币/道具等）的支付
- 虚拟商品支付请接入 IAP 应用内支付服务
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 支持设备：Phone、Tablet、PC/2in1
- 暂不支持模拟器

---

## Wallet Kit（钱包服务）

### 概述

Wallet Kit 集成了终端"芯-端-云"全栈技术的开放能力，可实现车钥匙、交通卡的凭证电子化。让用户能够轻松地将车钥匙和交通卡保存在手机中，以便在适当的时间使用。

### 核心能力

| 能力 | 说明 |
|------|------|
| 车钥匙 | 将车钥匙模拟到华为钱包，支持钥匙分享、蓝牙车钥匙等新业务场景 |
| 交通卡 | 在手机上开通交通卡，替代实体交通卡，地铁/公交刷卡乘车 |

### 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 仅适用于手机设备
- 暂不支持模拟器

---

## AppGallery Kit（应用市场服务）

### 概述

AppGallery Kit 提供应用市场业务的对外开放能力，支持应用的下载、推荐和分发等场景以提高曝光度，并为开发者提供便捷高效的数字商品服务接入流程和交互体验，助力商业变现。

### 核心能力

| 能力 | 说明 | 支持设备 |
|------|------|---------|
| 数字商品服务 | 数字商品的管理、交易、售后平台能力 | 详见 IAP 文档 |
| 应用市场推荐 | 直达应用市场详情页或卡片加桌页面，提高应用曝光率 | Phone、PC/2in1、Tablet、TV |
| 产品特性按需分发 | 应用多子业务独立演进，动态分发和资源拆分 | Phone、PC/2in1、Tablet、TV |
| 生态查询服务 | 查询元服务/应用被打开的场景，基于场景值做业务拓展 | Phone、PC/2in1、Tablet、TV |
| 应用市场更新功能 | 查询应用是否有可更新版本，应用内显示更新提醒 | Phone、PC/2in1、Tablet、Wearable、TV |
| 应用归因服务 | 判断用户下载和使用应用的原因，借助归因数据分析营销效果 | Phone、PC/2in1、Tablet、TV |
| 隐私管理服务 | 统一隐私弹框，查询隐私链接、签署状态、撤销签署记录 | Phone、PC/2in1、Tablet、TV |
| 图标管理服务 | 管理动态图标，查询/切换/恢复图标 | Phone、PC/2in1、Tablet、Wearable、TV |
| 应用评论服务 | 对应用进行评论，在应用内拉起应用评分弹窗 | Phone、PC/2in1、Tablet |

### 约束与限制

- 大部分能力仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 模拟器不支持数字商品服务、应用市场推荐、生态查询服务、更新功能、评论服务、图标管理服务及端云交互

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
- Ads Kit 简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-introduction
- Payment Kit 简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/payment-introduction
- Wallet Kit 简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/wallet-introduction
- AppGallery Kit 简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/store-introduction
- 广告服务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ads-kit
- 付费下载：https://developer.huawei.com/consumer/cn/doc/app/agc-help-paidapp-0000001140063597
