# Web寮€鍙戯紙ArkWeb锛?
> **閫傜敤鐗堟湰**锛欻armonyOS 6.1 / API 23锛堢ǔ瀹氾級銆傚吋瀹?API 14+銆?
## 姒傝堪

ArkWeb 鎻愪緵 Web 缁勪欢鍜?Web 寮曟搸鑳藉姏锛屾敮鎸佸湪搴旂敤鍐呭祵鍏ョ綉椤点€丣avaScript 涓?ArkTS 鍙屽悜閫氫俊銆侀〉闈㈠姞杞芥帶鍒躲€佸畨鍏ㄧ瓥鐣ョ鐞嗙瓑銆侫PI 23 鏂板鐢讳腑鐢汇€佸瓧浣撻鍔犺浇銆佸悓灞傛覆鏌撶瓑鐗规€э紱API 24 鏂板 URL 鐧藉悕鍗曘€佷笅杞藉洖璋冪瓑鐗规€с€?
## Web 缁勪欢鍩虹

```typescript
import { webview } from '@kit.ArkWeb';

@Entry
@Component
struct WebPage {
  controller: webview.WebviewController = new webview.WebviewController();

  build() {
    Column() {
      Web({ src: 'https://www.example.com', controller: this.controller })
        .width('100%')
        .height('100%')
        .javaScriptAccess(true)
        .domStorageAccess(true)
    }
  }
}
```

## 椤甸潰鍔犺浇

### 鍔犺浇鏈湴璧勬簮

```typescript
Web({ src: $rawfile('index.html'), controller: this.controller })
  .width('100%')
  .height('100%')
```

### 鍔犺浇甯﹀弬鏁扮殑 URL

```typescript
this.controller.loadUrl('https://www.example.com/path?param=value');
```

### 鍔犺浇 HTML 鏁版嵁

```typescript
this.controller.loadData(
  '<html><body><h1>Hello ArkWeb</h1></body></html>',
  'text/html',
  'UTF-8'
);
```

### 椤甸潰鍔犺浇浜嬩欢

```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .onPageBegin((event) => {
    console.info('Page begin: ' + event?.url);
  })
  .onPageEnd((event) => {
    console.info('Page end: ' + event?.url);
  })
  .onProgressChange((event) => {
    console.info('Loading progress: ' + event?.newProgress);
  })
  .onErrorReceive((event) => {
    console.error('Load error: ' + event?.error.getErrorInfo());
  })
```

## JavaScript Bridge锛坖avaScriptProxy锛?
### ArkTS 娉ㄥ唽瀵硅薄渚?JS 璋冪敤

```typescript
class WebBridge {
  constructor() {}

  getDeviceInfo(): string {
    return 'HarmonyOS Device';
  }

  showToast(msg: string): void {
    console.info('JS Toast: ' + msg);
  }
}

@Entry
@Component
struct WebBridgePage {
  controller: webview.WebviewController = new webview.WebviewController();

  build() {
    Column() {
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
        .javaScriptProxy({
          object: new WebBridge(),
          name: 'nativeBridge',
          methodList: ['getDeviceInfo', 'showToast'],
          controller: this.controller
        })
    }
  }
}
```

### JS 绔皟鐢?
```html
<script>
  let info = nativeBridge.getDeviceInfo();
  nativeBridge.showToast('Hello from JS');
</script>
```

### ArkTS 璋冪敤 JS 鍑芥暟

```typescript
this.controller.runJavaScript('updateFromNative("data from ArkTS")')
  .then((result) => {
    console.info('JS returned: ' + result);
  })
  .catch((err: Error) => {
    console.error('runJavaScript failed: ' + err.message);
  });
```

## 瀹夊叏鎺у埗

### 鍩熷悕鐧藉悕鍗?
```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .allowGeolocation('https://www.example.com')
  .allowWindowOpenMethod(true)
  .multiWindowAccess(false)
  .webDebuggingAccess(false)
```

### HTTP 鎷︽埅涓庤姹傛帶鍒?
```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .onInterceptRequest((event) => {
    if (event?.request.getRequestUrl().startsWith('https://ads.example.com')) {
      return new WebResourceResponse('text/plain', 'UTF-8', 200, 'Blocked', []);
    }
    return null;
  })
```

### SSL 閿欒澶勭悊

```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .onSslErrorEventReceive((event) => {
    event.handler.handleConfirm();
  })
```

## Cookie 绠＄悊

```typescript
import { webview } from '@kit.ArkWeb';

let cookieManager = webview.WebCookieManager.getInstance();

cookieManager.saveCookieAsync();

cookieManager.setCookie('https://www.example.com', 'session=abc123');

let cookies = cookieManager.getCookie('https://www.example.com');
console.info('Cookies: ' + cookies);

cookieManager.deleteEntireCookie();
```

## API 23 鏂扮壒鎬?
### 鐢讳腑鐢伙紙PiP锛?
```typescript
Web({ src: 'https://video.example.com', controller: this.controller })
  .enablePiP(true)
  .onPiPStatusChanged((event) => {
    console.info('PiP status: ' + event?.status);
  })
```

### 瀛椾綋棰勫姞杞?
```typescript
let config: webview.PreloadFontConfig = {
  fontFamily: 'CustomFont',
  src: $rawfile('fonts/custom.ttf')
};

webview.WebviewController.preloadFont(config);
```

### 鍚屽眰娓叉煋

```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .enableNativeEmbedMode(true)
  .onNativeEmbedLifecycleChange((event) => {
    console.info('Embed status: ' + event?.status);
    console.info('Embed id: ' + event?.embedId);
  })
```

## API 24 鏂扮壒鎬?
### URL 鐧藉悕鍗?
```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .urlWhiteList(['https://www.example.com/*', 'https://api.example.com/*'])
  .onUrlBlockIntercept((event) => {
    console.info('Blocked URL: ' + event?.url);
    return true;
  })
```

### 涓嬭浇鍥炶皟

```typescript
Web({ src: 'https://www.example.com', controller: this.controller })
  .onDownloadStart((event) => {
    if (event) {
      console.info('Download URL: ' + event.url);
      console.info('Download MIME: ' + event.mimeType);
      console.info('Download size: ' + event.contentLength);
    }
  })
```

## 鏉冮檺

| 鏉冮檺 | 璇存槑 |
|------|------|
| `ohos.permission.INTERNET` | 缃戠粶璁块棶 |
| `ohos.permission.GET_WIFI_INFO` | 缃戠粶鐘舵€佸垽鏂?|

---

## 瀹樻柟鍙傝€?
- Web 缁勪欢寮€鍙戞寚瀵硷細https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/web-component-V5
- Web 缁勪欢姒傝堪锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb-overview-V5
- JavaScript Bridge锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb-js-bridge-V5
- Web 瀹夊叏锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkweb-security-V5
- Web ArkTS API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-basic-components-web-V5
- webview API锛歨ttps://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-webview-V5