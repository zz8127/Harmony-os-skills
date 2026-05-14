# 人机交互与系统特性设计规范

> **适用版本**：HarmonyOS 设计指南
> **所属分类**：设计规范 / HMI & 系统特性

---

## 人机交互概述

### 核心思想

在全场景数字体验中，应用可能在多种设备上运行或通过多种输入方式操控。人机交互的核心思想是"根据用户的状态，提供符合当前状态的交互方式，保证用户交互体验的一致性"。

例如：
- 触屏设备：手指长按进入预览状态打开长按菜单
- 电脑设备：单击鼠标右键打开该菜单

### 输入方式分类

| 分类 | 输入方式 |
|------|---------|
| 直接交互 | 触屏手指、手写笔 |
| 间接交互 | 鼠标、触摸板、键盘、表冠、遥控器、车机摇杆、旋钮、手柄、隔空手势 |
| 语音交互 | 语音指令 |

### 设计原则

- 应用应考虑使用多种输入方式的可能性
- 实现相应功能，保证在当前输入方式下以正确、符合用户习惯的方式响应
- 同一操作在不同输入方式下应提供一致的交互结果

### 支持设备类型

智能手机、平板、电脑、智能穿戴、电视、车机、虚拟现实（VR）和增强现实（AR）等

### 官方链接

- 人机交互概述：https://developer.huawei.com/consumer/cn/doc/design-guides/hmi-overview-0000001795410269
- 手势设计：https://developer.huawei.com/consumer/cn/doc/design-guides/hmi-touchscreen-0000001928273206

---

## 系统特性

### 概述

系统特性定义了 HarmonyOS 提供的系统级 UI 组件和交互模式，应用应遵循这些规范以保证与系统体验的一致性。

### 核心系统特性

| 特性 | 说明 |
|------|------|
| 导航条 | 底部系统导航条，应用需适配避让规则 |
| 通知 | 系统通知设计与交互规范 |
| 实况窗 | 实时状态展示窗口（如通话、导航、运动等） |
| 多窗口交互 | 分屏、悬浮窗等窗口管理交互 |
| 服务卡片 | 桌面/负一屏的服务卡片展示与交互 |
| 画中画 | 小窗播放视频的交互规范 |
| 深色模式 | 深色主题配色与适配规范 |
| 状态栏 | 顶部状态栏的适配与交互 |
| 播控中心 | 媒体播放控制中心交互 |

### 导航条适配要点

- 应用内底部页签、工具栏、文本需自动抬高避让底部导航条
- 可滚动内容可直接显示在导航条下方，滚动到底部时需避让
- 沉浸式页面（全屏视频、游戏、阅读）超过 2 秒自动隐藏导航条
- 从底部上滑或从顶部下滑可恢复显示导航条

### 官方链接

- 系统特性总览：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-0000001826860773
- 导航条：https://developer.huawei.com/consumer/cn/doc/design-guides/navigation-0000001957075737
- 通知：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-notification-0000001793074217
- 实况窗：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-live-view-0000001955186861
- 多窗口交互：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-multi-window-interaction-0000001795392917
- 服务卡片：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-service-widget-0000002087671904
- 画中画：https://developer.huawei.com/consumer/cn/doc/design-guides/pip-0000001927422624
- 深色模式：https://developer.huawei.com/consumer/cn/doc/design-guides/dark-mode-0000001823255497
- 状态栏：https://developer.huawei.com/consumer/cn/doc/design-guides/status-bar-0000001776775568
- 播控中心：https://developer.huawei.com/consumer/cn/doc/design-guides/broadcasting-control-0000001957017133

---

## 官方参考

- 人机交互概述：https://developer.huawei.com/consumer/cn/doc/design-guides/hmi-overview-0000001795410269
- 系统特性：https://developer.huawei.com/consumer/cn/doc/design-guides/system-features-0000001826860773
- 设计概述：https://developer.huawei.com/consumer/cn/doc/design-guides/concept-0000002353669657
- 设计理念：https://developer.huawei.com/consumer/cn/doc/design-guides/design-concepts-0000001795698445
