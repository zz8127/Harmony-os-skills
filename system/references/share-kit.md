# 分享服务（Share Kit）

> HarmonyOS 6.1 / API 23

## 概述

分享服务（Share Kit）提供系统级分享面板和跨应用数据分享能力，通过 `@kit.ShareKit` 引入。支持文本、图片、文件等多种数据类型分享，API 23 新增读取扩展分享记录数据能力。

## 系统分享面板

调用系统分享面板，将数据分享到其他应用。

```typescript
import { systemShare, shareCore } from '@kit.ShareKit';
import { fileUri } from '@kit.CoreFileKit';
import { BusinessError } from '@kit.BasicServicesKit';

async function shareText(context: Context): Promise<void> {
  const shareData = new systemShare.ShareData({
    text: '分享文本内容',
    plainText: '纯文本内容'
  });

  const controller = new systemShare.ShareController(shareData);
  const options: systemShare.ShareOptions = {
    previewMode: systemShare.SharePreviewMode.DETAIL,
    selectionMode: systemShare.ShareSelectionMode.SINGLE
  };

  controller.show(context, options);
}
```

## 分享图片与文件

分享图片或文件类型数据。

```typescript
import { systemShare, shareCore } from '@kit.ShareKit';

async function shareImage(context: Context, imageUri: string): Promise<void> {
  const shareData = new systemShare.ShareData({
    plainText: '分享图片',
    contentInfo: {
      mimeType: 'image/jpeg',
      filePath: imageUri
    }
  });

  const controller = new systemShare.ShareController(shareData);
  controller.show(context, {
    previewMode: systemShare.SharePreviewMode.DETAIL
  });
}

async function shareFile(context: Context, fileUri: string, mimeType: string): Promise<void> {
  const shareData = new systemShare.ShareData({
    contentInfo: {
      mimeType: mimeType,
      filePath: fileUri
    }
  });

  const controller = new systemShare.ShareController(shareData);
  controller.show(context);
}
```

## 分享多类型数据

同时分享文本和附件。

```typescript
import { systemShare, shareCore } from '@kit.ShareKit';

async function shareMultiple(context: Context): Promise<void> {
  const shareData = new systemShare.ShareData({
    plainText: '多类型分享',
    contentInfo: {
      mimeType: 'text/plain',
      filePath: '/data/share/example.txt'
    }
  });

  const controller = new systemShare.ShareController(shareData);
  controller.show(context, {
    previewMode: systemShare.SharePreviewMode.DEFAULT,
    selectionMode: systemShare.ShareSelectionMode.MULTIPLE
  });
}
```

## 读取扩展分享记录（API 23）

API 23 新增读取分享记录数据接口，可获取其他应用分享过来的数据。

```typescript
import { shareCore } from '@kit.ShareKit';

async function readSharedData(shareRecordId: string): Promise<void> {
  const recordData = await shareCore.readingExtendedShareRecordData(shareRecordId);
  console.info(`分享记录数据: ${recordData}`);
}
```

## 分享到指定应用

通过指定目标应用包名实现定向分享。

```typescript
import { systemShare, shareCore } from '@kit.ShareKit';

async function shareToSpecificApp(context: Context, targetBundle: string): Promise<void> {
  const shareData = new systemShare.ShareData({
    plainText: '定向分享内容'
  });

  const controller = new systemShare.ShareController(shareData);
  controller.show(context, {
    targetBundleName: targetBundle
  });
}
```

## 权限

分享服务通常不需要额外权限，但访问文件数据时需要对应文件读取权限。

| 权限 | 说明 |
|------|------|
| 无特殊权限 | 系统分享面板无需额外权限 |

## 官方参考

- [Share Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/share-kit-overview-0000001774280634)
- [Share Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/share-systemshare-0000001821001513)
