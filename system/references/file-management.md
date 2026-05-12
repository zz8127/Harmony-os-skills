# 文件管理（Core File Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

Core File Kit（`@kit.CoreFileKit`）提供应用文件管理能力，包括：

- **应用沙箱**：每个应用拥有独立的文件沙箱目录，应用间文件隔离
- **文件读写**：通过 `fs` 模块进行文件打开、读写、复制、移动、删除等操作
- **文件选择器（FilePicker）**：通过系统 Picker 让用户选择照片、文档、音频等文件
- **Rawfile 访问**：读取应用资源目录下的 rawfile 文件

---

## 应用沙箱

### 沙箱目录结构

```
/data/storage/el2/base/
├── files/          # 持久化文件目录（应用卸载后清除）
├── cache/          # 缓存目录（系统空间不足时可能被清理）
├── temp/           # 临时文件目录（应用退出后可能被清理）
├── preferences/    # 偏好设置目录
└── distributedFiles/  # 分布式文件目录（跨设备同步）
```

### 获取沙箱路径

```typescript
import { UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';

export default class EntryAbility extends UIAbility {
  onCreate() {
    let filesDir = this.context.filesDir;
    let cacheDir = this.context.cacheDir;
    let tempDir = this.context.tempDir;
    let distributedFilesDir = this.context.distributedFilesDir;
    let preferencesDir = this.context.preferencesDir;
    let databaseDir = this.context.databaseDir;
    let bundleCodeDir = this.context.bundleCodeDir;
  }
}
```

### 在 UI 中获取 Context

```typescript
import { common } from '@kit.AbilityKit';

@Entry
@Component
struct FilePage {
  private context = getContext(this) as common.UIAbilityContext;

  build() {
    Column() {
      Button('获取文件路径').onClick(() => {
        console.info('filesDir: ' + this.context.filesDir);
        console.info('cacheDir: ' + this.context.cacheDir);
      })
    }
  }
}
```

---

## 文件读写

### 打开与关闭文件

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';

let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);

fs.closeSync(file);
```

### 写入文件

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';
let file = fs.openSync(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);

let writeLen = fs.writeSync(file.fd, 'Hello HarmonyOS');
console.info('写入长度: ' + writeLen);

fs.closeSync(file);
```

### 读取文件

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';
let file = fs.openSync(filePath, fs.OpenMode.READ_ONLY);

let buf = new ArrayBuffer(4096);
let readLen = fs.readSync(file.fd, buf);
let content = String.fromCharCode(...new Uint8Array(buf.slice(0, readLen)));
console.info('读取内容: ' + content);

fs.closeSync(file);
```

### 文件信息与判断

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';

let stat = fs.statSync(filePath);
console.info('文件大小: ' + stat.size);
console.info('是否目录: ' + stat.isDirectory());
console.info('是否文件: ' + stat.isFile());
console.info('修改时间: ' + stat.mtime);

let isExist = fs.accessSync(filePath);
console.info('文件是否存在: ' + isExist);
```

### 创建与删除目录

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let dirPath = this.context.filesDir + '/myDir';

fs.mkdirSync(dirPath);

fs.rmdirSync(dirPath);
```

### 复制与移动文件

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let srcPath = this.context.filesDir + '/test.txt';
let dstPath = this.context.filesDir + '/test_copy.txt';

fs.copyFileSync(srcPath, dstPath);

let movePath = this.context.filesDir + '/test_moved.txt';
fs.moveFileSync(srcPath, movePath);
```

### 删除文件

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';

fs.unlinkSync(filePath);
```

### 列出目录内容

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let dirPath = this.context.filesDir;

let list = fs.listFileSync(dirPath);
for (let i = 0; i < list.length; i++) {
  console.info('文件: ' + list[i]);
}
```

### 异步操作（推荐）

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';

let filePath = this.context.filesDir + '/test.txt';

try {
  let file = await fs.open(filePath, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  let writeLen = await fs.write(file.fd, 'Hello HarmonyOS Async');
  console.info('写入长度: ' + writeLen);
  await fs.close(file);
} catch (err) {
  console.error('文件操作失败: ' + JSON.stringify(err));
}
```

---

## 文件选择器（FilePicker）

FilePicker 通过系统 UI 让用户选择文件，应用无需申请敏感权限。

### PhotoViewPicker（选择照片/视频）

```typescript
import { picker } from '@kit.CoreFileKit';

let photoSelectOptions = new picker.PhotoSelectOptions();
photoSelectOptions.MIMEType = picker.PhotoViewMIMETypes.IMAGE_TYPE;
photoSelectOptions.maxSelectNumber = 5;

let photoViewPicker = new picker.PhotoViewPicker();

photoViewPicker.select(photoSelectOptions).then((result: picker.PhotoSelectResult) => {
  let uris: Array<string> = result.photoUris;
  for (let i = 0; i < uris.length; i++) {
    console.info('照片 URI: ' + uris[i]);
  }
}).catch((err: BusinessError) => {
  console.error('选择照片失败: ' + err.message);
});
```

### DocumentViewPicker（选择文档）

```typescript
import { picker } from '@kit.CoreFileKit';

let documentSelectOptions = new picker.DocumentSelectOptions();
documentSelectOptions.maxSelectNumber = 3;

let documentViewPicker = new picker.DocumentViewPicker();

documentViewPicker.select(documentSelectOptions).then((result: Array<string>) => {
  for (let i = 0; i < result.length; i++) {
    console.info('文档 URI: ' + result[i]);
  }
}).catch((err: BusinessError) => {
  console.error('选择文档失败: ' + err.message);
});
```

### AudioViewPicker（选择音频）

```typescript
import { picker } from '@kit.CoreFileKit';

let audioSelectOptions = new picker.AudioSelectOptions();
audioSelectOptions.maxSelectNumber = 5;

let audioViewPicker = new picker.AudioViewPicker();

audioViewPicker.select(audioSelectOptions).then((result: Array<string>) => {
  for (let i = 0; i < result.length; i++) {
    console.info('音频 URI: ' + result[i]);
  }
}).catch((err: BusinessError) => {
  console.error('选择音频失败: ' + err.message);
});
```

### 保存文件（PhotoViewPicker save）

```typescript
import { picker } from '@kit.CoreFileKit';

let photoSaveOptions = new picker.PhotoSaveOptions();
photoSaveOptions.newFileNames = ['saved_image.jpg'];

let photoViewPicker = new picker.PhotoViewPicker();

photoViewPicker.save(photoSaveOptions).then((result: Array<string>) => {
  console.info('保存路径 URI: ' + result[0]);
}).catch((err: BusinessError) => {
  console.error('保存失败: ' + err.message);
});
```

### 保存文件（DocumentViewPicker save）

```typescript
import { picker } from '@kit.CoreFileKit';

let documentSaveOptions = new picker.DocumentSaveOptions();
documentSaveOptions.newFileNames = ['saved_doc.txt'];

let documentViewPicker = new picker.DocumentViewPicker();

documentViewPicker.save(documentSaveOptions).then((result: Array<string>) => {
  console.info('保存路径 URI: ' + result[0]);
}).catch((err: BusinessError) => {
  console.error('保存失败: ' + err.message);
});
```

### 持久化 URI 授权

Picker 返回的 URI 默认仅本次有效。如需跨会话访问，须通过 `grantUriPermission` 持久化授权。

```typescript
import { picker } from '@kit.CoreFileKit';
import { fileUri } from '@kit.CoreFileKit';

let photoSelectOptions = new picker.PhotoSelectOptions();
photoSelectOptions.MIMEType = picker.PhotoViewMIMETypes.IMAGE_TYPE;
photoSelectOptions.maxSelectNumber = 1;

let photoViewPicker = new picker.PhotoViewPicker();

photoViewPicker.select(photoSelectOptions).then(async (result: picker.PhotoSelectResult) => {
  let uri = result.photoUris[0];
  let uriObj = new fileUri.FileUri(uri);
  let mode = 'r';
  await picker.grantUriPermission(uriObj, mode);
  console.info('持久化授权成功: ' + uri);
}).catch((err: BusinessError) => {
  console.error('授权失败: ' + err.message);
});
```

---

## 用户文件访问

通过 Picker 获取的 URI 可直接用于 `fs.openSync` 读取用户文件。

```typescript
import { fileIo as fs } from '@kit.CoreFileKit';
import { picker } from '@kit.CoreFileKit';

let documentSelectOptions = new picker.DocumentSelectOptions();
let documentViewPicker = new picker.DocumentViewPicker();

documentViewPicker.select(documentSelectOptions).then((uris: Array<string>) => {
  let file = fs.openSync(uris[0], fs.OpenMode.READ_ONLY);
  let buf = new ArrayBuffer(4096);
  let readLen = fs.readSync(file.fd, buf);
  let content = String.fromCharCode(...new Uint8Array(buf.slice(0, readLen)));
  console.info('文件内容: ' + content);
  fs.closeSync(file);
}).catch((err: BusinessError) => {
  console.error('读取用户文件失败: ' + err.message);
});
```

---

## Rawfile 访问

Rawfile 是放置在 `resources/rawfile/` 目录下的原始资源文件，通过 `resourceManager` 读取。

### 读取 Rawfile 内容

```typescript
import { resourceManager } from '@kit.LocalizationKit';

try {
  let resMgr = getContext(this).resourceManager;
  let content = await resMgr.getRawFileContent('config.json');
  let text = String.fromCharCode(...new Uint8Array(content.buffer));
  console.info('Rawfile 内容: ' + text);
} catch (err) {
  console.error('读取 Rawfile 失败: ' + JSON.stringify(err));
}
```

### 读取 Rawfile 为 String

```typescript
import { resourceManager } from '@kit.LocalizationKit';

try {
  let resMgr = getContext(this).resourceManager;
  let text = await resMgr.getRawFileContentStr('config.json');
  console.info('Rawfile 文本: ' + text);
} catch (err) {
  console.error('读取 Rawfile 失败: ' + JSON.stringify(err));
}
```

### 列出 Rawfile 目录

```typescript
import { resourceManager } from '@kit.LocalizationKit';

try {
  let resMgr = getContext(this).resourceManager;
  let fileList = await resMgr.getRawFileList('subdir');
  for (let i = 0; i < fileList.length; i++) {
    console.info('Rawfile: ' + fileList[i]);
  }
} catch (err) {
  console.error('列出 Rawfile 失败: ' + JSON.stringify(err));
}
```

---

## 权限

### 基础文件操作

沙箱内文件读写无需权限声明。

### 用户文件访问权限

通过 FilePicker 选择文件无需权限。直接访问公共目录需要以下权限：

```json
"requestPermissions": [
  {
    "name": "ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY",
    "reason": "$string:download_dir_reason",
    "usedScene": {
      "abilities": ["EntryAbility"],
      "when": "inuse"
    }
  },
  {
    "name": "ohos.permission.READ_WRITE_DESKTOP_DIRECTORY",
    "reason": "$string:desktop_dir_reason",
    "usedScene": {
      "abilities": ["EntryAbility"],
      "when": "inuse"
    }
  },
  {
    "name": "ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY",
    "reason": "$string:documents_dir_reason",
    "usedScene": {
      "abilities": ["EntryAbility"],
      "when": "inuse"
    }
  }
]
```

### 权限说明

| 权限 | 说明 | 授权方式 |
|------|------|---------|
| `READ_WRITE_DOWNLOAD_DIRECTORY` | 读写下载目录 | user_grant |
| `READ_WRITE_DESKTOP_DIRECTORY` | 读写桌面目录 | user_grant |
| `READ_WRITE_DOCUMENTS_DIRECTORY` | 读写文档目录 | user_grant |

> **推荐**：优先使用 FilePicker，无需申请权限，用户体验更好。

---

## 官方参考

- 文件管理概述：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-management-overview-V5
- 应用沙箱目录：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/app-sandbox-directory-V5
- 文件基础操作：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-management-V5
- FilePicker：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/file-picker-V5
- Rawfile 资源：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/rawfile-guidelines-V5
- fileIo API 参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-fileio-V5
