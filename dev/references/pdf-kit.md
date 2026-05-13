# PDF 服务（PDF Kit）

> HarmonyOS 6.1 / API 23

## 概述

PDF 服务（PDF Kit）提供 PDF 文档的加载、渲染、页面导航和文本提取等能力，通过 `@kit.PDFKit` 引入。API 23 新增文本内容提取和自定义缩放范围等特性。

## PdfService

PdfService 是 PDF 服务的入口，用于初始化和管理 PDF 文档。

```typescript
import { pdfService } from '@kit.PDFKit';

async function initializePdfService(): Promise<void> {
  await pdfService.init();
}
```

## PdfViewManager

PdfViewManager 管理 PDF 视图的创建与生命周期。

```typescript
import { pdfService, PdfViewManager } from '@kit.PDFKit';

async function createPdfView(filePath: string): Promise<PdfViewManager> {
  const viewManager = await pdfService.createPdfViewManager(filePath);
  return viewManager;
}
```

## 页面导航

在 PDF 文档中进行页面跳转和浏览。

```typescript
import { PdfViewManager } from '@kit.PDFKit';

async function navigatePages(viewManager: PdfViewManager): Promise<void> {
  const pageCount = await viewManager.getPageCount();
  console.info(`总页数: ${pageCount}`);

  await viewManager.goToPage(0);

  await viewManager.goToNextPage();

  await viewManager.goToPrevPage();

  const currentPage = await viewManager.getCurrentPage();
  console.info(`当前页: ${currentPage}`);
}
```

## 文本提取（API 23）

API 23 新增文本内容提取接口，可获取指定页面的文本。

```typescript
import { PdfViewManager } from '@kit.PDFKit';

async function extractText(viewManager: PdfViewManager, pageIndex: number): Promise<string> {
  const textContent = await viewManager.getTextContent(pageIndex);
  return textContent;
}

async function extractAllText(viewManager: PdfViewManager): Promise<string> {
  const pageCount = await viewManager.getPageCount();
  let fullText = '';
  for (let i = 0; i < pageCount; i++) {
    const pageText = await viewManager.getTextContent(i);
    fullText += pageText + '\n';
  }
  return fullText;
}
```

## 自定义缩放范围（API 23）

API 23 支持设置 PDF 视图的最大和最小缩放比例。

```typescript
import { PdfViewManager } from '@kit.PDFKit';

async function setZoomRange(viewManager: PdfViewManager): Promise<void> {
  await viewManager.setMaxZoom(5.0);
  await viewManager.setMinZoom(0.5);
  await viewManager.setZoom(2.0);
}
```

## 页面渲染

将 PDF 页面渲染为图片。

```typescript
import { PdfViewManager } from '@kit.PDFKit';
import { image } from '@kit.ImageKit';

async function renderPage(viewManager: PdfViewManager, pageIndex: number): Promise<image.PixelMap> {
  const pixelMap = await viewManager.renderPage(pageIndex, {
    width: 1080,
    height: 1920
  });
  return pixelMap;
}
```

## PDF 视图组件

在页面中嵌入 PDF 视图组件。

```typescript
import { PdfView } from '@kit.PDFKit';

@Entry
@Component
struct PdfViewerPage {
  private pdfUri: string = 'file:///data/storage/el2/base/files/example.pdf';

  build() {
    Column() {
      PdfView({ uri: this.pdfUri })
        .width('100%')
        .height('100%')
        .onPageChanged((currentPage: number) => {
          console.info(`当前页: ${currentPage}`);
        })
        .onLoadComplete((pageCount: number) => {
          console.info(`加载完成，共 ${pageCount} 页`);
        })
    }
  }
}
```

## 权限

| 权限 | 说明 |
|------|------|
| 无特殊权限 | PDF 服务本身无需额外权限 |

访问文件时需要对应文件读取权限。

## 官方参考

- [PDF Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/pdf-kit-overview-0000001820880921)
- [PDF Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/pdf-service-0000001774121286)
