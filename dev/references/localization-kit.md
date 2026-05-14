# Localization Kit

## 概述

Localization Kit（本地化开发服务）提供应用国际化和本地化能力。国际化（I18n）是系统提供的一套能力集，支持设置区域特性、时区和夏令时等；本地化（L10n）是开发者为满足不同地区用户在语言和文化方面的需求，针对具体目标语言对应用进行翻译和定制。

## 核心能力

### 国际化（I18n）

- 区域特性设置：不同地区的时间日期、数字与度量衡、电话号码、日历和历法、语言等
- 时区和夏令时：获取时区、夏令时跳变等
- 系统语言与区域管理
- 应用偏好语言设置
- 本地习惯排序

### 本地化（L10n）

- 多语言资源配置：配置不同语言或方言的资源
- 资源翻译：UI元素与代码逻辑分离，降低翻译难度
- 敏感禁忌检查：对用户界面显示内容进行检查，避免政治、宗教、文化等方面问题
- 语言测试：检查应用是否存在未翻译字符串、翻译是否准确、界面排版是否符合本地用户习惯

## npm 包名

`@kit.LocalizationKit`

## 关键 API

| API | 说明 |
|---|---|
| @ohos.i18n | 国际化能力，区域特性、时区、日历等 |
| @ohos.intl | 国际化格式化，日期/数字/排序等 |
| @ohos.resourceManager | 资源管理，多语言资源加载 |

## 国际化设计准则

- 不可对用户的文化和习惯进行假设，例如不能假设所有地区均以逗号作为数字分组分隔符
- UI元素（如图片、字符串）应作为应用资源从代码逻辑中分离出来
- 当需要提供其他地区用户版本时，仅需翻译对应资源，避免修改代码逻辑

## 权限要求

无特殊权限要求。

## 约束与限制

- 支持模拟器

## 官方链接

- [国际化和本地化概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n-l10n)
- [应用国际化](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n)
- [多语言适配](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/l10n-multilingual-resources)
- [语言测试](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/linguistic-testing)
- [系统语言与区域](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n-system-language-region)
- [应用偏好语言](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/i18n-preferred-language)
