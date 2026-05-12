# 质量服务

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。

## 崩溃服务（Crash）

### 概述

轻量级崩溃解决方案，自动采集应用崩溃信息，帮助快速发现、定位、解决应用崩溃（闪退）问题，避免因崩溃给用户带来糟糕体验。

### 端侧集成

```typescript
import crash from '@kit.CloudFoundation';

// 初始化崩溃服务（AGC 初始化时自动开启）

// 上报自定义异常
crash.recordException({
  name: 'CustomError',
  message: 'Something went wrong',
  stackTrace: new Error().stack
});

// 设置用户标识
crash.setUserId('user_12345');

// 设置自定义日志
crash.setCustomLog('key', 'value');
```

### 崩溃分析指标

| 指标 | 说明 |
|------|------|
| 崩溃率 | 崩溃次数 / 启动次数 |
| 影响用户数 | 发生崩溃的独立用户数 |
| 崩溃趋势 | 按时间维度展示崩溃变化 |
| 崩溃 Top 列表 | 按崩溃次数排序 |

### 告警配置

- 崩溃率超过阈值时自动邮件通知
- 支持设置日/周维度阈值
- 支持多接收人配置

---

## 性能服务（Performance / APM）

### 概述

AppGallery Connect 性能管理（APM, App Performance Management）服务，功能强大、使用简便。无须编写任何代码即可实现可视化数据报告的实时查看。

### 自动采集指标

| 平台 | 采集数据 |
|------|---------|
| Android | ANR 数据、体验分析、启动性能、屏幕性能、HTTP/HTTPS 网络性能、前后台活动性能 |
| iOS | 启动性能、屏幕性能、HTTP/HTTPS 网络性能 |

| 指标 | 说明 |
|------|------|
| 冷启动时间 | 应用冷启动耗时 |
| 热启动时间 | 应用热启动耗时 |
| ANR 率 | 应用无响应次数/启动次数 |
| 网络请求耗时 | HTTP 请求响应时间 |

### 自定义追踪

```typescript
import performance from '@kit.CloudFoundation';

// 创建自定义追踪
let trace = performance.startTrace('load_data');
trace.putAttribute('source', 'cloud_db');

// ... 执行耗时操作

// 停止追踪
trace.stop();
```

---

## 云测试（Cloud Testing）

### 概述

在云端真机或模拟器上进行多种自动化测试，出具详细报告。

### 测试类型

| 类型 | 说明 |
|------|------|
| 兼容性测试 | 遍历测试，快速发现 App 在华为手机上安装/启动/运行/UI/卸载等兼容性问题 |
| 稳定性测试 | Monkey 测试，挖掘长稳运行中的 Crash/ANR/Native crash/Leak 资源泄露等问题 |
| 功耗测试 | 通过耗电行为评估模型，采集 App 耗电数据 |
| 安全测试 | 多维度安全检测，深度识别应用潜在风险 |

---

## 云调试（Cloud Debugging）

### 概述

选择需要的设备，在云端远程调测应用，接近本地设备的调测体验。解决设备机型不足、设备管理困难及 bug 无法复现等问题。

### 核心能力

| 能力 | 说明 |
|------|------|
| ADB 远程代码调试 | 通过 IDE 插件远程 ADB 连接云端设备，如同本地代码调试 |
| 在线日志查看 | 实时日志查看与离线日志导出分析 |
| 多场景模拟 | 横竖屏切换、折叠屏主副屏切换、Mock Location 等 |
| 应用调试 | 从本地上传应用安装至真机设备进行调试 |
| 主题调试 | 上传主题至真机设备进行调试 |

### 注意事项

- 须确保使用**发布证书**（非调试证书）
- Build Mode 须配置为 **release**

---

## 接入检测

### 概述

在应用正式提交审核前，提前扫描应用软件包中影响审核的问题，生成自检报告，帮助提高应用通过审核的概率。

---

## 沙盒测试

### 概述

用于在应用未正式上线前模拟真实用户的使用体验。可在 AGC 控制台创建沙盒测试账号，测试对接现网真实环境的功能（如订单支付测试、游戏功能测试）。

---

## 开放式测试

### 概述

邀请用户参与应用测试，收集真实用户反馈，提前发现问题。

---

## 官方参考

- 崩溃服务：https://developer.huawei.com/consumer/cn/doc/agc-help/crash-introduction-0000001059260949
- 性能服务：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-apm-introduction-0000001052247254
- 测试服务概述：https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-help-test-overview-0000001107794814
- 云调试：https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-help-cloud-debug-0000001110524914
