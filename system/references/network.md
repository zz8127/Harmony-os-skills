# 网络开发

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

NetworkKit（@kit.NetworkKit）提供 HTTP 请求、RCP 远程通信、WebSocket 长连接、网络状态监听、文件上传下载等能力，覆盖应用层网络通信全场景。

## HTTP 请求

基于 @ohos.net.http 模块，支持 GET/POST 等常见方法、自定义请求头与超时配置。

### GET 请求

```typescript
import { http } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let httpRequest = http.createHttp();

httpRequest.request('https://example.com/api/data', {
  method: http.RequestMethod.GET,
  header: { 'Content-Type': 'application/json' },
  connectTimeout: 60000,
  readTimeout: 60000
}, (err: BusinessError, data: http.HttpResponse) => {
  if (err) {
    console.error('Request failed: ' + err.message);
    return;
  }
  console.info('Status: ' + data.responseCode);
  console.info('Body: ' + data.result);
  httpRequest.destroy();
});
```

### POST 请求

```typescript
import { http } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let httpRequest = http.createHttp();

httpRequest.request('https://example.com/api/submit', {
  method: http.RequestMethod.POST,
  header: { 'Content-Type': 'application/json' },
  extraData: { name: 'test', value: 42 },
  connectTimeout: 60000,
  readTimeout: 60000
}, (err: BusinessError, data: http.HttpResponse) => {
  if (err) {
    console.error('Request failed: ' + err.message);
    return;
  }
  console.info('Status: ' + data.responseCode);
  console.info('Body: ' + data.result);
  httpRequest.destroy();
});
```

### Promise 风格

```typescript
import { http } from '@kit.NetworkKit';

let httpRequest = http.createHttp();

httpRequest.request('https://example.com/api/data', {
  method: http.RequestMethod.GET,
  connectTimeout: 60000,
  readTimeout: 60000
}).then((data: http.HttpResponse) => {
  console.info('Status: ' + data.responseCode);
  console.info('Body: ' + data.result);
}).catch((err: Error) => {
  console.error('Request failed: ' + err.message);
}).finally(() => {
  httpRequest.destroy();
});
```

## RCP 远程通信

@ohos.net.rcp 是新一代远程通信协议模块，提供更灵活的会话管理与请求拦截能力，适用于需要精细控制请求生命周期的场景。

### 创建会话与 GET 请求

```typescript
import { rcp } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let session = rcp.createSession();

session.get('https://example.com/api/data').then((response: rcp.Response) => {
  console.info('Status: ' + response.statusCode);
  console.info('Body: ' + response.body?.toString());
}).catch((err: BusinessError) => {
  console.error('RCP request failed: ' + err.message);
}).finally(() => {
  session.close();
});
```

### POST 请求

```typescript
import { rcp } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let session = rcp.createSession();

let request = new rcp.Request('https://example.com/api/submit', 'POST', {
  'Content-Type': 'application/json'
}, JSON.stringify({ name: 'test', value: 42 }));

session.fetch(request).then((response: rcp.Response) => {
  console.info('Status: ' + response.statusCode);
  console.info('Body: ' + response.body?.toString());
}).catch((err: BusinessError) => {
  console.error('RCP request failed: ' + err.message);
}).finally(() => {
  session.close();
});
```

### 会话配置与拦截器

```typescript
import { rcp } from '@kit.NetworkKit';

let session = rcp.createSession({
  headers: { 'Authorization': 'Bearer token123' },
  timeout: { connectMs: 10000, transferMs: 60000 }
});

session.on('fetchStart', (req: rcp.Request) => {
  console.info('Request started: ' + req.url);
});

session.on('fetchEnd', (req: rcp.Request, resp: rcp.Response) => {
  console.info('Request ended: ' + resp.statusCode);
});
```

## WebSocket

基于 @ohos.net.websocket 模块，支持全双工长连接通信。

### 建立连接与消息收发

```typescript
import { websocket } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let ws = websocket.createWebSocket();

ws.on('open', (err: BusinessError, value: websocket.EventOpen) => {
  if (err) {
    console.error('Open failed: ' + err.message);
    return;
  }
  ws.send('Hello Server');
});

ws.on('message', (err: BusinessError, value: websocket.EventMessage) => {
  if (err) {
    console.error('Message error: ' + err.message);
    return;
  }
  console.info('Received: ' + value.data);
});

ws.on('close', (err: BusinessError, value: websocket.EventClose) => {
  console.info('Closed: code=' + value.code + ', reason=' + value.reason);
});

ws.on('error', (err: BusinessError) => {
  console.error('WebSocket error: ' + err.message);
});

ws.connect('wss://example.com/ws');
```

### 关闭连接

```typescript
ws.close(1000, 'Normal closure');
```

## 网络状态监听

基于 @ohos.net.connection 模块，监听网络连接与断开事件。

### 注册网络状态回调

```typescript
import { connection } from '@kit.NetworkKit';
import { BusinessError } from '@kit.BasicServicesKit';

let netConnection = connection.createNetConnection();

netConnection.on('netAvailable', (data: connection.NetHandle) => {
  console.info('Network available, netId: ' + data.netId);
});

netConnection.on('netLost', (data: connection.NetHandle) => {
  console.info('Network lost, netId: ' + data.netId);
});

netConnection.on('netCapabilitiesChange', (data: connection.NetCapabilityInfo) => {
  console.info('Capabilities changed');
});

netConnection.register(() => {
  console.info('NetConnection registered');
});
```

### 查询当前网络

```typescript
import { connection } from '@kit.NetworkKit';

let netHandle = connection.getDefaultNet();
let capabilities = connection.getNetCapabilities(netHandle);
console.info('Bearer types: ' + JSON.stringify(capabilities?.bearerTypes));
console.info('Link bandwidth up: ' + capabilities?.linkUpBandwidthKbps);
```

### 注销监听

```typescript
netConnection.unregister(() => {
  console.info('NetConnection unregistered');
});
```

## 文件上传下载

基于 @ohos.request 模块，支持后台文件上传与下载。

### 文件下载

```typescript
import { request } from '@kit.BasicServicesKit';
import { BusinessError } from '@kit.BasicServicesKit';

let downloadConfig: request.DownloadConfig = {
  url: 'https://example.com/file.zip',
  filePath: '/data/storage/el2/base/haps/entry/files/file.zip',
  header: {},
  enableMetered: true,
  enableRoaming: true,
  description: '',
  networkType: request.NETWORK_MOBILE | request.NETWORK_WIFI,
  title: 'file.zip'
};

try {
  let downloadTask = request.downloadFile(downloadConfig);
  downloadTask.on('progress', (receivedSize: number, totalSize: number) => {
    console.info('Progress: ' + receivedSize + '/' + totalSize);
  });
  downloadTask.on('complete', () => {
    console.info('Download complete');
  });
  downloadTask.on('fail', (err: number) => {
    console.error('Download failed: ' + err);
  });
} catch (err) {
  console.error('Download error: ' + (err as BusinessError).message);
}
```

### 文件上传

```typescript
import { request } from '@kit.BasicServicesKit';
import { BusinessError } from '@kit.BasicServicesKit';

let uploadConfig: request.UploadConfig = {
  url: 'https://example.com/upload',
  header: { 'Authorization': 'Bearer token123' },
  method: 'POST',
  files: [
    { filename: 'test.jpg', name: 'file', uri: 'internal://cache/test.jpg', type: 'image/jpeg' }
  ],
  data: [
    { name: 'userId', value: '12345' }
  ]
};

try {
  let uploadTask = request.uploadFile(uploadConfig);
  uploadTask.on('progress', (uploadedSize: number, totalSize: number) => {
    console.info('Upload progress: ' + uploadedSize + '/' + totalSize);
  });
  uploadTask.on('headerReceive', (headers: object) => {
    console.info('Response headers: ' + JSON.stringify(headers));
  });
  uploadTask.on('complete', () => {
    console.info('Upload complete');
  });
  uploadTask.on('fail', (err: number) => {
    console.error('Upload failed: ' + err);
  });
} catch (err) {
  console.error('Upload error: ' + (err as BusinessError).message);
}
```

## API 23 新增能力

### HTTP 请求增强

HttpRequestOptions 新增配置项：

| 参数 | 说明 |
|------|------|
| `customMethod` | 自定义请求方法 |
| `maxRedirects` | 最大跳转次数 |
| `sniHostName` | TLS 握手阶段声明目标域名 |
| `pathPreference` | 指定特定激活网络 |

### DNS 转码

```typescript
import { connection } from '@kit.NetworkKit';

let ascii = connection.getDnsAscii('中文域名.中国');
let unicode = connection.getDnsUnicode('xn--fiqs8s.xn--fiqs8s');
```

### VPN 应用 UID 查询

```typescript
let uid = connection.getConnectionOwnerUid();
```

### Remote Communication Kit（RCP）API 23 新增

| 新增能力 | 说明 |
|---------|------|
| `Response.toJSON` BigInt 模式 | 支持大整数序列化 |
| `OnAuthenticationChallenge` | 认证挑战回调 |
| `DebugEvent.redirectCount` | 获取重定向次数 |
| `ConnectionReusePolicy` | HTTP 管道复用策略 |
| `network_config.json` | 配置 HTTP 明文请求禁用策略 |
| `defaultSession` | 默认通信会话，便捷发起请求 |
| `CookieRepository` | Cookie 管理器 |

## 网络权限

```json
"requestPermissions": [
  { "name": "ohos.permission.INTERNET" },
  { "name": "ohos.permission.GET_NETWORK_INFO" }
]
```

- `ohos.permission.INTERNET`：允许应用访问网络，normal 级别，用户授权。
- `ohos.permission.GET_NETWORK_INFO`：允许应用获取网络连接信息，normal 级别，用户授权。

---

## 官方参考

- HTTP 网络请求：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/net-http-overview-V5
- RCP 远程通信：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-net-rcp-V5
- WebSocket 连接：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/net-websocket-overview-V5
- 网络连接管理：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/net-connection-manager-overview-V5
- 上传下载：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/net-request-upload-download-V5