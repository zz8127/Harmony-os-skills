# 控件设计规范

> **适用版本**：HarmonyOS NEXT 设计指南。兼容 HarmonyOS 6.0+。

## 概述

HarmonyOS 提供了完整的控件设计规范体系，涵盖导航类、展示类、操作类、输入类、选择类和容器类六大分类。每个控件都有详细的布局规则、交互规范和多设备适配说明，帮助开发者构建一致且高质量的用户界面。

---

## 控件分类

### 导航类

| 控件 | 说明 |
|------|------|
| 底部页签（BottomTab） | 底部导航栏，用于应用主页面间切换 |
| 子页签（ChipsGroup） | 页面内次级导航，用于内容分类筛选 |
| 标题栏（TitleBar） | 页面顶部标题区域，含返回、标题、操作按钮 |
| 导航点（Swiper） | 轮播指示器，标识当前页面位置 |

### 展示类

| 控件 | 说明 |
|------|------|
| 文本（Text） | 基础文本展示 |
| 分隔器（Divider） | 内容分隔线 |
| 子标题（SubHeader） | 内容区块标题 |
| 进度条（Progress） | 进度状态展示 |
| 索引条（AlphabetIndexer） | 字母索引导航 |
| 滚动条（ScrollBar） | 滚动位置指示 |
| 新事件标记（Badge） | 未读/新消息角标 |
| 即时反馈（Toast） | 轻量级操作反馈提示 |
| 即时操作（SnackBar） | 底部操作反馈条 |
| 气泡提示（Popup） | 悬浮气泡信息提示 |
| 数据可视化（DataPanel） | 数据图表展示 |
| 二维码（QRCode） | 二维码展示 |
| 文本时钟（TextClock） | 实时时钟展示 |
| 图片（Image） | 图片展示 |
| 空白（Blank） | 弹性空白填充 |

### 操作类

| 控件 | 说明 |
|------|------|
| 按钮（Button） | 基础操作按钮 |
| 下拉按钮（Select） | 下拉选择操作 |
| 状态按钮（ToggleButton） | 开关状态切换按钮 |
| 操作块（Chips） | 紧凑型操作入口 |
| 工具栏（Toolbar） | 操作工具集合栏 |
| 核心操作栏（ActionBar） | 页面核心操作区域 |
| 菜单（Menu） | 弹出式操作菜单 |
| 文本选择菜单（TextSelection） | 文本选中后的操作菜单 |

### 输入类

| 控件 | 说明 |
|------|------|
| 文本框（TextInput） | 单行文本输入 |
| 搜索框（Search） | 搜索内容输入 |
| 数字加减（Counter） | 数值增减输入 |
| 图案锁（PatternLock） | 图案密码输入 |

### 选择类

| 控件 | 说明 |
|------|------|
| 勾选（Checkbox） | 多选勾选框 |
| 开关（ToggleSwitch） | 开关切换 |
| 单选框（Radio） | 单选选择 |
| 评分条（Rating） | 星级评分 |
| 滑动条（Slider） | 连续值选择 |
| 选择器（Picker） | 滚轮式选择器 |
| 分段按钮（SegmentButton） | 分段式选择按钮 |

### 容器类

| 控件 | 说明 |
|------|------|
| 列表（List） | 垂直滚动列表容器 |
| 弹出框（Dialog） | 模态弹窗容器 |
| 半模态面板（BindSheet） | 底部半屏弹出面板 |

---

## 设计原则

1. **优先使用系统控件**：利用系统提供的标准控件，保证良好基础体验，减少设计和开发工作量
2. **必要时自定义**：自定义控件样式和大小以体现品牌特征，但需遵循交互规范
3. **多设备适配**：所有控件均需适配 Phone、Tablet、PC/2in1、Wearable 等设备
4. **智能穿戴适配**：部分控件已新增智能穿戴设备内容，需关注圆形表和方形表的布局差异

---

## 官方链接

- [控件概览](https://developer.huawei.com/consumer/cn/doc/design-guides/general_overview-0000001929599380)
- [导航类控件](https://developer.huawei.com/consumer/cn/doc/design-guides/component_navigation-0000001929763488)
- [按钮设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/button-0000001929683228)
- [列表设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/list-0000001929853910)
- [弹出框设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/dialog-0000001957012569)
- [半模态面板设计规范](https://developer.huawei.com/consumer/cn/doc/design-guides/bindsheet-0000001956852753)
