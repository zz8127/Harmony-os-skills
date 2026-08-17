# HarmonyOS Skills

![API 23/24](https://img.shields.io/badge/API-23%2F24-blue)
![HarmonyOS 6.1](https://img.shields.io/badge/HarmonyOS-6.1-green)
![Docs](https://img.shields.io/badge/参考文档-121篇-orange)
![MIT License](https://img.shields.io/badge/License-MIT-yellow)

一站式 HarmonyOS 应用开发知识库，覆盖从开发到上架全流程。以 HarmonyOS 6.1.0 (API 23) 为基准，兼容 API 24 (6.1.1 Release)，并跟踪 API 26 Beta。

## Skills 目录

| 目录 | 主题 | 参考文档数 | 覆盖内容 |
|------|------|-----------|----------|
| `dev/` | 开发规范 | 34 | Stage 模型 / ArkUI / ArkTS / ArkData / ArkWeb / 卡片 / 权限 / 发布 / NDK / IPC / 输入法 / 国际化 / 无障碍 / 性能分析 / 华为账号 / 文件服务 / 最佳实践 / 应用 FAQ / 行业实践 / 应用质量 |
| `system/` | 系统能力 | 36 | 蓝牙 / Wi-Fi / NFC / 星闪 / 定位 / 传感器 / 网络 / 后台任务 / 文件管理 / 密钥 / 加密框架 / 分布式 / 协同服务 / 测试 / 车机 / 穿戴 / 驱动 / 企业管理 / 企业威胁防护 / 算法加速 / 运动健康 / 天气 |
| `media/` | 媒体服务 | 11 | 相机 / AVPlayer / AVSession / AudioKit / AVCodecKit / DRM / 铃声 / ImageKit / 2D 绘制 / 3D 图形 / AR Engine |
| `ai-meta/` | AI 与元服务 | 6 | 意图框架 / 语音 / 视觉 / Core AI / CANN / MindSpore / 推理运行时 / 元服务 / 智能体框架 |
| `design/` | 设计规范 | 14 | 设计原则 / 色彩 / 字体 / 图标 / 布局 / 动效 / 人机交互 / UX 最佳实践 / 控件 / 多设备设计 / 元服务设计 / 设计变更说明 |
| `samples/` | 示例代码 | 8 | 官方示例 / Gitee 仓 / 按 Kit 分类 / 工具与测试 |
| `templates/` | 模板组件 | 4 | DevEco 模板 / 生态市场 / 主题图标 / ArkUI 组件规范 |
| `agc/` | AGC 服务 | 8 | 分发 / 云开发 / 认证 / 增长 / 质量 / 变现 / 游戏服务 / 应用分析 |

## 快速开始

### 在 SOLO / Trae IDE 中使用

1. 将本项目克隆到本地任意目录
2. 在 SOLO 或 Trae IDE 中打开项目工作区
3. IDE 会自动识别 `skills/` 目录下的 Skill 定义文件
4. 在对话中直接描述你的开发需求，AI 会自动匹配并加载对应 Skill

示例对话：

```
"我想开发一个蓝牙BLE设备扫描功能"     → 自动加载 system/ 蓝牙 Skill
"帮我设计一个符合HarmonyOS规范的登录页" → 自动加载 design/ 设计规范 Skill
"如何把应用发布到AppGallery"          → 自动加载 agc/ 分发 Skill
```

## 版本信息

| 项目 | 版本 | 说明 | 日期 |
|------|------|------|------|
| HarmonyOS | 26.0.0 (Beta) | API 26 Beta2（DevEco Studio 26.0.0.621） | 2026-07-28 |
| HarmonyOS | 6.1.1 (Release) | API 24（DevEco Studio 6.1.1.290），生产环境推荐 | 2026-06-30 |
| HarmonyOS | 6.1.0 (稳定) | API 23（DevEco Studio 6.1.0.830），本知识库基准版本 | 2026-04-20 |

## 版本变更追踪

- **API 24 (6.1.1 Release)**：已发布。各 Skill 的 SKILL.md 中均含"API 24 Beta1 变更追踪"章节，记录 Ability Kit / ArkUI / ArkTS / ArkWeb / FAST Kit / Content Embed Kit / Enterprise Threat Protection Kit 等变更。
- **API 26 (26.0.0 Beta)**：Beta 阶段，持续跟踪中。待正式发布后纳入正式文档。

## 自动周检

项目配置了定时任务（每周一 10:00 北京时间）：

1. 从[华为开发者官方文档首页](https://developer.huawei.com/consumer/cn/doc/)进入，检查新版本与 Kit 变更
2. 对比现有 Skills 文档，补充缺失内容
3. 更新本 README.md 的版本信息与统计
4. 三轮检查机制确保更新到位后，推送至 Gitee / GitCode / GitHub

## 参与贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/your-skill`)
3. 提交改动 (`git commit -m 'Add some skill'`)
4. 推送分支 (`git push origin feature/your-skill`)
5. 发起 Pull Request

## 许可证

[MIT License](LICENSE)
