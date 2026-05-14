# Test Kit

## 概述

Test Kit（应用测试服务）是 HarmonyOS 自动化测试框架的总称，提供单元测试、UI 测试和白盒性能测试三大能力。框架以 ohpm 包 `@ohos/hypium` 独立发布，开发者可在 DevEco Studio 中编写、执行测试脚本，也可通过命令行（hdc shell aa test）触发执行。

## 核心能力

### 单元测试框架（JsUnit）

自动化测试框架基础底座，提供测试脚本识别、调度、执行和结果汇总能力。

| 特性 | 功能说明 |
|---|---|
| 基础流程能力 | 测试用例识别调度及异步执行 |
| 断言能力 | 判断用例实际结果与预期值是否相符 |
| Mock 能力 | 函数级 Mock，修改函数行为返回指定值或执行指定操作 |
| 数据驱动能力 | 复用同一测试脚本，使用不同输入数据驱动执行 |
| 专项能力 | 用例筛选、随机执行、压力测试、超时设置、遇错即停、跳过执行 |

基础流程接口：

| 接口 | 说明 |
|---|---|
| `describe` | 定义测试套 |
| `it` | 定义测试用例 |
| `beforeAll` | 所有用例开始前执行一次 |
| `beforeEach` | 每条用例开始前执行 |
| `afterEach` | 每条用例结束后执行 |
| `afterAll` | 所有用例结束后执行一次 |
| `beforeItSpecified` | 仅在指定用例开始前执行（1.0.15+） |
| `afterItSpecified` | 仅在指定用例结束后执行（1.0.15+） |
| `beforeEachIt` | 每条用例开始前执行，外层套件对内层生效（1.0.25+） |
| `afterEachIt` | 每条用例结束后执行，外层套件对内层生效（1.0.25+） |
| `expect` | 断言接口 |
| `xdescribe` | 跳过整个测试套（1.0.17+） |
| `xit` | 跳过单条测试用例（1.0.17+） |

### UI 测试框架（UITest）

提供 UI 界面查找和模拟操作能力，覆盖 UI 自动化测试关键场景。

| 能力 | 说明 |
|---|---|
| 控件查找与操作 | 依据多种属性构造匹配器查找控件，支持滚动查找 |
| 模拟触摸屏操作 | 点击、双击、长按、滑动、拖拽、多指操作 |
| 页面加载等待 | 等待控件出现或页面空闲 |
| 模拟文本输入 | 基于控件或坐标输入文本，支持复制粘贴方式和追加输入 |
| 截图 | 截取指定区域或指定屏幕的屏幕截图 |
| UI 事件监听 | 监听 toast、dialog 等控件出现 |
| 模拟键鼠操作 | 键盘输入、鼠标操作 |
| 窗口查找与操作 | 查找和操作窗口 |
| 模拟触摸板操作 | 触控板手势模拟 |
| 模拟手写笔操作 | 手写笔动作模拟 |
| 模拟表冠操作 | 表冠旋转等操作模拟 |
| 屏幕显示操作 | 屏幕显示控制 |

核心类：

| 类 | 说明 |
|---|---|
| `Driver` | UI 测试驱动入口，提供控件查找、坐标操作、截图等能力 |
| `ON` / `On` | 控件匹配器构造，支持 type、text、id 等属性匹配 |
| `Component` | 控件对象，提供点击、输入文本、获取属性等操作 |
| `PointerMatrix` | 多指操作坐标矩阵 |
| `UIEventObserver` | UI 事件监听器 |
| `UiDirection` | 滑动方向枚举 |

### 白盒性能测试框架

提供白盒性能测试能力，用于测量应用内部函数/模块的执行性能。

## npm 包名

`@kit.TestKit`

## ohpm 依赖

```json
{
  "devDependencies": {
    "@ohos/hypium": "1.0.25"
  }
}
```

## 关键 API

| API | 说明 |
|---|---|
| `abilityDelegatorRegistry` | 程序框架服务，获取 AbilityDelegator 用于启动被测应用 |
| `Driver.create()` | 创建 UI 测试 Driver 实例 |
| `driver.findComponent(ON)` | 查找单个控件 |
| `driver.findComponents(On)` | 查找多个控件 |
| `driver.waitForComponent(ON, timeout)` | 等待控件出现 |
| `driver.waitForIdle(idleMs, timeoutMs)` | 等待页面空闲 |
| `driver.click(x, y)` | 坐标点击 |
| `driver.swipe(x1, y1, x2, y2, speed)` | 滑动 |
| `driver.drag(x1, y1, x2, y2, speed)` | 拖拽 |
| `driver.screenCapture(savePath, options?)` | 屏幕截图 |
| `driver.inputText(point, text)` | 基于坐标输入文本 |
| `component.click()` | 控件点击 |
| `component.inputText(text)` | 控件输入文本 |
| `component.pinchOut(scale)` | 双指放大 |
| `driver.createUIEventObserver()` | 创建 UI 事件监听器 |
| `driver.assertComponentExist(ON)` | 断言控件存在 |

## 权限要求

无额外权限要求。测试 HAP 的 APL 等级为 normal，截图保存路径需使用应用沙箱路径。

## 约束与限制

- 测试脚本需连接硬件设备执行
- UI 测试框架不支持并发调用（不可多个测试用例同时操作 UI）
- 命令行执行需通过 `hdc shell aa test` 命令

## 官方链接

- [自动化测试框架使用指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkxtest-guidelines-0000001930756221)
- [单元测试框架使用指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines)
- [UI 测试框架使用指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines)
- [白盒性能测试框架使用指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/perftest-guideline)
- [UITest API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest)
