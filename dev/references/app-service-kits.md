# 应用服务类 Kit 合集

## 概述

应用服务类 Kit 提供日历、联系人、文件预览、阅读、融合场景、通话等系统级应用服务能力，帮助开发者快速集成常见的应用服务功能。

---

## Calendar Kit（日历服务）

### 概述

Calendar Kit提供日历与日程管理能力，允许开发者将应用中与时间相关的日程服务（如出行、餐饮、运动、娱乐等）与系统日历进行集成。

### 核心能力

- 创建/获取/删除日历账户
- 创建/删除/更新/查询日程
- 日程一键服务：通过永久性授权机制，将日程服务以DeepLink形式写入日历，支持服务按钮直达

### npm 包名

`@kit.CalendarKit`

### 关键 API

| API | 说明 |
|---|---|
| CalendarManager | 日历账户管理 |
| Calendar | 日历对象操作 |
| Event | 日程对象操作 |

### 权限要求

| 权限 | 说明 |
|---|---|
| ohos.permission.READ_CALENDAR | 读取系统默认日历账户和当前应用创建的日历账户及日程 |
| ohos.permission.WRITE_CALENDAR | 添加/删除/修改当前应用创建的日历账户及日程 |
| ohos.permission.READ_WHOLE_CALENDAR | 读取所有日历账户及所有应用创建的日程 |
| ohos.permission.WRITE_WHOLE_CALENDAR | 添加/删除/修改所有日历账户及所有应用创建的日程 |

### 约束与限制

- 仅支持Stage模型
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 支持模拟器

### 官方链接

- [Calendar Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-overview)
- [日历账户管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-calendar-developer)
- [日程管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-event-developer)

---

## Contacts Kit（联系人服务）

### 概述

Contacts Kit帮助开发者轻松实现联系人的增删改查等功能，提供Picker选择联系人和联系人管理两类能力。

### 核心能力

- 使用Picker选择联系人（面向所有应用开放，无需权限）
- 联系人管理：增加、删除、修改、查询联系人信息（受限开放）

### npm 包名

`@kit.ContactsKit`

### 关键 API

| API | 说明 |
|---|---|
| @ohos.contact | 联系人管理核心模块 |
| contact.selectContacts | Picker方式拉起联系人列表 |
| contact.addContact | 添加联系人 |
| contact.deleteContact | 删除联系人 |
| contact.updateContact | 更新联系人 |
| contact.queryContact | 查询联系人 |

### 权限要求

| 权限 | 说明 |
|---|---|
| ohos.permission.READ_CONTACTS | 读取联系人（受限开放，仅符合指定场景的应用可申请） |
| ohos.permission.WRITE_CONTACTS | 写入联系人（受限开放，仅符合指定场景的应用可申请） |

### 约束与限制

- Picker选择联系人无需申请权限
- 联系人管理能力受限开放
- 支持模拟器

### 官方链接

- [Contacts Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-intro)
- [使用picker管理联系人](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-addcontactviaui)
- [@ohos.contact API参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-contact)

---

## Preview Kit（文件预览服务）

### 概述

Preview Kit为应用提供便捷的文件快速预览、文件打开加速和通用文件缓存加速能力。

### 核心能力

- 文件预览：对图片、视频、音频、文本、html、文档等进行内容查看
- 文件打开加速：预加载机制提前加载文件，缩短用户打开文件时间
- 通用文件缓存加速：缓存解码数据到磁盘，省去重复解码时间

### npm 包名

`@kit.PreviewKit`

### 关键 API

| API | 说明 |
|---|---|
| canPreview | 判断文件是否支持预览 |
| 文件预览API | 快速启动预览界面 |
| 文件打开加速API | 预加载文件 |
| 通用文件缓存加速API | 缓存解码数据 |

### 支持的文件类型

- 文本：txt、cpp、c、h、java、xhtml、xml
- 网页：html、htm
- 图片：jpg、png、gif、webp、bmp、svg
- 音频：m4a、aac、mp3、ogg、wav
- 视频：mp4、mkv、ts
- 文档：pdf
- Office文档：doc、docx、xls、xlsx、ppt、pptx、csv、ofd

### 权限要求

无特殊权限要求，但访问文件需相应文件访问权限。

### 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 文件预览支持Phone、Tablet和2in1
- 文件打开加速仅支持2in1设备
- 模拟器不支持pdf/pptx/xlsx/docx等文档类文件预览，不支持文件打开加速和通用文件缓存加速

### 官方链接

- [Preview Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-introduction)
- [文件预览](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-filepreview)
- [文件打开加速](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/preview-openfileboost)

---

## Reader Kit（阅读服务）

### 概述

Reader Kit为开发者提供多种格式电子书的解析、排版、阅读交互能力，帮助开发者快速构建书籍阅读应用。

### 核心能力

- 多种格式书籍解析：txt、epub、mobi、azw、azw3
- txt、富文本内容排版：支持仿真和横滑方式分页排版
- 阅读页组件（ReadPageComponent）：显示排版内容、多种翻页交互和翻页动效

### 亮点/特征

- 支持多种电子书籍格式解析
- 对富文本内容（html+css）的排版符合W3C标准规范
- 支持扩展自定义字体
- ReadPageComponent采用OpenGL（C/C++）绘制翻页动效

### npm 包名

`@kit.ReaderKit`

### 关键 API

| API | 说明 |
|---|---|
| BookParser | 电子书解析引擎，支持多种格式书籍文件解析 |
| ReadPageComponent | 阅读页UI组件，支持排版内容显示和翻页交互 |
| SpineItem | 书脊内容节点，标识可阅读的内容资源 |

### 权限要求

无特殊权限要求。

### 约束与限制

- 仅支持有本地文件的书籍，不支持在线文件流
- 不提供DRM保护能力
- 仅支持标准格式书籍，非标准格式可能抛出异常
- 仅适用于HarmonyOS NEXT 5.0.4及以上版本的Phone、PC/2in1、Tablet设备
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 不支持模拟器

### 官方链接

- [Reader Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-introduction)
- [书籍内容解析](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-parser)
- [构建阅读器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/reader-read-page)

---

## Scenario Fusion Kit（融合场景服务）

### 概述

Scenario Fusion Kit基于ArkUI框架组件开发，提供跨多个子系统融合的场景化组件，降低开发者接入复杂度，确保鸿蒙生态体验统一。一行核心代码启用，智能推荐输入建议，复杂表单一键填充。

### 核心能力

#### 场景化Button组件

- 快速验证手机号Button
- 选择头像Button
- 打开APP Button
- 选择收货地址Button
- 选择发票抬头Button
- 地图选点Button
- 权限设置Button
- 获取手机号和风险等级Button
- 服务动态授权码Button
- 元服务分享Button
- 反馈与投诉Button

#### 场景化Input组件

- 省市区选择器Input

#### 场景化API

- 通过API获取系统信息属性
- 通过API异步获取系统信息属性
- 通过API获取系统设置属性
- 通过API展示关注组件
- 文件路径转换API

#### 智能填充服务

- 智能推荐输入建议
- 复杂表单一键填充

### npm 包名

`@kit.ScenarioFusionKit`

### 权限要求

各场景化Button/Input组件内部处理权限申请，开发者无需单独申请。

### 约束与限制

- 大部分场景仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 不同场景支持的设备类型不同（Phone、Tablet、PC/2in1、TV、Wearable）
- 支持模拟器开发，但部分场景在模拟器上不支持

### 官方链接

- [Scenario Fusion Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scenario-fusion-preparations)

---

## Call Service Kit（通话服务）

### 概述

Call Service Kit是HarmonyOS为开发者提供的应用内通话管理服务，支持便捷的来电一键接听、横幅通知、静音与取消静音等功能。

### 核心能力

#### 来电场景

- 应用将来电信息上报给Call Service Kit
- 系统展示来电横幅通知
- 用户可执行接听/拒接、静音/解除静音、挂断等操作
- 支持锁屏来电通知、多路来电通知

#### 去电场景

- 应用主动发起音/视频通话
- 屏幕左上角展示通话胶囊
- 不支持多路共存，同一时间只能有1路去电

### npm 包名

`@kit.CallKit`

### 关键 API

| API | 说明 |
|---|---|
| 来电上报API | 将来电信息上报系统 |
| 通话状态管理API | 管理通话状态 |
| 通话控制API | 接听/拒接/挂断/静音等操作 |

### 权限要求

需申请通话相关权限，具体参考官方文档。

### 约束与限制

- 来电/去电场景支持Phone、Tablet、Wearable
- 企业联系人信息来去电页面显示支持Phone、Tablet、PC/2in1、Wearable
- 同一时间最多支持3路应用内来电
- 同一时间最多支持1路应用内去电
- 仅支持中国大陆
- 依赖Push Kit
- 不支持模拟器

### 与相关 Kit 的关系

- **Push Kit**：应用在后台时，需Push Kit先拉起应用主进程，应用才能给Call Service Kit上报来电

### 官方链接

- [Call Service Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/call-preparations)
- [来电场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/incoming-calls)
