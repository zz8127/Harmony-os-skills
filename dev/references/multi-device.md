# 一次开发，多端部署

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 定义

**一套代码工程，一次开发上架，多端按需部署**

目标：支撑开发者快速高效开发支持多种终端设备形态的应用，实现跨设备的流转、迁移和协同的分布式体验。

---

## 三个核心问题与解决思路

| 问题 | 解决思路 |
|------|---------|
| 页面如何适配 | 布局能力（自适应布局 + 响应式布局） |
| 功能如何兼容 | 功能级一多（资源限定符、设备能力检测） |
| 工程如何组织 | 工程级一多（三层架构 + 多HAP部署） |

---

## 界面级一多

### 自适应布局

元素根据相对关系自动适应容器变化：

| 能力 | 说明 |
|------|------|
| 拉伸能力 | 组件按固定比例拉伸（layoutWeight） |
| 均分能力 | 组件在容器中均分排列 |
| 占比能力 | 组件按百分比设置宽度 |
| 缩放能力 | 组件按设计稿比例缩放（scale） |
| 延伸能力 | 列表等容器自动延伸内容 |
| 隐藏能力 | 内容过多时隐藏次要信息 |
| 折行能力 | 换行继续排列 |

### 响应式布局

| 能力 | 说明 |
|------|------|
| 断点 | 屏幕宽度阈值（xs/sm/md/lg/xl） |
| 栅格 | 12栅格系统 |
| 窗口宽高 | 根据窗口尺寸动态调整布局 |

### 响应式适配

```typescript
@StorageProp('currentBreakpoint') bp: string = 'sm'

Column() {
  if (this.bp === 'sm') {
    this.PhoneLayout()
  } else {
    this.TabletLayout()
  }
}
```

---

## 功能级一多

### 设备能力检测

```typescript
import deviceInfo from '@ohos.deviceInfo'

if (deviceInfo.deviceType === 'phone') {
  // 手机逻辑
} else if (deviceInfo.deviceType === 'tablet') {
  // 平板逻辑
}
```

### API 14+：字体自适应

新增 `fontId` 系统字体唯一标识符，用于在手机→平板/2in1设备分发时合理适配布局和字体：

```typescript
import window from '@ohos.window'

// 获取当前字体ID
let fontId = this.config.fontId
```

### 资源限定符

```
resources/
├── base/           # 默认
├── zh-CN/          # 中文
├── sm/             # 小屏幕设备
├── lg/             # 大屏幕设备
└── dark/           # 深色模式
```

---

## 工程级一多

### 三层工程结构（推荐）

```
/application
├── common/              # 公共基础层
├── features/            # 功能模块层
└── products/            # 产品层
    ├── product_phone/  # 手机HAP
    ├── product_tv/      # 智慧屏HAP
    └── product_wearable/ # 穿戴HAP
```

### API 14+：HSP声明多UIAbility

```json
// HSP模块支持声明非入口UIAbility
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

## 分布式技术

### 四大分布式技术

| 技术 | 说明 |
|------|------|
| 分布式软总线 | 设备间互联互通、统一通信能力 |
| 分布式设备虚拟化 | 多设备资源融合、能力互助 |
| 分布式数据管理 | 跨设备数据同步、用户数据无缝衔接 |
| 分布式任务调度 | 跨设备应用启动、远程调用、迁移 |

### HarmonyOS 6 流转优化（API 22+）

- 逻辑与UI分离使流转开发代码量降低40%以上
- 数据双向绑定机制简化流转步骤

### 平行视界（API 23 新增）

支持应用在折叠屏/平板等大屏设备上实现系统级分栏兼容方案，冷启动自动进入双页布局：

```json
// profile/easy_go.json
{
  "deviceType": "common",
  "displayModeOptions": {
    "landscape": { "splitRatio": "1:1", "primaryWindow": "start" }
  }
}
```

在 `module.json5` 中添加：
```json
"easyGo": "./profile/easy_go.json"
```

支持 `common`、`phone`、`tablet` 三种设备类型，可配置分栏比例和主页位置。

参考：https://developer.huawei.com/consumer/cn/forum/topic/0202207943504517071

### 应用流转（多端协同）

```typescript
import distributedMission from '@ohos.distributedMissionManager'

distributedMission.registerMissionCallback({
  onConnect: (mission, deviceId) => {
    // 流转连接成功
  },
  onDisconnect: (mission, deviceId) => {
    // 流转断开
  }
})
```

---

## 设计原则

| 原则 | 说明 |
|------|------|
| 差异性 | 充分了解设备特性，针对性设计 |
| 一致性 | 设备共性采用通用设计 |
| 灵活性 | 适配不同交互方式（触屏/遥控/语音） |
| 协同性 | 展现多设备无缝流转体验 |
