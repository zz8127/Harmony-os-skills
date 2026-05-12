---
name: harmonyos-agc
description: |
  AppGallery Connect (AGC) 应用分发与云服务开发指南。
  触发场景：应用上架/分发/审核、AGC 云开发（云函数/云数据库/云存储/云托管）、
  认证服务、增长（推送/远程配置/A-B测试/App Linking/应用内消息/素材管理）、
  质量（崩溃/性能/云测试/云调试）、变现（IAP/广告/付费下载）等。
  基于：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-introduction-0000001057492641
---

# AppGallery Connect (AGC) 开发指南

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。
> **更新时间**：2026-04-24
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-overview-0000001100246618

---

## 快速导航

- [应用分发](references/distribution.md) — 创建应用/版本管理/发布/审核/灰度发布/沙盒测试
- [云开发](references/cloud-development.md) — 云函数/云数据库/云存储/云托管/云缓存/API网关
- [认证服务](references/auth.md) — 匿名/邮箱/手机/第三方登录/华为账号
- [增长服务](references/growth.md) — 推送/远程配置/A-B测试/App Linking/应用内消息/素材管理/分析
- [质量服务](references/quality.md) — 崩溃/性能/云测试/云调试/接入检测
- [变现服务](references/monetization.md) — 应用内支付/广告/付费下载
- [游戏服务](references/game-service.md) — 成就/排行榜/云存档/防沉迷/游戏事件

---

## AGC 服务全景

根据 [AGC 简介](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-introduction-0000001057492641)，AGC 为应用的**创意、开发、分发、运营、经营**各环节提供一站式服务。

| 分类 | 服务 | 说明 |
|------|------|------|
| **分发** | 应用分发 | 应用上架/版本管理/审核/灰度发布，覆盖 200+ 国家与地区，支持 78 种语言 |
| **测试** | 沙盒测试 | 上线前模拟真实用户环境（IAP/游戏等） |
| | 云测试 | 兼容性/稳定性/功耗/安全自动化测试 |
| | 云调试 | 远程真机调试，ADB 远程代码调试 |
| | 开放式测试 | 邀请用户参与测试 |
| | 接入检测 | 审核前自检，提前发现影响审核的问题 |
| **云开发** | 云函数 | Serverless 事件驱动函数计算 |
| | 云数据库 | 端云协同 NoSQL 数据库（含 for Object） |
| | 云存储 | 文件上传/下载/CDN 分发 |
| | 云托管 | 网站/静态内容托管，一键部署 |
| | 云缓存 | Redis 兼容缓存服务 |
| | API 网关 | API 统一管理/鉴权/限流 |
| **认证** | 认证服务 | 多种登录方式统一管理 |
| **增长** | 推送服务 | Push Kit 消息推送（含精准推送） |
| | 远程配置 | 无需发版即可修改应用行为 |
| | A/B 测试 | 对比不同方案效果 |
| | App Linking | 跨平台深度链接，直达应用内内容 |
| | 应用内消息 | 基于用户情景的定向消息 |
| | 素材管理 | 素材 A/B 测试与无需发版的素材更新 |
| | 分析服务 | 用户行为/事件/漏斗分析 |
| **质量** | 崩溃服务 | 崩溃采集/分析/告警 |
| | 性能服务 | ANR/慢操作/网络性能/可视化实时报告 |
| | 云监控 | 应用运行状态实时监控 |
| **变现** | 应用内支付 | IAP 消耗型/非消耗型/订阅 |
| | 广告服务 | Ads Kit 广告变现 |
| | 付费下载 | 应用付费下载 |
| | 联运服务 | 华为渠道联运 |

---

## 快速接入

### 1. 创建项目与应用

1. 登录 [AGC 控制台](https://developer.huawei.com/consumer/cn/service/jsp/agc/index.html)
2. 创建项目 → 添加应用 → 下载 `agconnect-services.json`
3. 将配置文件放入工程 `entry/src/main/resources/rawfile/`

### 2. 集成 AGC SDK

```typescript
// oh-package.json5
"dependencies": {
  "@hw-agconnect/api": "x.x.x",
  "@hw-agconnect/core": "x.x.x"
}

// 初始化
import { AGConnect } from '@hw-agconnect/core';
AGConnect.initialize(getContext(this));
```

### 3. 开通服务

在 AGC 控制台 → 我的项目 → 选择应用 → 点击对应服务的「开通」按钮。

### 4. 服务计费

AGC 服务分为**免费服务**和**收费服务**：
- 免费服务：无需开通结算账户即可使用
- 收费服务：需开通结算账户并签署付费服务协议，通常提供一定免费配额，超额部分按量付费
- 在「项目设置 → 项目套餐」中查看和管理服务订购与配额

---

## 与 HarmonyOS 开发的关系

| 场景 | 对应 Skill |
|------|-----------|
| 应用打包签名 | `dev/references/publish.md` |
| Push Kit 代码集成 | `samples/references/app-service.md` |
| IAP 代码集成 | `samples/references/app-service.md` |
| 设计规范 | `design/SKILL.md` |

---

## API 24 Beta1 变更追踪（2026-04-30）

> HarmonyOS 6.1.1(24) Beta1 已发布，AGC 服务暂无重大变更。持续关注官方更新。

---

## 官方参考

- **AGC 简介**：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-introduction-0000001057492641
- **AGC 帮助中心**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-overview-0000001100246618
- **应用分发文档**：https://developer.huawei.com/consumer/cn/doc/app/agc-help-app-0000002235710234
- **云开发文档**：https://developer.huawei.com/consumer/cn/doc/agc-help/cloudfunction-introduction-0000001059221573
- **服务计费**：https://developer.huawei.com/consumer/cn/doc/development/AppGallery-connect-Guides/agc-service-billing-0000001058092595
- **API 参考**：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/agc-api-overview
