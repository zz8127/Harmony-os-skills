# IME Kit

## 概述

IME Kit（输入法开发服务）负责建立编辑框所在应用与输入法应用之间的通信通道，确保两者可以共同协作提供文本输入功能，也为系统应用提供管理输入法应用的能力。

## 核心能力

### 输入法应用开发

- 支持创建固定态、悬浮态、状态栏三种类型的Panel
- 可支持开发一个输入法应用同时部署在手机、平板等多设备中
- 提供插入/删除字符、选中文本、监听物理键盘按键事件等能力

### 自定义编辑框

- 支持开发者自定义编辑框，实现绑定输入法应用
- 实现输入法应用的文字输入、删除、选中、光标移动等操作

### 系统管理能力

- 显示/隐藏输入法软键盘
- 切换输入法
- 获取所有输入法列表

## npm 包名

`@kit.IMEKit`

## 关键 API

| API | 说明 |
|---|---|
| inputMethodEngine | 输入法引擎服务API，用于输入法应用开发 |
| inputMethod | 输入法框架API，用于自绘编辑框绑定输入法 |
| InputMethodExtensionAbility | 输入法扩展能力基类 |
| InputMethodExtensionContext | 输入法扩展上下文 |
| inputMethodList | 输入法列表管理API |
| InputMethodSubtype | 输入法子类型管理 |
| inputMethod.Panel | 输入法面板管理 |

## 与相关 Kit 的关系

- **ArkUI**：IME Kit在输入法软键盘和自绘编辑框时使用ArkUI提供的部分组件、事件、动效、状态管理等能力，例如Text、Button组件，onClick点击事件

## 权限要求

- 切换输入法应用的系统API需要申请系统权限
- 部分API仅支持当前输入法应用调用

## 约束与限制

- 针对切换输入法应用的系统API，需要申请系统权限
- 部分API仅支持当前输入法应用调用
- 支持模拟器

## 官方链接

- [IME Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-intro)
- [实现一个输入法应用](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/inputmethod-application-guide)
- [inputMethodEngine API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethodengine)
- [inputMethod API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-inputmethod)
