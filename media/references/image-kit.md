# 图片处理（Image Kit）

> HarmonyOS 6.1 / API 23

## 概述

图片处理（Image Kit）提供图片解码、编码、像素操作、元数据读写和图片打包等能力，通过 `@kit.ImageKit` 引入。API 23 新增图片元数据读写、PixelMap 自动旋转等特性。

## ImageSource 创建

从文件、缓冲区或资源创建 ImageSource。

```typescript
import { image } from '@kit.ImageKit';
import { fileIo as fs } from '@kit.CoreFileKit';

async function createFromFile(filePath: string): Promise<image.ImageSource> {
  const file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
  const imageSource = image.createImageSource(file.fd);
  fs.closeSync(file);
  return imageSource;
}

async function createFromBuffer(buffer: ArrayBuffer): Promise<image.ImageSource> {
  return image.createImageSource(buffer);
}

async function createFromResource(): Promise<image.ImageSource> {
  return image.createImageSource($r('app.media.example'));
}
```

## PixelMap 操作

创建和操作像素图，包括缩放、旋转、裁剪、翻转等。

```typescript
import { image } from '@kit.ImageKit';

async function createPixelMap(imageSource: image.ImageSource): Promise<image.PixelMap> {
  const decodingOptions: image.DecodingOptions = {
    editable: true,
    desiredSize: { width: 200, height: 200 },
    desiredPixelFormat: image.PixelFormat.RGBA_8888
  };
  return imageSource.createPixelMap(decodingOptions);
}

async function manipulatePixelMap(pixelMap: image.PixelMap): Promise<void> {
  await pixelMap.scale(2.0, 2.0);
  await pixelMap.rotate(90);
  await pixelMap.translate(50, 50);
  await pixelMap.flip(true, false);
  await pixelMap.crop({ x: 0, y: 0, size: { width: 100, height: 100 } });
}

async function getPixelMapInfo(pixelMap: image.PixelMap): Promise<void> {
  const info = await pixelMap.getImageInfo();
  console.info(`宽: ${info.size.width}, 高: ${info.size.height}`);
  console.info(`像素格式: ${info.pixelFormat}`);
}

async function readWritePixels(pixelMap: image.PixelMap): Promise<void> {
  const region: image.Region = { x: 0, y: 0, size: { width: 10, height: 10 } };
  const data = new ArrayBuffer(10 * 10 * 4);
  await pixelMap.readPixels(area: region, data);
  await pixelMap.writePixels(area: region, data);
}
```

## 图片元数据读写（API 23）

API 23 新增图片元数据读取和修改接口，支持 EXIF 等元数据操作。

```typescript
import { image } from '@kit.ImageKit';

async function readImageMetadata(imageSource: image.ImageSource): Promise<void> {
  const metadata = await imageSource.readImageMetadata();
  console.info(`EXIF 方向: ${metadata.orientation}`);
  console.info(`拍摄时间: ${metadata.dateTimeOriginal}`);
  console.info(`ISO: ${metadata.isoSpeedRatings}`);
  console.info(`曝光时间: ${metadata.exposureTime}`);
}

async function modifyImageMetadata(imageSource: image.ImageSource): Promise<void> {
  const metadata: image.ImageMetadata = {
    orientation: '1',
    imageWidth: '1920',
    imageHeight: '1080'
  };
  await imageSource.modifyImageMetadata(metadata);
}
```

## PixelMap 自动旋转（API 23）

API 23 新增从 Surface 创建 PixelMap 时支持自动旋转，根据 EXIF 方向信息自动调整。

```typescript
import { image } from '@kit.ImageKit';

async function createPixelMapWithTransformation(surfaceId: string): Promise<image.PixelMap> {
  const options: image.PixelMapFromSurfaceOptions = {
    surfaceId: surfaceId,
    autoRotate: true
  };
  return image.createPixelMapFromSurfaceWithTransformation(options);
}
```

## 图片打包

将 PixelMap 或 ImageSource 打包为指定格式的数据。

```typescript
import { image } from '@kit.ImageKit';

async function packToData(pixelMap: image.PixelMap): Promise<ArrayBuffer> {
  const packer = image.createImagePacker();
  const packOptions: image.PackingOption = {
    format: 'image/jpeg',
    quality: 90
  };
  const data = await packer.packing(pixelMap, packOptions);
  await packer.release();
  return data;
}

async function packToFile(pixelMap: image.PixelMap, filePath: string): Promise<void> {
  const packer = image.createImagePacker();
  const packOptions: image.PackingOption = {
    format: 'image/png',
    quality: 100
  };
  const file = fs.openSync(filePath, fs.OpenMode.CREATE | fs.OpenMode.WRITE_ONLY);
  await packer.packToFile(pixelMap, file.fd, packOptions);
  fs.closeSync(file);
  await packer.release();
}
```

## 支持格式

| 格式 | 解码 | 编码 |
|------|------|------|
| JPEG | ✅ | ✅ |
| PNG | ✅ | ✅ |
| GIF | ✅ | ❌ |
| BMP | ✅ | ✅ |
| WebP | ✅ | ✅ |
| HEIF | ✅ | ✅ |
| SVG | ✅ | ❌ |

## 权限

| 权限 | 说明 |
|------|------|
| 无特殊权限 | 图片处理本身无需额外权限 |

访问文件时需要对应文件读写权限。

## 官方参考

- [Image Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/image-overview-0000001774121218)
- [Image Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/image-0000001774121214)
