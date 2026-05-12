# UI开发 — ArkUI声明式开发

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 开发范式

ArkUI提供两种开发范式：

| 范式 | 语言 | 适用场景 |
|------|------|----------|
| 声明式开发（主推） | ArkTS | 大型应用、复杂度高、团队协作 |
| 类Web开发 | JS + HML + CSS | 简单应用、Web前端开发者 |

**新项目一律使用ArkTS声明式开发范式。**

---

## ArkUI 引擎升级（HarmonyOS 6 / API 22+）

### NODE级函数式更新

ArkUI通过编译器生成特定函数，将UI组件更新和数据变更**细粒度绑定**：

- **旧机制**：COMPONENT/ELEMENT 树形结构 Diff 对比（API 12及之前）
- **新机制**：单节点 NODE 函数式更新（API 14+）
- **效果**：布局渲染性能大幅优化，声明式UI组件树形结构简化

### 逻辑与UI分离

通过数据双向绑定机制传递页面变化逻辑：
- 流转开发代码量**降低40%以上**
- 跨端迁移和协同开发效率显著提升

---

## HarmonyOS 6.1 新增特性（API 23）

### ArkUI 增强（6.1.0 Release 新增）

#### List/Grid 长按聚拢动效

List 与 Grid 组件支持长按聚拢动效，交互操作更直观：

```typescript
// List 组件长按聚拢
List() {
  ForEach(this.data, (item) => {
    ListItem() { /* ... */ }
  })
}
.enableStickyDrag(true)  // 启用长按拖拽聚拢
```

#### 自定义组件 Attach/Detach 生命周期

新增 Attach 与 Detach 阶段，完善多语言环境排版与阅读：

```typescript
@Component
struct MyComponent {
  // 生命周期：aboutToAppear → onAttach → [build] → onDetach → aboutToDisappear
  
  onAttach() {
    console.info('组件已附加到组件树')
  }
  
  onDetach() {
    console.info('组件已从组件树分离')
  }
}
```

#### Navigation 分栏样式可定制

满足多栏布局下的个性化设计需求：

```typescript
Navigation() {
  // 自定义分栏样式配置
}
.navBarStyle(NavBarStyle.STACK)  // 可定制分栏模式
```

### 悬浮标签页 + 迷你栏

`HdsTabs` 组件（`@kit.UIDesignKit`）支持 `barFloatingStyle`，可实现悬浮页签栏 + 可折叠迷你栏的组合：

```typescript
import { HdsTabs, HdsTabsController } from '@kit.UIDesignKit';

// 设置页签栏悬浮样式
HdsTabs({
  barFloatingStyle: {
    barOverlap: true,
    vertical: false,
    barPosition: BarPosition.End,
    miniBar: { expanded: true }  // 可折叠迷你栏
  }
})
```

使用场景：音乐/播客应用的快捷媒体控制器（播放/暂停 ↔ 快进/快退）

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-bar-floating

### 沉浸光感视效

HDS 组件支持 `systemMaterialEffect`，系统根据设备算力自动适配材质效果：

```typescript
// 系统自适应（推荐）
HdsTabsFloatingStyle({
  systemMaterialEffect: 'AUTO'  // 系统自动平衡性能与显示
})

// 手动控制
let types = hdsMaterial.getSystemMaterialTypes();
if (types.includes('IMMERSIVE')) {
  // 手动选用 EXQUISITE / GENTLE / SMOOTH
}
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-bar-floating

### 平行视界（折叠屏/平板）

支持 `easy_go.json` 配置文件，应用在大屏/折叠屏首次冷启动自动分栏：

```json
// profile/easy_go.json
{
  "deviceType": "common",
  "displayModeOptions": {
    "landscape": { "splitRatio": "1:1", "primaryWindow": "start" },
    "portrait": { "splitRatio": "1:1", "primaryWindow": "start" }
  }
}
```

在 `module.json5` 中配置 `easyGo` 字段指向该配置文件。

参考：https://developer.huawei.com/consumer/cn/forum/topic/0202207943504517071

---

## ArkTS基础

### 基本页面结构

```typescript
@Entry
@Component
struct Index {
  @State message: string = 'Hello HarmonyOS 6'

  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
      Button('Click me')
        .onClick(() => {
          this.message = 'Clicked!'
        })
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Center)
  }
}
```

### ArkTS vs TypeScript 差异

- **强制使用静态类型**：必须声明变量类型
- **禁止structural typing**：不支持对象展开等操作
- **禁止any类型隐式转换**

### 装饰器

| 装饰器 | 作用域 | 说明 |
|--------|--------|------|
| `@Entry` | struct | 页面入口 |
| `@Component` | struct | 定义组件 |
| `@Preview` | struct | 预览器预览 |
| `@State` | 变量 | 组件内私有状态 |
| `@Prop` | 变量 | 父→子单向传递 |
| `@Link` | 变量 | 父↔子双向同步 |
| `@Provide` | 变量 | 祖先→后代单向传递 |
| `@Consume` | 变量 | 响应@Provide |
| `@ObjectLink` | 变量 | 嵌套对象双向绑定 |
| `@Builder` | 方法 | 自定义构建函数 |
| `@Styles` | 方法 | 组件复用样式 |
| `@Extend` | 方法 | 多态样式扩展 |

---

## 布局容器

### 线性布局（Column / Row）

```typescript
Column({ space: 10 }) { }           // 垂直排列
  .width('100%')
  .height('100%')
  .alignItems(HorizontalAlign.Center)
  .justifyContent(FlexAlign.SpaceEvenly)

Row({ space: 5 }) { }                // 水平排列
```

### 弹性布局（Flex）

```typescript
Flex({
  direction: FlexDirection.Row,
  justifyContent: FlexAlign.SpaceBetween,
  alignItems: ItemAlign.Center
}) { }
```

### 层叠布局（Stack）、相对布局（RelativeContainer）、栅格（Grid）、列表（List）等

用法与 API 12 版本基本一致，参考组件文档。

---

## 新增组件与能力（API 14+）

### 粒子动画（API 12+）

```typescript
@Entry
@Component
struct ParticleExample {
  build() {
    Stack() {
      Text('Snow Effect')
        .width(300).height(300)
        .backgroundColor('rgb(240, 250, 255)')

      Particle({
        particles: [{
          emitter: {
            particle: {
              type: ParticleType.POINT,
              config: { radius: 5 },
              count: 100
            },
            color: { range: ['rgb(39, 135, 222)'] }
          }
        }]
      })
    }
    .width('100%').height('100%')
  }
}
```

### 属性动画（API 14+ 增强）

属性动画支持更多维度：

| 分类 | 可动画属性 |
|------|-----------|
| 布局属性 | 位置、大小、内/外边距、权重等 |
| 仿射变换 | 平移、旋转、缩放、锚点等 |
| 背景 | 背景颜色、背景模糊等 |
| 内容 | 文字大小/颜色、图片对齐、模糊等 |
| 前景 | 前景颜色等 |
| 外观 | 透明度、圆角、边框、阴影等 |

### 组件尺寸变化事件（API 12+）

```typescript
Text('Resize Me')
  .onSizeChange((oldValue, newValue) => {
    console.info(`Old: ${JSON.stringify(oldValue)}, New: ${JSON.stringify(newValue)}`)
  })
```

### InterstitialDialogAction（API 12+，元服务）

用于元服务中临时展示信息或待处理操作的自定义弹框。

### API 14+：模糊效果（ArkGraphics2D）

```typescript
Text('Blur Effect')
  .backdropBlur(20)  // 背景模糊
  .foregroundBlurStyle(BlurStyle.Background)  // 前景模糊
```

---

## 动态属性设置（API 11+）

```typescript
// 通过AttributeModifier动态设置属性，支持if/else
Text('Dynamic')
  .attributeModifier(new MyModifier())
```

---

## 像素单位

| 单位 | 说明 |
|------|------|
| lpx | 设计稿逻辑像素（基准750lpx） |
| vp | 虚拟像素（自动适配设备密度） |
| fp | 字体像素（随系统字体大小变化） |

---

## 自定义组件

```typescript
@Component
struct MyCard {
  @Prop title: string
  @State expanded: boolean = false

  build() {
    Column() {
      Row() {
        Text(this.title)
          .fontSize(18)
          .fontWeight(FontWeight.Bold)
        if (this.expanded) {
          Text('详情内容...').fontSize(14)
        }
      }
      .onClick(() => {
        this.expanded = !this.expanded
      })
    }
    .padding(16)
    .backgroundColor('#F5F5F5')
    .borderRadius(8)
  }
}
```

---

## 路由导航

```typescript
import router from '@ohos.router'

// 跳转
router.pushUrl({ url: 'pages/Index', params: { id: 1 } })

// 返回
router.back()

// 替换
router.replaceUrl({ url: 'pages/Detail', params: { id: 2 } })
```
