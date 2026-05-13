# 扫码服务（Scan Kit）

> HarmonyOS 6.1 / API 23

## 概述

扫码服务（Scan Kit）提供条形码和二维码的扫描与生成能力，通过 `@kit.ScanKit` 引入。支持默认 UI 扫码、自定义 UI 扫码、图片识码三种模式。API 23 新增穿戴设备扫码支持。

## 默认 UI 扫码

使用系统默认扫码界面，一行代码即可完成扫码。

```typescript
import { scanBarcode, scanCore } from '@kit.ScanKit';
import { BusinessError } from '@kit.BasicServicesKit';

async function startDefaultScan(context: Context): Promise<void> {
  try {
    const options: scanBarcode.ScanOptions = {
      scanTypes: [scanCore.ScanType.QR_CODE, scanCore.ScanType.BAR_CODE],
      enableMultiMode: true,
      enableAlbum: true
    };
    const result: scanBarcode.ScanResult = await scanBarcode.startScanForResult(context, options);
    console.info(`原始值: ${result.originalValue}`);
    console.info(`码格式: ${result.scanType}`);
  } catch (error) {
    const e = error as BusinessError;
    console.error(`扫码失败: ${e.code} - ${e.message}`);
  }
}
```

## 自定义 UI 扫码

使用 ScanComponent 嵌入自定义页面，灵活控制扫码界面布局。

```typescript
import { scanCore, scanBarcode } from '@kit.ScanKit';

@Entry
@Component
struct CustomScanPage {
  private scanComponent?: scanBarcode.ScanComponent;
  private context: Context = getContext(this);

  build() {
    Column() {
      ScanComponent({
        controller: this.getScanController()
      })
        .width('100%')
        .height(500)
        .onLightClick(() => {
          this.scanComponent?.openLight();
        })
        .onCloseClick(() => {
          this.scanComponent?.closeLight();
        })

      Row() {
        Button('相册选图')
          .onClick(() => {
            this.scanFromAlbum();
          })
        Button('开灯')
          .onClick(() => {
            this.scanComponent?.openLight();
          })
      }
      .margin({ top: 20 })
    }
  }

  private getScanController(): scanBarcode.ScanComponentController {
    const controller = new scanBarcode.ScanComponentController();
    controller.on('scanResult', (result: Array<scanBarcode.ScanResult>) => {
      if (result.length > 0) {
        console.info(`扫码结果: ${result[0].originalValue}`);
      }
    });
    return controller;
  }

  private async scanFromAlbum(): Promise<void> {
    const options: scanBarcode.ScanOptions = {
      scanTypes: [scanCore.ScanType.QR_CODE],
      enableMultiMode: false,
      enableAlbum: true
    };
    const result = await scanBarcode.startScanForResult(this.context, options);
    console.info(`相册扫码: ${result.originalValue}`);
  }
}
```

## 图片识码

对静态图片进行码识别，无需摄像头。

```typescript
import { scanCore } from '@kit.ScanKit';
import { image } from '@kit.ImageKit';

async function decodeFromImage(pixelMap: image.PixelMap): Promise<string> {
  const options: scanCore.DecodeOptions = {
    scanTypes: [scanCore.ScanType.QR_CODE, scanCore.ScanType.BAR_CODE],
    enableMultiMode: true
  };
  const result: scanCore.DecodeResult = await scanCore.decode(pixelMap, options);
  return result.originalValue;
}

async function decodeFromImageSource(imageSource: image.ImageSource): Promise<string> {
  const pixelMap = await imageSource.createPixelMap();
  return decodeFromImage(pixelMap);
}
```

## 穿戴设备扫码（API 23）

API 23 新增穿戴设备扫码支持，适配小屏幕交互。

```typescript
import { scanBarcode, scanCore } from '@kit.ScanKit';

async function startWearableScan(context: Context): Promise<void> {
  const options: scanBarcode.ScanOptions = {
    scanTypes: [scanCore.ScanType.QR_CODE],
    enableMultiMode: false,
    enableAlbum: false
  };
  const result: scanBarcode.ScanResult = await scanBarcode.startScanForResult(context, options);
  console.info(`穿戴设备扫码结果: ${result.originalValue}`);
}
```

## 权限

| 权限 | 说明 |
|------|------|
| `ohos.permission.CAMERA` | 摄像头权限（扫码必需） |

在 `module.json5` 中声明：

```json
{
  "requestPermissions": [
    { "name": "ohos.permission.CAMERA" }
  ]
}
```

## 官方参考

- [Scan Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/scan-kit-overview-0000001774121558)
- [Scan Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/scan-barcode-0000001774280606)
