# 网络开发示例（Network）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## HTTP 请求

```typescript
import http from '@ohos.net.http';

// 创建请求任务
let httpRequest = http.createHttp();

// GET 请求
let result = await httpRequest.request(
  'https://example.com/api/data',
  {
    method: http.RequestMethod.GET,
    header: {
      'Content-Type': 'application/json'
    },
    connectTimeout: 60000,
    readTimeout: 60000
  }
);

console.info('响应码：' + result.responseCode);
console.info('响应体：' + result.result);

// 关闭请求
httpRequest.destroy();
```

## RCP（远端通讯协议）

> ⚠️ **模块路径待核实**：`@ohos.sdk.etc` 可能不正确，RCP 可能为 `@ohos.rpc` 或其他路径，请以官方文档为准。

```typescript
import rcp from '@ohos.sdk.etc';

// RCP Session
let session = rcp.createSession({
  baseAddress: 'https://api.example.com'
});

// GET
let response = await session.get('/data', {
  headers: { 'Accept': 'application/json' }
});

// POST
let postResponse = await session.post('/data', {
  body: JSON.stringify({ name: 'test' })
});

session.close();
```

## WebSocket

```typescript
import webSocket from '@ohos.net.webSocket';

// 创建 WebSocket 连接
let ws = webSocket.createWebSocket();

ws.on('open', (err, info) => {
  console.info('连接打开');
  ws.send('Hello');
});

ws.on('message', (err, data) => {
  console.info('收到消息：' + data);
});

ws.on('close', (err, info) => {
  console.info('连接关闭');
});

// 建立连接
ws.connect('wss://example.com/ws');

// 关闭连接
ws.close();
```

## 网络状态监听

```typescript
import observer from '@ohos.telephony.observer';

// 监听网络信号状态变化
observer.on('netStateChange', (data) => {
  console.info('网络状态变化：' + JSON.stringify(data));
});

// 获取网络连接信息
import connection from '@ohos.net.connection';
let netHandle = connection.getDefaultNetSync();
let connectionProperties = connection.getConnectionPropertiesSync(netHandle);
console.info('连接类型：' + connectionProperties.linkType);
```

## 网络编程完整示例仓

**Gitee 仓**：https://gitee.com/harmonyos4me/harmonyos_network_samples

覆盖：HTTP / TCP / TLS / UDP / WebSocket / Wi-Fi / RCP 等协议示例

## 注意事项

- 所有网络请求需要声明 `ohos.permission.INTERNET` 权限
- 使用 HTTPS 时注意证书校验
- HTTP 请求在 API 14+ 推荐使用 RCP 替代

## 官方参考

- HTTP：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/http-request
- WebSocket：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/websocket
