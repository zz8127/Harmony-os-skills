# ArkWeb

## 概述

ArkWeb（方舟Web）提供了Web组件，用于在HarmonyOS应用中显示Web页面内容。ArkWeb基于Chromium内核开发，为全场景设备提供安全、可靠、一致的网页浏览体验。应用如需渲染网页，必须使用ArkWeb组件。

ArkWeb内核版本与系统版本对应关系：

| 系统版本 | Chromium版本 |
|---|---|
| HarmonyOS 4.0及之前 | M99 |
| HarmonyOS 4.1-5.1 | M114 |
| HarmonyOS 6.0 | M132（默认，推荐）/ M114（可选） |
| HarmonyOS 6.1 | M132 |

## 使用场景

- 应用集成Web页面：在界面中嵌入Web内容，降低开发成本，提升运维效率
- 浏览器网页浏览：打开三方网页、无痕浏览、广告拦截等
- 小程序：渲染小程序页面、同层渲染、视频托管

## 核心能力

- Web页面加载：声明式加载、离屏加载
- 生命周期管理：组件生命周期状态变化、页面加载状态通知
- 常用属性与事件：User-Agent管理、Cookie及数据存储、字体管理、Web深色模式适配、权限管理
- 与应用界面交互：自定义文本选择菜单、上下文菜单、文件上传界面
- JavaScript交互：通过JavaScriptProxy实现ArkTS与Web页面JavaScript双向通信
- 安全与隐私：无痕浏览模式、广告拦截、坚盾守护模式
- 维测能力：DevTools调试、crashpad崩溃信息收集、白屏定位、Hypium自动化测试
- 高阶能力：同层渲染、网络托管、媒体播放托管、自定义输入法、密码保险箱接入
- API 23新增：画中画、字体预加载、同层渲染增强

## npm 包名

@ohos.web.webcomponent（ArkTS API）

## 关键 API

| API | 说明 |
|---|---|
| Web() | 创建Web组件，加载指定URL |
| javaScriptProxy() | 注册ArkTS对象供Web页面JavaScript调用 |
| runJavaScript() | 在Web页面中执行JavaScript脚本 |
| WebCookieManager | Cookie管理 |
| WebDataBase | Web数据存储管理 |
| webview.WebviewController | Web组件控制器，提供页面导航、刷新等操作 |

## 权限要求

访问在线Web网页需申请网络权限：

```
ohos.permission.INTERNET
```

## 官方链接

- ArkWeb简介：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-component-overview
- Web组件API参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/arkts-basic-components-web
- DevTools调试：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-debugging-with-devtools
