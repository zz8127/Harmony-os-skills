# 云开发（Serverless）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 概述

AGC 云开发提供 Serverless 后端服务，帮助开发者统一构建和管理后端服务和云资源，提供包含计算、弹性伸缩、存储等 Serverless 能力，降本增效，安全可靠。

---

## 云函数（Cloud Functions）

### 概念

无服务器函数计算，事件触发执行，按调用次数计费。

### 支持运行时

| 运行时 | 版本 |
|--------|------|
| Node.js | 14.x / 16.x / 18.x |
| Python | 3.9 |
| Java | 11 |

### 端侧调用

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

### 触发方式

| 触发类型 | 说明 |
|---------|------|
| HTTP 触发 | 通过 URL 直接调用 |
| 云数据库触发 | 数据变更时自动执行 |
| 云存储触发 | 文件上传/删除时执行 |
| 定时触发 | Cron 表达式定时执行 |
| 审核触发 | 审核结果回调 |

### 限制

| 项目 | 限制 |
|------|------|
| 函数执行超时 | 60s（可申请 300s） |
| 函数内存 | 128MB-1024MB |
| 代码包大小 | ≤ 50MB |
| 并发实例 | 默认 1000 |

---

## 云数据库（Cloud DB）

### 概念

端云协同 NoSQL 数据库，支持离线操作和自动同步。提供 **Cloud DB** 和 **Cloud DB for Object** 两种模式。

### 数据模型

- **对象类型**：类似表结构，定义字段名和类型
- **权限控制**：按角色/条件配置读写权限
- **数据同步**：端侧修改自动同步到云侧

### 端侧操作

```typescript
import cloudDB from '@kit.CloudFoundation';

// 查询
let query = cloudDB.query('UserType')
  .equalTo('age', 18)
  .limit(20);
let results = await cloudDB.execute(query);

// 插入
let user = { name: 'test', age: 25 };
await cloudDB.insert('UserType', user);

// 更新
await cloudDB.update('UserType', { age: 26 }, { name: 'test' });

// 删除
await cloudDB.delete('UserType', { name: 'test' });
```

### 权限配置

| 角色 | 说明 |
|------|------|
| 所有用户 | 未登录用户 |
| 已认证用户 | 已登录用户 |
| 数据创建者 | 创建该数据的用户 |
| 指定用户 | 特定用户 ID |

---

## 云存储（Cloud Storage）

### 概念

可扩展、免维护的云端存储服务，支持图片/视频/文档上传下载，集成 CDN 加速，支持断点续传。

### 核心能力

| 能力 | 说明 |
|------|------|
| 文件上传/下载 | SDK 支持安全可靠的文件传输 |
| 断点续传 | 因网络或用户原因中止后可恢复 |
| 文件元数据管理 | 查询和设置文件元数据 |
| 跨域访问 | 控制台或 SDK 配置跨域规则 |
| 可伸缩 | EB 级数据存储，解决海量存储难题 |

### 端侧操作

```typescript
import cloudStorage from '@kit.CloudFoundation';

// 上传文件
let uploadResult = await cloudStorage.upload({
  localPath: '/data/avatar.jpg',
  cloudPath: 'images/avatar.jpg'
});

// 下载文件
await cloudStorage.download({
  cloudPath: 'images/avatar.jpg',
  localPath: '/data/avatar.jpg'
});

// 获取下载链接
let url = await cloudStorage.getDownloadUrl('images/avatar.jpg');
```

### 安全规则

```json
{
  "rules": {
    "images": {
      ".read": "auth != null",
      ".write": "auth != null && auth.uid == $uid"
    }
  }
}
```

---

## 云托管（Cloud Hosting）

### 概念

提供内容托管服务，包括网站托管和存储加速功能，无需关注域名申请、证书管理等安全配置，一键部署，安全快速。

### 核心能力

| 能力 | 说明 |
|------|------|
| 静态网站托管 | HTML/CSS/JS 等静态内容 |
| 动态网站托管 | 支持服务端渲染 |
| 存储加速 | CDN 加速分发 |
| 一键部署 | 快速上线网站 |

### 适用场景

- 应用官网/落地页
- 管理后台
- 营销活动页面
- H5 轻应用

---

## 云缓存（Cloud Cache）

### 概念

提供 Redis 兼容的缓存服务，用于加速数据访问，降低数据库压力。

---

## API 网关

### 概念

API 统一管理、鉴权、限流，为云函数和后端服务提供统一的 API 入口。

### 核心能力

| 能力 | 说明 |
|------|------|
| API 管理 | 创建/发布/版本管理 |
| 鉴权 | Token/API Key 认证 |
| 限流 | 防止 API 滥用 |
| 监控 | 调用量/延迟/错误率 |

---

## 官方参考

- 云函数：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudfunction-introduction-0000001059221573
- 云数据库：https://developer.huawei.com/consumer/cn/doc/agc-help/clouddb-introduction-0000001059253201
- 云存储：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudstorage-introduction-0000001059255085
- 云托管：https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/agc-cloudhosting-introductions-0000001057944575
