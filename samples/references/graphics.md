# 图形开发示例（Graphics）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## Canvas 2D 绘图（ArkGraphics 2D）

```typescript
import drawing from '@ohos.graphics.drawing';

// 在 XComponent 上绘制
@Entry
@Component
struct CanvasExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true);
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings);

  build() {
    XComponentController.create()
    XComponent({ type: 'texture', id: 'canvas' })
      .onLoad((ctx) => {
        // ctx 是 XComponent 的 native Canvas
      })
    Canvas(this.context)
      .width(300)
      .height(300)
      .onReady(() => {
        // 绘制矩形
        this.context.fillStyle = '#007DFF';
        this.context.fillRect(10, 10, 200, 100);

        // 绘制圆形
        this.context.beginPath();
        this.context.arc(100, 50, 30, 0, Math.PI * 2);
        this.context.fillStyle = '#36D1A1';
        this.context.fill();

        // 绘制文本
        this.context.font = '24px HarmonyOS Sans';
        this.context.fillStyle = '#000000';
        this.context.fillText('Hello HarmonyOS', 10, 80);
      })
  }
}
```

## 模糊效果（API 14+）

```typescript
import drawing from '@ohos.graphics.drawing';

// 使用 BlurStyle
let brush = new drawing.Brush();
brush.setColor(0x80007DFF);
brush.setBlurStyle(BlurStyle.NORMAL, 10); // 模糊半径 10
// 配合 RenderNode 使用实现背景模糊
```

## 可变帧率（DisplaySync）

```typescript
import displaySync from '@kit.ArkGraphics2D';

// 创建可变帧率控制器
let displaySyncScene = displaySync.createDisplaySyncScene();

// 设置期望帧率
displaySyncScene.setTargetFrameRateRange({
  min: 30,
  max: 120,
  expected: 60
});

// 开始同步
displaySyncScene.start();

// 停止
displaySyncScene.stop();
```

## 自定义渲染（FrameNode/RenderNode）

```typescript
import { FrameNode, RenderNode, DrawingColor } from '@kit.ArkUI';

// 创建自定义渲染节点
let rootNode = new FrameNode(getContext());
let renderNode = new RenderNode();

// 设置几何信息
renderNode.setPosition(100, 100, 200, 200);

// 设置背景
renderNode.setBackgroundColor(0xFF007DFF);

// 添加到根节点
rootNode.appendChild(renderNode);

// 在 ArkUI 中渲染自定义节点
XComponent({ type: 'node', content: rootNode })
```

## 官方参考

- ArkGraphics 2D 概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkgraphics-2d
- Canvas 开发：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/canvas-2d
- 模糊效果：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/graphics-blur
- DisplaySync：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/displaysync-guide
