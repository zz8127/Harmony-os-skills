# 鍥惧舰寮€鍙戯紙ArkGraphics 2D锛?
> **閫傜敤鐗堟湰**锛欻armonyOS 6.1 / API 23锛堢ǔ瀹氾級銆傚吋瀹?API 14+銆?
## 姒傝堪

ArkGraphics 2D 鎻愪緵 Canvas 缁樺埗銆佽嚜瀹氫箟娓叉煋銆佹ā绯婃晥鏋溿€佸姩鎬佸抚鐜囥€丏rawing 缁勪欢绛?2D 鍥惧舰鑳藉姏锛屾槸搴旂敤瀹炵幇鑷畾涔?UI 缁樺埗鍜岃瑙夋晥鏋滅殑鏍稿績宸ュ叿闆嗐€?
## Canvas 缁樺埗

### Canvas 鍩虹鐢ㄦ硶

```typescript
@Entry
@Component
struct CanvasPage {
  private settings: RenderingContextSettings = new RenderingContextSettings(true);
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings);

  build() {
    Column() {
      Canvas(this.context)
        .width('100%')
        .height(400)
        .onReady(() => {
          this.context.fillStyle = '#FF0000';
          this.context.fillRect(50, 50, 200, 100);

          this.context.strokeStyle = '#0000FF';
          this.context.lineWidth = 3;
          this.context.strokeRect(50, 200, 200, 100);
        })
    }
  }
}
```

### 璺緞缁樺埗

```typescript
this.context.beginPath();
this.context.moveTo(100, 100);
this.context.lineTo(200, 100);
this.context.lineTo(150, 50);
this.context.closePath();
this.context.fillStyle = '#00FF00';
this.context.fill();
this.context.stroke();
```

### 鍦嗗姬涓庤礉濉炲皵鏇茬嚎

```typescript
this.context.beginPath();
this.context.arc(150, 150, 80, 0, Math.PI * 2);
this.context.stroke();

this.context.beginPath();
this.context.moveTo(50, 300);
this.context.bezierCurveTo(100, 200, 200, 400, 250, 300);
this.context.stroke();

this.context.beginPath();
this.context.moveTo(50, 350);
this.context.quadraticCurveTo(150, 250, 250, 350);
this.context.stroke();
```

### 娓愬彉濉厖

```typescript
let linearGradient = this.context.createLinearGradient(0, 0, 300, 0);
linearGradient.addColorStop(0, '#FF0000');
linearGradient.addColorStop(0.5, '#00FF00');
linearGradient.addColorStop(1, '#0000FF');
this.context.fillStyle = linearGradient;
this.context.fillRect(0, 0, 300, 200);

let radialGradient = this.context.createRadialGradient(150, 150, 10, 150, 150, 100);
radialGradient.addColorStop(0, '#FFFFFF');
radialGradient.addColorStop(1, '#000000');
this.context.fillStyle = radialGradient;
this.context.fillRect(0, 200, 300, 200);
```

### 鏂囧瓧缁樺埗

```typescript
this.context.font = '30px sans-serif';
this.context.fillStyle = '#333333';
this.context.textAlign = 'center';
this.context.textBaseline = 'middle';
this.context.fillText('Hello HarmonyOS', 150, 150);

this.context.strokeStyle = '#FF0000';
this.context.strokeText('Outline Text', 150, 200);
```

### 鍥剧墖缁樺埗

```typescript
let img = new ImageBitmap('common/icon.png');

this.context.drawImage(img, 10, 10);
this.context.drawImage(img, 10, 10, 100, 100);
this.context.drawImage(img, 0, 0, 100, 100, 10, 10, 200, 200);
```

### 鍙樻崲鎿嶄綔

```typescript
this.context.save();

this.context.translate(150, 150);
this.context.rotate(Math.PI / 4);
this.context.scale(1.5, 1.5);

this.context.fillStyle = '#FF6600';
this.context.fillRect(-50, -50, 100, 100);

this.context.restore();
```

### 闃村奖鏁堟灉

```typescript
this.context.shadowBlur = 15;
this.context.shadowColor = '#000000';
this.context.shadowOffsetX = 5;
this.context.shadowOffsetY = 5;
this.context.fillStyle = '#FF9900';
this.context.fillRect(50, 50, 150, 100);
```

## 鑷畾涔夋覆鏌?
### 绂诲睆 Canvas

```typescript
let offscreen = new OffscreenCanvas(300, 300);
let offCtx = offscreen.getContext('2d');

offCtx.fillStyle = '#4488FF';
offCtx.fillRect(0, 0, 150, 150);

offCtx.fillStyle = '#FF8844';
offCtx.fillRect(150, 150, 150, 150);

let imageBitmap = offscreen.transferToImageBitmap();
this.context.drawImage(imageBitmap, 0, 0);
```

### 鍍忕礌鎿嶄綔

```typescript
let imageData = this.context.getImageData(0, 0, 100, 100);

for (let i = 0; i < imageData.data.length; i += 4) {
  imageData.data[i] = 255 - imageData.data[i];
  imageData.data[i + 1] = 255 - imageData.data[i + 1];
  imageData.data[i + 2] = 255 - imageData.data[i + 2];
}

this.context.putImageData(imageData, 0, 0);
```

## 妯＄硦鏁堟灉

### 鑳屾櫙妯＄硦

```typescript
@Entry
@Component
struct BlurPage {
  build() {
    Stack() {
      Image($r('app.media.background'))
        .width('100%')
        .height('100%')

      Column() {
        Text('Blur Effect')
          .fontSize(24)
          .fontColor(Color.White)
      }
      .width(200)
      .height(200)
      .backgroundColor('#80FFFFFF')
      .blur(20)
    }
  }
}
```

### 鍓嶆櫙妯＄硦

```typescript
Image($r('app.media.photo'))
  .width(300)
  .height(300)
  .blur(10, BlurType.THIN)
```

## 鍔ㄦ€佸抚鐜?
```typescript
import { display } from '@kit.ArkUI';

@Entry
@Component
struct FrameRatePage {
  build() {
    List() {
      ListItem() {
        Text('Dynamic Frame Rate Item')
      }
    }
    .frameRateRange({
      expected: 60,
      min: 30,
      max: 120
    })
  }
}
```

## Drawing 缁勪欢

### Shape 涓?Path

```typescript
@Entry
@Component
struct DrawingPage {
  build() {
    Column() {
      Shape() {
        Path()
          .commands('M100 0 L200 100 L0 100 Z')
          .fill(Color.Orange)
          .stroke(Color.Red)
          .strokeWidth(2)
      }
      .width(200)
      .height(200)
      .viewPort({ x: 0, y: 0, width: 200, height: 200 })

      Shape() {
        Circle({ width: 100, height: 100 })
          .fill(Color.Blue)
          .stroke(Color.White)
      }
      .width(120)
      .height(120)
    }
  }
}
```

### 鍩虹鍥惧舰缁勪欢

```typescript
Column() {
  Circle({ width: 80, height: 80 })
    .fill(Color.Red)

  Ellipse({ width: 120, height: 60 })
    .fill(Color.Green)

  Rect({ width: 100, height: 60 })
    .radius(10)
    .fill(Color.Blue)

  Line()
    .width(200)
    .height(2)
    .backgroundColor(Color.Black)

  Polyline()
    .points([[0, 0], [50, 50], [100, 0]])
    .fill(Color.Transparent)
    .stroke(Color.Purple)
    .strokeWidth(2)

  Polygon()
    .points([[50, 0], [100, 40], [80, 100], [20, 100], [0, 40]])
    .fill(Color.Yellow)
    .stroke(Color.Orange)
}
```

## 鏉冮檺

鏈?Kit 鏃犻渶鐗规畩鏉冮檺澹版槑銆?
---

## 瀹樻柟鍙傝€?
- Canvas 缁樺埗锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-canvas-V5
- Canvas API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-canvasrenderingcontext2d-V5
- Drawing 缁勪欢锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-graphics-drawing-V5
- 妯＄硦鏁堟灉锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-universal-attributes-blur-V5
- 鍔ㄦ€佸抚鐜囷細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-frame-rate-V5
- Shape 缁勪欢锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-drawing-components-shape-V5