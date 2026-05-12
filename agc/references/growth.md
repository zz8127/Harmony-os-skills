# 增长服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 推送服务（Push Kit）

### 概述

通过 AppGallery Connect 向用户推送通知和透传消息。支持**精准推送**（订阅用户、受众群组、AB 实验等功能）。

### 消息类型

| 类型 | 说明 | 场景 |
|------|------|------|
| 通知消息 | 系统通知栏展示 | 运营推送/系统通知 |
| 透传消息 | 由应用自行处理 | 数据同步/静默更新 |

### 端侧集成

```typescript
import push from '@kit.PushKit';

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

// 订阅通知点击
push.on('notificationClicked', (msg) => {
  console.info('点击了推送通知');
});
```

### 服务端推送

```http
POST https://push-api.cloud.huawei.com/v2/{appId}/messages:send
Authorization: Bearer {access_token}
Content-Type: application/json

{
  "message": {
    "notification": {
      "title": "新消息",
      "body": "您有一条新消息"
    },
    "android": {
      "target_type": 1,
      "target_value": "push_token"
    }
  }
}
```

---

## 远程配置（Remote Configuration）

### 概念

在云端配置参数，应用端实时获取，无需发版即可修改应用行为。

### 端侧代码

```typescript
import remoteConfig from '@kit.CloudFoundation';

// 获取配置
let value = remoteConfig.getValue('feature_flag');
if (value.asBoolean()) {
  // 开启新功能
}

// 拉取最新配置
await remoteConfig.fetchAndApply();
```

### 适用场景

- 功能开关（Feature Flag）
- 运营活动配置
- A/B 测试参数
- 灰度放量比例

---

## A/B 测试

### 概念

将用户分为对照组和实验组，对比不同方案的效果。需分配「管理员」「APP管理员」「运营」或「开发」角色才可启用。

### 实验流程

1. 创建实验 → 2. 设置分组和变量 → 3. 设置目标指标 → 4. 开始实验 → 5. 分析结果

### 与远程配置结合

A/B 测试的分组变量通过远程配置下发，端侧代码无需特殊处理。

---

## App Linking

### 概述

跨平台深度链接服务，用户通过链接可直接到达应用内指定内容，帮助应用提升活跃度。

### 核心能力

| 能力 | 说明 |
|------|------|
| 聚合链接 | 统一的短链接/长链接 |
| 深度链接 | 跳转到应用内指定页面 |
| 延迟深度链接 | 未安装应用时先引导安装再跳转 |
| 网址允许清单 | 正则表达式限制合法跳转地址，防止钓鱼 |
| 社交分享 | 链接分享到社交平台 |

### 使用场景

- 营销活动推广
- 邀请好友
- 内容分享
- 促销优惠券直达

---

## 应用内消息（In-App Messaging）

### 概述

在用户使用应用时，基于用户情景（事件触发）向用户发送有针对性的消息，鼓励用户使用关键功能，也可发送营销内容增强用户粘性。

### 核心能力

| 能力 | 说明 |
|------|------|
| 默认消息样式 | 预置弹窗/卡片/Banner 样式 |
| 自定义样式 | 自定义消息外观 |
| 事件触发 | 基于应用内事件在关键时刻展示消息 |
| 目标用户定向 | 按用户属性/行为定向发送 |

### 消息类型

| 类型 | 说明 |
|------|------|
| 弹窗消息 | 居中弹窗，适合重要提示 |
| Banner 消息 | 顶部/底部横幅 |
| 卡片消息 | 图片+文字+按钮 |
| 图片消息 | 全屏图片展示 |

---

## 素材管理（Material Management）

### 概述

提供素材测试和素材更新能力，帮助开发者优化应用在 AppGallery 上的展示效果。

### 素材测试

- 为一个应用提供多套素材进行 A/B 测试
- 给不同用户呈现不同素材，获取市场反馈
- 通过大数据分析选择更优素材，提升下载转化率和市场曝光度

### 素材更新

- 上传效果更好的新素材
- **无需升级应用版本**即可更新应用信息素材
- 快速迭代应用展示内容

---

## 分析服务（Analytics Kit）

### 概念

采集用户行为数据，支持事件分析、漏斗分析、用户画像等，助力精细化运营（拉新、促活、转化、召回）。

### 端侧代码

```typescript
import analytics from '@kit.AnalyticsKit';

// 上报自定义事件
analytics.onEvent({
  name: 'purchase_complete',
  params: {
    item_id: 'product_001',
    price: 99.9,
    currency: 'CNY'
  }
});

// 设置用户属性
analytics.setUserProfile('vip_level', 'gold');

// 设置当前页面
analytics.setCurrentScreen('home_page', 'HomeActivity');
```

### 预定义事件

| 事件 | 说明 |
|------|------|
| $StartApp | 应用启动 |
| $EndApp | 应用退出 |
| $PageView | 页面浏览 |
| $SignIn | 用户登录 |

---

## 官方参考

- 推送服务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/push-kit
- 远程配置：https://developer.huawei.com/consumer/cn/doc/agc-help/remote-configuration-introduction-0000001059260805
- A/B 测试：https://developer.huawei.com/consumer/cn/doc/agc-help/abtest-introduction-0000001059254973
- App Linking：https://developer.huawei.com/consumer/cn/doc/appgallery-connect-guides/agc-applinking-allowlist-0000001059304615
- 应用内消息：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-appmessage-introduction-0000001071884501
- 素材管理：https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/agc-materialtest-introduction-0000001080765462
- 分析服务：https://developer.huawei.com/consumer/cn/doc/agc-help/analytics-introduction-0000001059254261
