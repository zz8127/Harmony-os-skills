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

## AppGallery Connect API

### 概述

AppGallery Connect API 是一套 RESTful API，通过这些 API 可以无需登录 AppGallery Connect 即可定制服务或实现流程自动化，提升工作效率。

### 前置条件

在发起 API 调用前，需先获得 AppGallery Connect 服务端的授权。

### API 类别

| API 类别 | 功能说明 |
|---------|---------|
| Testing API | 对 HarmonyOS 应用/元服务进行版本测试，邀请测试用户体验并收集意见 |
| Upload Management API | 完成应用文件上传（APP 软件包、图标、介绍图片、视频文件等） |
| Publishing API | 完成应用/元服务的发布管理（版权版号、基本信息、版本信息、提交发布/撤销审核等） |
| Provisioning API | 管理证书、Profile 和调试设备 |
| Domain Management API | 管理元服务所需的业务域名和服务器域名配置 |
| Reports API | 查询 AGC 中部分分析数据（下载安装、安装失败等报表数据） |

### 官方链接

- AppGallery Connect API 业务介绍：https://developer.huawei.com/consumer/cn/doc/app/agc-help-connect-api-introduction-0000002270974725
- 获取服务端授权：https://developer.huawei.com/consumer/cn/doc/app/agc-help-connect-api-obtain-server-auth-0000002271134661

---

## 预加载（Prefetch）

### 概述

预加载是 Cloud Foundation Kit 提供的一种可提前加载所需资源的服务。通过预加载，可以将页面所需的文本、图片、音频、视频等资源数据提前加载到本地进行缓存，以提升应用页面加载速度。

预加载仅以字符串数据形式进行缓存，应用使用时不需要修改原有数据格式，获取缓存后可直接进行解析，并且可以对隐私、敏感数据进行加密。

### 预加载类型

| 类型 | 说明 | 适用场景 |
|------|------|---------|
| 安装预加载 | 应用安装时下载云侧应用数据进行缓存，应用打开时直接获取本地首开页面缓存数据 | 应用首次打开首页加载提速 |
| 周期性预加载 | 系统每隔 12 小时拉取一次指定页面的云侧数据并缓存到本地 | 任意页面加载提速，节日主题资源、H5 离线包等场景 |
| 跳链安装预加载 | 结合 App Linking Kit 的延迟链接功能，提前将用户点击的详情页数据缓存到本地 | 被分享用户安装应用后首次打开详情页加载提速 |

> 跳链安装预加载仅支持在 HarmonyOS 应用中调用。

### H5 预加载组件 FastWeb

基于 OpenHarmony 基础组件开发的高性能 Web 容器，具有预启动、预渲染、预编译 JavaScript 生成字节码缓存、离线资源免拦截注入等能力，可为应用中 Web 页面加载提速。FastWeb 无需使用 Cloud Foundation Kit 能力。

### 工作原理

1. 预加载服务根据配置的数据预加载策略从应用后台获取数据
2. 预加载服务将获取的数据在本地进行缓存
3. 应用使用获取的缓存数据进行页面渲染

### 典型应用场景

| 场景 | 说明 |
|------|------|
| 提升应用首开速度 | 将必要资源提前加载到本地缓存，用户首次访问时直接从缓存获取，减少白屏时间 |
| 实现节日主题即发即现 | 通过周期性数据拉取提前将主题资源获取到本地，活动开始时直接从本地获取展示 |

### 约束与限制

**设备限制**：支持 Phone、Tablet；从 API 23 开始新增支持 PC/2in1

**数据限制**：仅支持缓存文本、图片、音频、视频等静态资源数据，不支持代码、脚本等动态资源数据

**配额限制**

| 配额类型 | 配额 |
|---------|------|
| 安装预加载缓存大小 | 2MB |
| 周期性预加载缓存大小 | 3MB |
| 跳链安装预加载缓存大小 | 3MB |

### 开发流程

1. 配置预加载策略
2. 开发预加载资源接口
3. 调用预加载
4. （可选）使用命令行工具调试周期性预加载

### 官方链接

- 预加载概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-overview
- 开发流程：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-devprocess
- 配置预加载：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-config
- 开发预加载资源接口：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-cloud-interdev
- 调用预加载：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-call

---

## 官方参考

- 云函数：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudfunction-introduction-0000001059221573
- 云数据库：https://developer.huawei.com/consumer/cn/doc/agc-help/clouddb-introduction-0000001059253201
- 云存储：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudstorage-introduction-0000001059255085
- 云托管：https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/agc-cloudhosting-introductions-0000001057944575
- AppGallery Connect API：https://developer.huawei.com/consumer/cn/doc/app/agc-help-connect-api-introduction-0000002270974725
- 预加载服务：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-prefetch-service
