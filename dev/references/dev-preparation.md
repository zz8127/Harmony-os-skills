# 开发准备

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 环境搭建

### DevEco Studio 安装

1. 下载 DevEco Studio **5.0.2**（最新版）：https://developer.huawei.com/consumer/cn/develop/devo/studio
2. 安装 Node.js（如果未安装）
3. 安装 ohpm（鸿蒙包管理器）
4. 安装 SDK（通过 DevEco Studio 的 SDK Manager）

### SDK 要求

- **DevEco Studio**：5.0.2（推荐）
- **API Version**：23（HarmonyOS 6）
- **JDK**：1.8 及以上
- **Node.js**：最新 LTS 版本

### SDK 版本配套

| 软件 | 版本 | 备注 |
|------|------|------|
| DevEco Studio | 6.1.0 | HarmonyOS 6.1应用开发推荐（稳定） |
| Public SDK | API 23 | 默认获取的稳定版SDK |
| Public SDK (Beta) | API 23+ | 可切换尝鲜Beta版SDK |
| Node.js | LTS | - |

---

## 工程创建

### 创建新工程

1. DevEco Studio → File → New → New Project
2. 选择模板（Empty Ability / Flexible Layout Ability 等）
3. 填写工程信息：
   - **Project name**：工程名
   - **Bundle name**：应用唯一标识（上线后不可修改）
   - **Save location**：工程保存路径

### 三层架构工程（推荐用于多端部署）

```
/application
├── common/          # 公共能力层
├── features/        # 功能模块层
└── products/        # 产品层
    ├── default/     # 手机/平板
    ├── tv/         # 智慧屏
    └── wearable/   # 智能穿戴
```

---

## 应用配置文件

### app.json5（应用级）

```json
{
  "app": {
    "bundleName": "com.example.myapp",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name"
  }
}
```

### module.json5（模块级）

```json
{
  "module": {
    "name": "entry",
    "type": "entry",
    "srcEntry": "./ets/entryability/EntryAbility.ets",
    "description": "$string:module_desc",
    "mainElement": "EntryAbility",
    "deviceTypes": ["phone", "tablet"],
    "deliveryWithInstall": true,
    "pages": "$profile:main_pages",
    "abilities": [
      {
        "name": "EntryAbility",
        "srcEntry": "./ets/entryability/EntryAbility.ets",
        "exported": true,
        "skills": [
          {
            "entities": ["entity.system.home"],
            "actions": ["action.system.home"]
          }
        ]
      }
    ]
  }
}
```

### API 14+：HSP支持声明多UIAbility

```json
{
  "module": {
    "type": "hsp",
    "abilities": [
      {
        "name": "MyHspAbility",
        "srcEntry": "./ets/hspability/MyHspAbility.ets"
      }
    ]
  }
}
```

---

## main_pages.json（页面路由）

```json
{
  "src": [
    { "src": "pages/Index", "name": "Index" },
    { "src": "pages/Detail", "name": "Detail" }
  ]
}
```

---

## 签名配置

### 生成密钥和CSR

DevEco Studio → Build → Generate Key and CSR

### 申请证书（AGC）

1. AGC → 用户与访问 → 证书管理 → 申请证书
2. 上传.csr文件，下载.cer文件

### 申请Profile

1. AGC → 证书管理 → 申请Profile
2. 选择应用、证书
3. 下载.p7b文件

### 自动签名（仅限调试）

DevEco Studio → File → Project Structure → Signing Configs → 勾选 Automatically generate signature

---

## 设备类型

| deviceTypes | 设备类型 |
|-------------|----------|
| phone | 手机 |
| tablet | 平板 |
| tv | 智慧屏 |
| wearable | 智能穿戴 |
| car | 车机 |
| 2in1 | 二合一设备 |
