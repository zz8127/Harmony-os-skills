# DevEco Studio 工程模板

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template

## 创建工程

`DevEco Studio → File → New → Create Project`

### 模板类型详解

#### Empty Ability（推荐）

适用设备：Phone / Tablet / 2in1

- 最基础的 Stage 模型工程
- 包含 Entry HAP + 一个 EntryAbility
- 适合学习阶段和小型项目

```
entry/src/main/ets/
├── entryability/
│   └── EntryAbility.ets      # 程序入口
├── pages/
│   └── Index.ets             # 首页
└── app.ets                   # 应用生命周期
```

#### Atomic Service（元服务）

适用设备：全部（手机/平板/手表/电视等）

- 免安装的小程序形态
- 支持服务卡片（Widget）
- 需在 module.json5 中配置 `metadata` 声明元服务

```json
{
  "app": {
    "bundleName": "com.example.atomic",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name"
  },
  "module": {
    "type": "entry",
    "srcEntry": "./ets/entryability/EntryAbility.ets",
    "skills": [
      {
        "entities": ["entity.system.home"],
        "actions": ["action.system.home"]
      }
    ]
  }
}
```

#### Native C++（Native 开发）

适用设备：Phone / Tablet

- 支持 C++ 编写Native侧代码
- 可调用方舟引擎能力
- 适合性能敏感场景（游戏/图形/音视频）

```
entry/src/main/cpp/
├── CMakeLists.txt
├── hello.cpp
└── napi/
    └── mymodule.cpp
```

#### TV（智慧屏）

适用设备：华为智慧屏（TV）

- 遥控器交互模式
- 4K 分辨率适配
- 支持分布式能力

#### Wearable（智能手表）

适用设备：华为手表

- 圆形表盘 UI
- 低功耗优化
- 传感器数据接入

#### Car（车机）

适用设备：车机

- 大屏触控+语音交互
- 驾驶安全模式
- 多设备协同

---

## SDK 版本与模板配套

| DevEco Studio | 对应模板 SDK | 说明 |
|---------------|-------------|------|
| **6.1.0** | **API 23（稳定）** | **当前最新版** |
| 5.0.4 | API 16 | 稳定版 |
| 3.1.1 | API 9 | 老版本 |

> ⚠️ 建议使用 DevEco Studio 6.1.0 新建工程，确保 SDK 为最新稳定版。

---

## 模板自定义

创建工程后可在以下文件中调整配置：

| 文件 | 用途 |
|------|------|
| `AppScope/app.json5` | 应用全局配置（bundleName/版本等） |
| `entry/src/main/module.json5` | 模块配置（abilities/路由等） |
| `entry/src/main/resources/` | 资源文件（图片/字符串/主题） |
| `hvigor/build-profile.json5` | 构建配置 |

---

## 常见问题

**Q：创建模板后提示 SDK 缺失？**
A：进入 File → Settings → SDK Manager，下载对应版本的 HarmonyOS SDK。

**Q：如何将 Empty Ability 改为元服务？**
A：在 module.json5 的 `abilities` 中添加 `skills` 配置，声明 `entity.system.home` 和 `action.system.home`。

**Q：TV/手表模板找不到？**
A：在 DevEco Studio 新建工程时选择对应设备类型 Tab（如 TV/Wearable）。
