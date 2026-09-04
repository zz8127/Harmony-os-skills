# HarmonyOS Skills 新电脑迁移指南

> 生成时间：2026-09-04 | 知识库版本：API 26 Release / SDK 26.0.0.821（2026-08-29）| 参考文档总数：137 篇

---

## 一、项目总览

本项目是一站式 **HarmonyOS 应用开发知识库**，基于 Trae/SOLO IDE 的 Skills 机制，覆盖从开发到上架的完整流程。知识库包含 **8 个子技能库 + 137 篇参考文档**，并配置了**每周一 10:00 北京时间自动检查华为官方文档并更新**的定时任务。

### 知识库规模

| 技能目录 | 主题 | 参考文档数 | 覆盖内容 |
|----------|------|-----------|----------|
| `dev/` | 开发规范 | **35** | Stage模型 / ArkUI / ArkTS / ArkData / ArkWeb / 卡片 / 权限 / 发布 / NDK / IPC / 输入法 / 国际化 / 无障碍 / 性能分析 / 华为账号 / 文件服务 / 最佳实践 / 应用FAQ / 行业实践 / 应用质量 / 桌面拓展 / 手写笔 / PDF / 实况窗 / UI设计 / 开发准备 / 测试 |
| `system/` | 系统能力 | **51** | 蓝牙 / Wi-Fi / NFC / 星闪 / 定位 / 传感器 / 网络 / 后台任务 / 文件管理 / 密钥 / 加密框架 / 分布式 / 协同服务 / 测试 / 车机 / 穿戴 / 驱动 / 企业管理 / 企业威胁防护 / 算法加速 / 运动健康 / 天气 / 资产存储 / FFRT / 输入服务 / 多模态融合感知 / 设备证书 / 数据防泄漏 / 在线认证 / 网络加速 / 远场通信 / 企业数据保护 / 企业数字空间 / 用户认证 / 设备安全 / 基础服务 / 熄屏导航 / 机密空间 / 灵犀加速 / 服务与支持 / 机械设备管理 / 电话蜂窝 / 扫码 / 分享 / 地图 / 电源 / 配件服务 |
| `media/` | 媒体服务 | **11** | 相机 / AVPlayer / AVSession / AudioKit / AVCodecKit / DRM+铃声 / ImageKit / 2D绘制 / 3D图形+空间重建 / AR Engine / 相册 |
| `ai-meta/` | AI与元服务 | **6** | 意图框架 / 语音+视觉 / 核心AI / CANN+推理运行时 / 元服务 / 智能体框架 |
| `design/` | 设计规范 | **14** | 设计原则 / 色彩 / 字体 / 图标 / 布局 / 动效 / 人机交互+系统特性 / UX最佳实践 / 41个控件 / 多设备设计 / 元服务设计 / 设计变更说明 / 设计资源概览 / 多设备开发 |
| `agc/` | AGC服务 | **8** | 应用分发 / 云开发+Connect API / 认证+账号服务 / 增长（推送+AppLinking）/ 质量+崩溃分析 / 变现（广告+IAP+支付+钱包+AppGallery）/ 游戏服务 / 应用分析+行业风向标 |
| `samples/` | 示例代码 | **8** | 应用框架 / 应用服务 / 图形 / 媒体 / 网络 / 系统 / AI / 工具与测试 |
| `templates/` | 模板组件 | **4** | DevEco Studio 内置模板 / 生态市场模板 / 设计资源 / ArkUI 组件规范 |
| **合计** | | **137** | |

---

## 二、新电脑迁移步骤（按顺序执行）

### 步骤 1：安装基础软件

```
1. 安装 Git：https://git-scm.com/download/win
   （默认安装路径 C:\Program Files\Git 或 D:\Program Files\Git 均可，后续需核对路径）

2. 安装 Trae IDE / SOLO IDE：https://trae.cn 下载安装包

3. 注册并登录三个代码托管平台账号（如未注册）：
   - Gitee：https://gitee.com
   - GitCode：https://gitcode.com
   - GitHub：https://github.com
```

### 步骤 2：克隆项目到新电脑

在新电脑任选一个空目录（如 `D:\Projects\HarmonyOS`），在 Trae IDE 终端中执行：

```bash
git clone https://gitee.com/zeng-jinxi/harmony-os-skills.git D:\Projects\HarmonyOS
cd D:\Projects\HarmonyOS
```

### 步骤 3：添加三个远程仓库

```bash
# 已默认有 origin(Gitee)，添加另外两个
git remote add gitcode https://gitcode.com/z812731674/Harmony-os-skills.git
git remote add github  https://github.com/zz8127/Harmony-os-skills.git

# 验证三个远程都存在
git remote -v
```

预期输出：
```
origin   https://gitee.com/zeng-jinxi/harmony-os-skills.git (fetch/push)
gitcode  https://gitcode.com/z812731674/Harmony-os-skills.git (fetch/push)
github   https://github.com/zz8127/Harmony-os-skills.git (fetch/push)
```

### 步骤 4：在 Trae IDE 中加载 Skills

将项目打开为工作区，IDE 会自动识别 Skills。如果没有自动加载：
- 打开项目的 `SKILL.md` 根文件（HarmonyOS 生态知识库总索引）
- 再分别打开各子目录 `dev/SKILL.md`、`system/SKILL.md` 等确保缓存生成

### 步骤 5：验证 Git 路径

在 Trae IDE 终端中执行以下命令检查 Git 是否可用：

```powershell
# 若默认 PATH 中找不到，老电脑用的是：
& "D:\Program Files\Git\cmd\git.exe" --version

# 新电脑根据实际安装路径调整，记录下完整路径，定时任务中要用
```

---

## 三、定时任务重建（重要：每周自动更新知识库）

### 在新电脑的 Trae IDE 对话中，一次性发送以下内容重建定时任务：

> **复制以下整块内容，直接发送到新电脑 Trae IDE 的对话中即可自动完成定时任务创建：**

---

```
请帮我创建一个定时任务，配置如下：

任务名称：HarmonyOS API 版本周检

Cron 表达式：0 10 * * 1（每周一上午 10:00，Asia/Shanghai 时区）

任务消息（完整 Prompt）：

----------------------------------------
HarmonyOS Skills 版本周检与更新任务。

**检查入口**：从华为开发者文档首页 https://developer.huawei.com/consumer/cn/doc/ 进入，逐项对比现有 Skills 文档与官方最新内容的差异。

**工作目录**：【请替换为新电脑项目根目录的绝对路径，例如 D:\Projects\HarmonyOS】

**参考文档基数**（供对比参考）：dev/ 35 篇、system/ 51 篇、media/ 11 篇、ai-meta/ 6 篇、design/ 14 篇、agc/ 8 篇、samples/ 8 篇、templates/ 4 篇，共 137 篇。文档实际数量以每次周检统计为准，README.md 中的统计和徽章数字需要同步更新。

**执行步骤**：

1. **获取官方最新版本信息**：
   - WebFetch https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/overview-allversion 获取版本列表
   - 对比根 SKILL.md 的「版本历史」表格，检查是否有新版本发布（26.0.0 Release / 27.0.0 Beta 等）
   - 如果有新版本，WebFetch 该版本的版本说明和 OS 新特性页面，收集 30+ Kit 的新增或增强能力

2. **从文档首页检查 Kit 变更**：
   - WebFetch https://developer.huawei.com/consumer/cn/doc/ 获取文档首页
   - 逐领域对比首页列出的所有 Kit（应用框架 / 系统 / 媒体 / 图形 / 应用服务 / AI）与现有 references/ 目录下的文件
   - 检查是否有新增 Kit 或 Kit 描述变更；Mechanic Kit 这类"仅在 API 变更清单中存在但官方未发布指南页"的情形，记为待收录并在周检记录中说明
   - 如有新增 Kit，从首页进入对应 Kit 的官方文档链接获取详细内容（必须 WebFetch 官方页面后基于页面最新内容编写，禁止臆造）

3. **更新文档**（如有变更）：
   - 在根 SKILL.md 的版本历史表格新增一行（HarmonyOS 版本 / API / DevEco Studio / 性质 / 日期）
   - 在根 SKILL.md 末尾新增「周检记录（YYYY-MM-DD）」小节，记录本周发现的版本变化、新增/变更 Kit、补充内容
   - 更新「HarmonyOS 26.x 新增特性」章节（或对应新版本的特性章节），按领域列出各 Kit 新增/增强
   - 更新各子 Skill 的 SKILL.md 版本适配说明、API 变更追踪、导航表格
   - 创建或更新对应的 references/ 文件：标题 # Kit名称、概述、核心能力、npm包名、关键API、权限/设备/区域约束、版本变更、官方链接；文件必须保存为纯 UTF-8 编码，禁止出现鎴銆等 GBK→UTF-8 双重编码乱码字符

4. **更新 README.md（必做，即使本周无 Kit 变更）**：
   - 检查「版本信息」表格，与根 SKILL.md「版本历史」最新三行保持一致，过期则更新
   - 检查「版本变更追踪」章节，若 API 26 Release/API 27 等有新状态，更新说明
   - 统计 8 个 references/ 子目录下实际 .md 文件数，更新「Skills 目录」表中"参考文档数"列，以及顶部徽章中的文档总数（当前137篇，每次周检后变动）
   - 若新增了 Kit/专题，同步更新对应目录行的"覆盖内容"描述

5. **3 次检查机制（防止更新不到位）**：
   - 第 1 次检查：完成所有上述更新步骤
   - 第 2 次检查：重新读取所有修改/新增的文件（含 README.md 和各 SKILL.md），验证内容完整性、表格格式正确性、本地 references/ 链接的目标文件实际存在
   - 第 3 次检查：确认 git push 成功推送到 Gitee（origin）、GitCode（gitcode）和 GitHub（github）三个远程仓库，任一仓库失败需重试最多 3 次

6. **Git 提交与推送**（PowerShell 语法，注意 Git 完整路径）：
   ```
   & "Git的完整路径，例如 D:\Program Files\Git\cmd\git.exe" add -A
   & "Git的完整路径" commit -m "chore: 周检更新 - YYYY-MM-DD"
   & "Git的完整路径" push origin master
   & "Git的完整路径" push gitcode master
   & "Git的完整路径" push github master
   ```

7. **无变更处理**：
   - 若检查后版本、OS 新特性页、官方首页 Kit 均无变化，输出"本周检查无新变更"即可，无需 git commit
   - 例外：若 README.md 的版本信息或文档统计数字与实际不符，仍需更新并单独提交
   - 例外：若已有 references/ 文件内容与官方最新页面有差异（子能力新增/权限变更），仍需更新并提交

**注意事项**：
- 所有新增/更新内容必须基于 WebFetch 官方文档链接获取的最新页面内容，确保时效性和正确性，禁止臆造 Kit 名称或 API 参数
- 不要修改 .trae/ 目录下的文件
- 所有文档内容使用中文，不加任何代码注释
- 三个远程仓库 origin(Gitee)、gitcode(GitCode)、github(GitHub)，推送时必须三个都推

----------------------------------------
```

---

### 定时任务参数速查（若发送上面整块对话还没自动创建，可手动在 Trae 定时任务界面按此填表）

| 字段 | 值 |
|------|----|
| **任务名称** | HarmonyOS API 版本周检 |
| **Cron 表达式** | `0 10 * * 1` |
| **时区** | `Asia/Shanghai` |
| **下次执行** | 下周一 10:00（若今天是周一且已过 10 点，就是下下周一）|
| **Prompt 消息** | 上面整块内容（执行步骤 1~7 + 注意事项）|

---

## 四、验证新电脑迁移成功的检查清单

按顺序完成以下验证，全部打勾即迁移完成：

- [ ] `git clone` 成功，项目目录下可看到 8 个子目录（dev/ system/ media/ ai-meta/ design/ agc/ samples/ templates/）
- [ ] `git remote -v` 显示三个远程：origin + gitcode + github
- [ ] 根目录 SKILL.md、README.md、LICENSE 均存在且能正常读取（中文无乱码）
- [ ] `dev/references/arkts.md`、`system/references/test-kit.md`、`media/references/ar-engine.md` 三个新增文件存在
- [ ] Trae IDE 对话中发送"开发 HarmonyOS 蓝牙 BLE 功能"会自动加载 system/ 技能
- [ ] 在 Trae 定时任务列表中可看到「HarmonyOS API 版本周检」任务，状态 Active，Cron 0 10 * * 1
- [ ] 手动执行一次 `git push --dry-run origin master` 不报错（验证推送权限配置正确）

---

## 五、常用 Git 命令速查（新电脑日常使用）

```bash
# 查看变更
git status
git diff

# 日常提交
git add -A
git commit -m "描述"
git push origin master
git push gitcode master
git push github master

# 拉取最新（避免冲突）
git pull origin master

# 三仓库同步拉取
git fetch --all
```

---

## 六、问题排查

| 常见问题 | 解决方法 |
|----------|---------|
| 终端中 `git` 命令找不到 | 使用完整路径 `& "C:\Program Files\Git\cmd\git.exe"` 或把 Git 安装路径加入系统 PATH |
| 推送 GitHub 连接被重置 | 重试 2-3 次；国内网络偶发，或用 `git remote set-url github git@github.com:zz8127/Harmony-os-skills.git` 改用 SSH |
| 文件写入后中文乱码 | 所有写入必须是纯 UTF-8 编码，本项目禁止使用 GBK/GB2312；乱码文件需从官方文档 WebFetch 最新内容后重写 |
| references/ 中有些链接点击跳转错 | 检查 SKILL.md 中导航条目路径：同目录下 references/xxx.md 用相对路径，跨目录用 `../xxx/references/xxx.md` |
| 定时任务创建后不执行 | 检查 Cron 时区是否选 Asia/Shanghai；Trae IDE 定时任务页面中是否状态为 Active（非 Paused） |

---

## 七、附录：137 篇参考文档完整清单（用于对比是否齐全）

### dev/（35 篇）
accessibility-kit / account-kit / app-faq / app-framework / app-quality / app-service-kits / architecture / arkdata / arkts / arkweb / best-practices / core-file-kit / data-augmentation-kit / desktop-extension-kit / dev-preparation / deveco-service / file-manager-service-kit / form-kit / ime-kit / industry-practices / ipc-kit / live-view-kit / localization-kit / multi-device / ndk-development / notification / other / pdf-kit / pen-kit / performance-analysis-kit / permissions / publish / testing / ui-design-kit / ui-development

### system/（51 篇）
accessory-kit / aod-navigation-kit / asset-store-kit / background-task / basic-services / ble / bluetooth-bredr / car-kit / confidential-space-kit / crypto-architecture / data-loss-prevention-kit / device-certificate-kit / device-info / device-security / distributed / driver-kit / enterprise-data-guard-kit / enterprise-kits / enterprise-space-kit / enterprise-threat-protection-kit / fast-kit / ffrt-kit / file-management / health-service-kit / input-kit / input-multimodal-kit / keystore / linx-kit / location / map-kit / mdm-kit / mechanic-kit / multimodal-awareness-kit / nearlink-kit / network-boost-remote-kit / network / nfc / online-authentication-kit / power / remote-communication-kit / scan-kit / security-kits / sensor / service-collaboration-kit / service-support-kit / share-kit / telephony-kit / test-kit / wear-engine-kit / weather-service-kit / wifi

### media/（11 篇）
ar-engine / arkgraphics-3d / audio-kit / avcodec-kit / avplayer / avsession / camera / drm-ringtone-kit / graphics2d / image-kit / photo

### ai-meta/（6 篇）
agent-framework / cann-kit / core-ai-kits / intent-speech / meta-service / mindspore-nnrt-kit

### design/（14 篇）
animation / atomic-service-design / color / controls / design-changes / hmi-system-features / icon / layout / multi-device / multi-device-design / overview / resources / typography / ux-best-practices

### agc/（8 篇）
analytics / auth / cloud-development / distribution / game-service / growth / monetization / quality

### samples/（8 篇）
ai / app-framework / app-service / graphics / media / network / system / tool-test

### templates/（4 篇）
arkui-components / design-resources / deveco-templates / market-templates
