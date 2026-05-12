# 相册访问（PhotoAccessHelper）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）。兼容 API 14+。

## 概述

PhotoAccessHelper 用于访问和管理设备相册中的图片/视频资源。

## 权限申请

```json
"requestPermissions": [
  { "name": "ohos.permission.READ_MEDIA_IMAGES" },
  { "name": "ohos.permission.READ_MEDIA_VIDEO" },
  { "name": "ohos.permission.WRITE_MEDIA_IMAGES" }
]
```

## 查询相册资源

```typescript
import { photoAccessHelper } from '@kit.MediaLibraryKit';

let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

// 查询所有图片
let fetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: ['uri', 'display_name', 'size', 'date_added'],
  predicates: photoAccessHelper.MediaFetchOptions.create({
    selections: photoAccessHelper.MediaFetchOptions.createSelectionArgs(),
    selectionArgs: [],
    order: 'date_added DESC',
    limit: 20,
    offset: 0
  })
};

let fetchResult = await phAccessHelper.getAssets(fetchOptions);
let count = fetchResult.getCount();

// 遍历结果
while (fetchResult.isAfterLast() === false) {
  let asset = fetchResult.getNextObject();
  console.info('Asset: ' + asset.uri + ', Name: ' + asset.displayName);
  fetchResult.close();
}
```

## 创建相册

```typescript
// 创建用户相册
let albumName = 'MyAlbum';
let album = await phAccessHelper.createAlbum(albumName);
console.info('Created album: ' + album.albumName);
```

## 保存图片

```typescript
import { fileIo } from '@kit.CoreFileKit';

let file = fileIo.openSync('/path/to/image.jpg', fileIo.OpenMode.READ_ONLY);
let createOptions: photoAccessHelper.CreateOptions = {
  title: 'my_photo',
  displayName: 'my_photo.jpg'
};
let assetUri = await phAccessHelper.createAsset(
  photoAccessHelper.MediaType.IMAGE,
  createOptions,
  file
);
fileIo.closeSync(file);
```

## 官方参考

- MediaLibraryKit：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/photoaccesshelper-overview-V5
