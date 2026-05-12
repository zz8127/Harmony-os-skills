# ArkUI 组件库速查

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/arkui/arkui-arkts/arkts-components-overview

## 组件总览

HarmonyOS ArkUI 提供 **80+** 标准化组件，开发者可直接使用。

---

## 基础组件

### Text

```typescript
Text('Hello HarmonyOS')
  .fontSize(16)
  .fontFamily('HarmonyOS Sans')
  .fontWeight(FontWeight.Medium)
  .fontColor('#182431')
  .textAlign(TextAlign.Center)
  .maxLines(2)
  .textOverflow(TextOverflow.Ellipsis)
```

### Button

```typescript
Button('点击', { type: ButtonType.Normal, stateEffect: true })
  .fontSize(16)
  .width(200)
  .height(40)
  .onClick(() => {
    console.info('点击了按钮');
  })

// ButtonType: Normal / Circle / Capsule
```

### Image

```typescript
Image('https://example.com/image.png')
  .width('100%')
  .height(200)
  .objectFit(ImageFit.Cover)
  .borderRadius(8)
  .alt($r('app.media.placeholder'))
```

### Span（行内文本）

```typescript
Text() {
  Span('纯文本')
    .fontColor(Color.Blue)
  Span('可点击')
    .fontColor(Color.Red)
    .onClick(() => {})
}
```

---

## 容器组件

### Column / Row / Stack

```typescript
// Column - 垂直排列
Column({ space: 12 }) {
  Text('Item 1')
  Text('Item 2')
}
.width('100%')
.alignItems(HorizontalAlign.Center)

Row({ space: 8 }) { /* 水平排列 */ }
Stack({ alignContent: Alignment.BottomEnd }) { /* 层叠 */ }
```

### List

```typescript
List({ space: 10, initialIndex: 0 }) {
  ListItem() {
    Text('列表项 1')
  }
  ListItem() {
    Text('列表项 2')
  }
}
.width('100%')
.height(300)
.listDirection(Axis.Vertical)
```

### Grid

```typescript
Grid() {
  GridItem() { Text('1') }
  GridItem() { Text('2') }
  GridItem() { Text('3') }
}
.columnsTemplate('1fr 1fr 1fr')
.rowsTemplate('1fr 1fr')
.width('100%')
.height(300)
```

### Tabs

```typescript
Tabs({ barPosition: BarPosition.End }) {
  TabContent() { Text('首页内容') }.tabBar('首页')
  TabContent() { Text('分类') }.tabBar('分类')
  TabContent() { Text('购物车') }.tabBar('购物车')
}
.width('100%')
.height('100%')
```

### HdsTabs — 悬浮标签页 + 迷你栏（API 23 新增）

`HdsTabs`（`@kit.UIDesignKit`）是增强版底部标签组件，支持悬浮样式和可折叠迷你栏：

```typescript
import { HdsTabs, HdsTabsController } from '@kit.UIDesignKit';

HdsTabs({
  controller: this.hdsTabsController,
  barFloatingStyle: {
    barOverlap: true,      // 悬浮在内容之上
    vertical: false,
    barPosition: BarPosition.End,
    miniBar: { expanded: false }  // 可折叠迷你栏
  }
}) {
  TabContent() { Text('首页') }.tabBar('首页')
  TabContent() { Text('发现') }.tabBar('发现')
  TabContent() { Text('我的') }.tabBar('我的')
}
.width('100%')
.height('100%')

// 切换迷你栏展开/折叠状态
this.hdsTabsController.setBarFloatingMiniBarExpanded(true);
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-bar-floating

---

## 媒体组件

### Video

```typescript
Video({
  src: 'https://example.com/video.mp4',
  currentProgressRate: PlaybackRate.Speed_Forward_1_00,
  controller: this.videoController
})
  .width('100%')
  .height(300)
  .autoPlay(false)
  .muted(false)
  .onPrepared((e) => { console.info('准备完成') })
  .onFinish(() => { console.info('播放结束') })
```

### XComponent（游戏/相机/Canvas）

```typescript
XComponent({
  id: 'canvas',
  type: 'texture',  // texture / surface / node
  controller: this.xComponentController
})
  .width('100%')
  .height('100%')
```

---

## 弹窗组件

### AlertDialog

```typescript
AlertDialog.show({
  title: '提示',
  message: '确定要删除吗？',
  autoCancel: true,
  primaryButton: {
    value: '取消',
    action: () => { console.info('取消') }
  },
  secondaryButton: {
    value: '确定',
    action: () => { console.info('确定') }
  }
})
```

### ActionSheet

```typescript
ActionSheet.show({
  title: '选择操作',
  message: '请选择',
  buttons: [
    { text: '拍照', color: '#182431' },
    { text: '相册', color: '#182431' },
    { text: '取消', color: '#99182431' }
  ],
  cancel: () => { console.info('取消') }
})
```

### CustomDialog

```typescript
// 定义
@CustomDialog
struct MyDialog {
  controller: CustomDialogController
  build() {
    Column() {
      Text('自定义弹窗')
        .fontSize(20)
      Button('关闭')
        .onClick(() => this.controller.close())
    }
    .padding(20)
  }
}

// 使用
let dialogController = new CustomDialogController({
  builder: MyDialog()
});
dialogController.open();
```

---

## 导航组件

### Navigation

```typescript
Navigation() {
  List() {
    ListItem() { Text('页面1') }
    ListItem() { Text('页面2') }
  }
}
.title('主标题')
.titleMode(NavigationTitleMode.Mini)
.backButtonVisible(true)
.mode(NavigationMode.Stack)
```

### Router（页面路由）

```typescript
import router from '@ohos.router';

// 跳转
router.pushUrl({ url: 'pages/Detail', params: { id: 1 } });

// 返回
router.pop();

// 获取参数
let params = router.getParams() as Record<string, number>;
```

---

## 绘图组件

### Circle / Rect / Shape

```typescript
Circle({ width: 100, height: 100 })
  .fill('#007DFF')
  .stroke('#003BB3')
  .strokeWidth(2)

Rect({ width: 200, height: 100 })
  .radius(8)
  .fill('#99CCFF')

Shape() {
  Path().commands('M0 0 L100 100 L100 0 Z')
    .fill('#36D1A1')
}
```

---

## 表单组件

### TextInput / TextArea

```typescript
TextInput({ placeholder: '请输入账号' })
  .type(InputType.Number)
  .maxLength(11)
  .onChange((value: string) => {
    console.info('输入：' + value);
  })

TextArea({ placeholder: '请输入备注' })
  .height(100)
  .showCount(true)
```

### Checkbox / Radio / Toggle

```typescript
Checkbox({ name: 'agree' })
  .select(false)
  .onChange((value: boolean) => {
    console.info('选中：' + value);
  })

Radio({ value: 'male', group: 'gender' })
  .onChange((isChecked: boolean) => {})

Toggle({ type: ToggleType.Switch, isOn: false })
  .onChange((isOn: boolean) => {})
```

### Slider

```typescript
Slider({
  value: 30,
  min: 0,
  max: 100,
  step: 1,
  style: SliderStyle.OutSet
})
  .showTips(true)
  .onChange((value: number) => {
    console.info('滑块值：' + value);
  })
```

---

## 组件使用注意事项

- 所有组件均需在 `@Component` 装饰器下使用
- ArkTS 推荐使用 `.` 链式调用配置属性
- 尺寸单位默认 vp，无需写 px
- 图片/媒体资源放在 `resources/` 目录下
- 组件状态使用 `@State` / `@Link` / `@Prop` 管理

---

## 官方参考

- ArkUI 组件总览：https://developer.huawei.com/consumer/cn/doc/arkui/arkts-arkui-arkts-components-overview
- 组件设计规范：https://developer.huawei.com/consumer/cn/design/
