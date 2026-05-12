# HarmonyOS Skills

![API 23](https://img.shields.io/badge/API-23-blue)
![HarmonyOS 6.1](https://img.shields.io/badge/HarmonyOS-6.1-green)
![MIT License](https://img.shields.io/badge/License-MIT-yellow)

一站式 HarmonyOS 应用开发知识库，覆盖从开发到上架全流程，基于 HarmonyOS 6.1.0 (API 23) 稳定版。

## Skills 目录

| 目录 | 主题 | 覆盖内容 |
|------|------|----------|
| `dev/` | 开发规范 | Stage 模型 / ArkUI / ArkTS / 权限 / 发布 / 数据持久化 / 通知 / 测试 / Web / 架构 |
| `system/` | 系统能力 | 蓝牙 / Wi-Fi / NFC / 定位 / 传感器 / 网络 / 后台任务 / 文件管理 / 密钥 / 分布式 |
| `media/` | 媒体服务 | 相机 / 音视频 / 相册 / 图形 2D |
| `ai-meta/` | AI 与元服务 | 意图框架 / 语音 / MLKit / 元服务 / CANN / 智能体 |
| `design/` | 设计规范 | 色彩 / 字体 / 图标 / 布局 / 动效 / 多设备 |
| `samples/` | 示例代码 | 官方示例 / Gitee 仓 / 按 Kit 分类 |
| `templates/` | 模板组件 | DevEco 模板 / 生态市场 / 主题图标 |
| `agc/` | AGC 服务 | 分发 / 云开发 / 认证 / 增长 / 质量 / 变现 / 游戏服务 |

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

| 项目 | 版本 | 日期 |
|------|------|------|
| HarmonyOS | 6.1.0 | 2026-04-20 |
| API | 23 (Stable) | 2026-04-20 |
| DevEco Studio | 6.1.0 | 2026-04-20 |

## API 24 Beta1 跟踪

> 本项目当前基于 API 23 稳定版。API 24 Beta1 发布后，将逐步适配新特性并标注兼容性说明。
> 跟踪状态：待华为官方发布 API 24 Beta1 SDK。

## 参与贡献

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/your-skill`)
3. 提交改动 (`git commit -m 'Add some skill'`)
4. 推送分支 (`git push origin feature/your-skill`)
5. 发起 Pull Request

## 许可证

[MIT License](LICENSE)
