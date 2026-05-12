# 应用测试

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）；HarmonyOS 6.0 / API 22（稳定）。兼容 API 14+。

## 概述

HarmonyOS 应用测试框架（arkxtest）是一体化测试底座，由**单元测试框架（JsUnit）**和**UI测试框架（UiTest）**两部分组成，以 ohpm 包 `@ohos/hypium` 独立发布。

| 框架 | 核心能力 | 适用场景 |
|------|---------|---------|
| JsUnit（单元测试） | 用例识别、调度、断言、Mock、数据驱动 | 函数/类/组件逻辑验证 |
| UiTest（UI测试） | 控件查找、事件模拟、状态断言 | 界面交互自动化验证 |

**测试金字塔原则**：

- **70% 单元测试**：业务逻辑、工具函数、状态管理
- **20% 集成测试**：服务调用、组件组合
- **10% UI自动化测试**：核心用户旅程、端到端场景

---

## 单元测试

### 框架依赖

在模块级 `oh-package.json5` 中配置 `@ohos/hypium`：

```json
{
  "devDependencies": {
    "@ohos/hypium": "1.0.25"
  }
}
```

### 测试文件结构

```
entry/src/ohosTest/ets/
├── test/
│   ├── ability.test.ets
│   ├── calculator.test.ets
│   └── list/
│       └── ListAbility.test.ets
├── testrunner/
│   └── OpenHarmonyTestRunner.ets
└── module.json5
```

**命名约定**：`xxx.test.ets`

### 核心API

从 `@ohos/hypium` 导入：

| 接口 | 说明 |
|------|------|
| `describe` | 定义测试套 |
| `it` | 定义测试用例 |
| `expect` | 断言入口 |
| `beforeAll` | 测试套前置（执行一次） |
| `beforeEach` | 每条用例前置 |
| `afterEach` | 每条用例后置 |
| `afterAll` | 测试套后置（执行一次） |
| `xit` | 跳过测试用例 |
| `xdescribe` | 跳过测试套 |

### 断言API

| 方法 | 说明 |
|------|------|
| `assertEqual(value)` | 严格相等 |
| `assertNotEqual(value)` | 不相等 |
| `assertTrue()` | 为 true |
| `assertFalse()` | 为 false |
| `assertNull()` | 为 null |
| `assertNotNull()` | 不为 null |
| `assertUndefined()` | 为 undefined |
| `assertDefined()` | 已定义 |
| `assertContain(value)` | 包含指定值 |
| `assertThrowError(message)` | 抛出指定异常 |
| `assertClose(value, margin)` | 浮点近似相等 |
| `assertDeepEquals(value)` | 深度相等（对象/数组） |

### 用例级别与规模

`it` 第二个参数支持位运算组合：

| 枚举 | 说明 |
|------|------|
| `TestType.FUNCTION` | 功能测试 |
| `TestType.PERFORMANCE` | 性能测试 |
| `TestType.POWER` | 功耗测试 |
| `Level.LEVEL0` ~ `Level.LEVEL4` | 用例级别 |
| `Size.SMALLTEST` / `MEDIUMTEST` / `LARGETEST` | 用例规模 |

### 代码示例

```typescript
import { describe, it, expect, beforeAll, afterAll, Level, TestType, Size } from '@ohos/hypium'

export default function calculatorTest() {
  describe('CalculatorTest', () => {
    let calc: Calculator

    beforeAll(() => {
      calc = new Calculator()
    })

    afterAll(() => {
      calc = null
    })

    it('add_should_return_sum', TestType.FUNCTION | Size.MEDIUMTEST | Level.LEVEL1, 0, () => {
      expect(calc.add(2, 3)).assertEqual(5)
      expect(calc.add(-1, 1)).assertEqual(0)
    })

    it('divide_should_throw_on_zero', TestType.FUNCTION | Size.SMALLTEST | Level.LEVEL0, () => {
      expect(() => calc.divide(1, 0)).assertThrowError('Division by zero')
    })

    it('percentage_should_be_close', TestType.FUNCTION | Size.SMALLTEST | Level.LEVEL1, () => {
      expect(calc.percentage(1, 3)).assertClose(33.33, 0.01)
    })
  })
}

class Calculator {
  add(a: number, b: number): number {
    return a + b
  }

  divide(a: number, b: number): number {
    if (b === 0) {
      throw new Error('Division by zero')
    }
    return a / b
  }

  percentage(value: number, total: number): number {
    return (value / total) * 100
  }
}
```

### 异步测试

```typescript
import { describe, it, expect, Level } from '@ohos/hypium'

describe('AsyncTest', () => {
  it('async_operation', Level.LEVEL1, async (done: Function) => {
    let result = await fetchData('https://api.example.com/data')
    expect(result.status).assertEqual(200)
    done()
  })
})
```

### DevEco Studio 执行

1. 连接目标设备
2. 右键测试文件 / 测试套 / 单条用例 → Run Tests
3. 支持四种执行粒度：测试包、测试类、测试套、单条用例
---

## UI测试

### 框架依赖

UI测试在单元测试基础上增量开发，额外导入 `@kit.TestKit`：

```typescript
import { abilityDelegatorRegistry, Driver, ON, Component } from '@kit.TestKit'
import { UIAbility, Want } from '@kit.AbilityKit'
```

> **注意**：旧版 `UiDriver`、`UiComponent`、`By` 自 API 9 起已废弃，应使用 `Driver`、`Component`、`ON`。

### ON 选择器

`ON` 类提供控件特征描述，支持链式调用：

| 方法 | 说明 | 示例 |
|------|------|------|
| `ON.text(txt, pattern?)` | 文本匹配 | `ON.text('登录')` |
| `ON.id(id)` | ID 匹配 | `ON.id('submitBtn')` |
| `ON.type(tp)` | 类型匹配 | `ON.type('Button')` |
| `ON.clickable(b?)` | 可点击 | `ON.clickable(true)` |
| `ON.scrollable(b?)` | 可滚动 | `ON.scrollable(true)` |
| `ON.enabled(b?)` | 可用状态 | `ON.enabled(true)` |
| `ON.focused(b?)` | 焦点状态 | `ON.focused(true)` |
| `ON.selected(b?)` | 选中状态 | `ON.selected(true)` |
| `ON.isBefore(on)` | 相对位置（在前） | `ON.text('标签').isBefore(ON.id('input'))` |
| `ON.isAfter(on)` | 相对位置（在后） | `ON.id('input').isAfter(ON.text('标签'))` |
| `ON.within(on)` | 父容器约束 | `ON.text('项').within(ON.type('List'))` |
| `ON.description(desc)` | 描述匹配 | `ON.description('关闭')` |

**匹配模式**（`MatchPattern`）：

| 值 | 说明 |
|---|------|
| `EQUALS` | 精确匹配（默认） |
| `CONTAINS` | 包含 |
| `STARTS_WITH` | 前缀匹配 |
| `ENDS_WITH` | 后缀匹配 |

### Driver 操作

`Driver` 是 UI 测试入口类：

| 方法 | 说明 |
|------|------|
| `Driver.create()` | 创建 Driver 实例 |
| `delayMs(ms)` | 延时等待 |
| `findComponent(on)` | 查找单个控件 |
| `findComponents(on)` | 查找多个控件 |
| `waitForComponent(on, timeout)` | 等待控件出现 |
| `waitForIdle(idleMs, timeoutMs)` | 等待页面空闲 |
| `assertComponentExist(on)` | 断言控件存在 |
| `pressBack()` | 返回键 |
| `pressHome()` | Home键 |
| `click(x, y)` | 坐标点击 |
| `doubleClick(x, y)` | 坐标双击 |
| `longClick(x, y)` | 坐标长按 |
| `swipe(x1, y1, x2, y2, speed?)` | 坐标滑动 |
| `drag(x1, y1, x2, y2, speed?)` | 坐标拖拽 |
| `fling(direction, speed)` | 方向抛滑 |
| `inputText(point, text)` | 坐标输入文本 |
| `triggerKey(keyCode)` | 按键注入 |
| `triggerCombineKeys(key1, key2, key3?)` | 组合键 |
| `screenCap(savePath)` | 截屏 |
| `screenCapture(savePath, rect?)` | 区域截屏 |
| `findWindow(filter)` | 查找窗口 |

### Component 操作

`Component` 代表 UI 控件实例：

| 方法 | 说明 |
|------|------|
| `click()` | 点击控件 |
| `doubleClick()` | 双击控件 |
| `longClick()` | 长按控件 |
| `inputText(text)` | 输入文本（默认清空后输入） |
| `clearText()` | 清空文本 |
| `scrollSearch(on)` | 滚动查找子控件 |
| `scrollToTop()` | 滚动到顶部 |
| `scrollToBottom()` | 滚动到底部 |
| `dragTo(target)` | 拖拽到目标控件 |
| `pinchOut(scale)` | 双指放大 |
| `pinchIn(scale)` | 双指缩小 |
| `getId()` | 获取控件ID |
| `getText()` | 获取文本 |
| `getType()` | 获取类型 |
| `getBounds()` | 获取边界 |
| `getBoundsCenter()` | 获取中心坐标 |
| `isClickable()` | 是否可点击 |
| `isScrollable()` | 是否可滚动 |
| `isEnabled()` | 是否可用 |
| `isFocused()` | 是否获焦 |
### 代码示例

```typescript
import { describe, it, expect, Level } from '@ohos/hypium'
import { abilityDelegatorRegistry, Driver, ON } from '@kit.TestKit'
import { UIAbility, Want } from '@kit.AbilityKit'

const delegator = abilityDelegatorRegistry.getAbilityDelegator()

export default function uiTest() {
  describe('LoginUiTest', () => {
    it('login_flow', Level.LEVEL1, async (done: Function) => {
      let driver = Driver.create()
      let bundleName = abilityDelegatorRegistry.getArguments().bundleName

      let want: Want = {
        bundleName: bundleName,
        abilityName: 'EntryAbility'
      }
      await delegator.startAbility(want)
      await driver.waitForIdle(4000, 5000)

      let ability: UIAbility = await delegator.getCurrentTopAbility()
      expect(ability.context.abilityInfo.name).assertEqual('EntryAbility')

      let usernameInput = await driver.findComponent(ON.id('usernameInput'))
      await usernameInput.inputText('testuser')

      let passwordInput = await driver.findComponent(ON.id('passwordInput'))
      await passwordInput.inputText('123456')

      let loginBtn = await driver.findComponent(ON.text('登录'))
      await loginBtn.click()
      await driver.waitForIdle(4000, 5000)

      await driver.assertComponentExist(ON.textContains('欢迎'))

      await driver.pressBack()
      done()
    })

    it('scroll_and_find_item', Level.LEVEL2, async (done: Function) => {
      let driver = Driver.create()

      let list = await driver.findComponent(ON.id('todoList').scrollable(true))
      let targetItem = await list.scrollSearch(ON.text('待办项50'))
      let text = await targetItem.getText()
      expect(text).assertContain('待办项50')

      done()
    })

    it('swipe_and_pinch', Level.LEVEL2, async (done: Function) => {
      let driver = Driver.create()

      await driver.swipe(300, 800, 300, 200, 600)

      let image = await driver.findComponent(ON.type('Image'))
      await image.pinchOut(1.5)
      await image.pinchIn(0.8)

      done()
    })
  })
}
```

---

## Mock测试

`@ohos/hypium` 提供函数级 Mock 能力，可对指定函数进行行为替换。

### Mock API

| 方法 | 说明 |
|------|------|
| `Mock.mock(fn)` | 创建 Mock 函数 |
| `mock.returnValue(value)` | 指定返回值 |
| `mock.returnValues(...values)` | 依次返回多个值 |
| `mock.mockImplementation(fn)` | 替换实现 |
| `mock.mockClear()` | 清除调用记录 |
| `mock.mockReset()` | 重置为空实现 |
| `mock.calls` | 调用记录数组 |

### 代码示例

```typescript
import { describe, it, expect, beforeEach, Mock, mock } from '@ohos/hypium'

describe('MockTest', () => {
  let mockFetch: Mock

  beforeEach(() => {
    mockFetch = mock(jest.fn())
    mockFetch.mockReturnValue({ status: 200, data: 'mocked' })
  })

  it('should_return_mocked_data', 0, () => {
    let result = mockFetch('https://api.example.com/data')
    expect(result.status).assertEqual(200)
    expect(result.data).assertEqual('mocked')
    expect(mockFetch.calls.length).assertEqual(1)
  })

  it('should_return_sequential_values', 0, () => {
    mockFetch.mockReturnValues({ status: 200 }, { status: 404 })
    expect(mockFetch().status).assertEqual(200)
    expect(mockFetch().status).assertEqual(404)
  })
})
```
---

## 测试配置

### oh-package.json5 依赖配置

```json
{
  "name": "entry",
  "version": "1.0.0",
  "devDependencies": {
    "@ohos/hypium": "1.0.25"
  }
}
```

### 测试模块 module.json5

测试模块位于 `src/ohosTest/` 目录，拥有独立的 `module.json5`：

```json
{
  "module": {
    "name": "entry_test",
    "type": "feature",
    "deviceTypes": ["phone", "tablet"],
    "deliveryWithInstall": true,
    "installationFree": false
  }
}
```

### hvigorfile.ts 测试构建配置

测试模块的 `hvigorfile.ts` 通常无需额外配置，DevEco Studio 自动生成。如需自定义测试任务，可在模块级 `hvigorfile.ts` 中扩展。

### DevEco Studio 执行测试

1. 连接目标设备
2. 选择测试文件 → 右键 → **Run Tests**
3. 支持四种执行粒度：
   - 测试包级别：执行全部用例
   - 测试类级别：执行 `.ets` 文件全部用例
   - 测试套级别：执行 `describe` 中全部用例
   - 用例级别：执行指定 `it` 用例

### 命令行执行测试

通过 `hdc shell aa test` 命令执行：

**执行全部用例**：

```bash
hdc shell aa test -b com.example.myapp -m entry -s unittest OpenHarmonyTestRunner
```

**执行指定测试套**：

```bash
hdc shell aa test -b com.example.myapp -m entry -s unittest OpenHarmonyTestRunner -s class CalculatorTest
```

**执行指定用例**：

```bash
hdc shell aa test -b com.example.myapp -m entry -s unittest OpenHarmonyTestRunner -s class CalculatorTest#add_should_return_sum
```

**常用参数**：

| 参数 | 说明 | 示例 |
|------|------|------|
| `-b` / `--bundleName` | 应用包名 | `-b com.example.myapp` |
| `-m` / `--moduleName` | 模块名 | `-m entry` |
| `-s unittest` | TestRunner 名称 | `-s unittest OpenHarmonyTestRunner` |
| `-s class` | 指定测试套/用例 | `-s class Suite#case` |
| `-s notClass` | 排除测试套/用例 | `-s notClass Suite` |
| `-s timeout` | 超时时间（ms） | `-s timeout 15000` |
| `-s breakOnError` | 遇错即停 | `-s breakOnError true` |
| `-s random` | 随机顺序执行 | `-s random true` |
| `-s testType` | 按类型筛选 | `-s testType function` |
| `-s level` | 按级别筛选 | `-s level 0` |
| `-s size` | 按规模筛选 | `-s size small` |
| `-s stress` | 重复执行次数 | `-s stress 100` |

### 测试结果日志

命令行执行后，框架输出 `OHOS_REPORT_*` 格式日志：

| 字段 | 含义 |
|------|------|
| `OHOS_REPORT_STATUS_CODE: 1` | 用例开始执行 |
| `OHOS_REPORT_STATUS_CODE: 0` | 用例执行通过 |
| `OHOS_REPORT_STATUS_CODE: -1` | 用例执行报错 |
| `OHOS_REPORT_STATUS_CODE: -2` | 用例执行失败 |
| `OHOS_REPORT_RESULT: stream=` | 汇总：run / Failure / Error / Pass / Ignore |
---

## 应用专项测试

### 兼容性测试（云测试）

AppGallery Connect 云测试提供一站式真机兼容性验证：

- **海量远程真机**：覆盖主流 HarmonyOS 设备型号
- **自动化执行**：7×24 小时自动测试
- **详细报告**：截图、日志、性能数据
- **免费额度**：每个开发者账号每天 300 分钟

**接入流程**：

1. AGC → 我的应用 → 云测试
2. 上传已签名的 release 包（.hap 或 .app）
3. 选择目标设备型号
4. 执行兼容性测试
5. 查看测试报告

**前提条件**：

- 使用发布证书签名
- release 模式打包
- 包大小不超过 4GB

### 稳定性测试

验证应用长时间运行的可靠性：

| 测试类型 | 说明 |
|---------|------|
| Monkey 测试 | 随机事件注入，验证崩溃/ANR |
| 遍历测试 | 自动遍历页面，验证功能稳定性 |
| 压力测试 | 重复执行用例（`-s stress N`） |

DevEco Testing 工具提供稳定性测试能力，支持服务卡片式操作。

### 安全测试

| 测试项 | 说明 |
|--------|------|
| 隐私合规 | 隐私声明完整性、权限申请合理性 |
| 数据安全 | 敏感数据加密存储、传输安全 |
| 代码安全 | 混淆、反编译防护 |
| 漏洞扫描 | AGC 安全扫描服务 |

**前提条件**：应用已配置隐私声明和隐私标签。

### 性能测试

| 指标 | 说明 |
|------|------|
| 冷启动时间 | 应用首次启动耗时 |
| 热启动时间 | 应用恢复前台耗时 |
| 页面切换时间 | 路由跳转耗时 |
| 内存占用 | 运行时内存峰值 |
| 帧率（FPS） | 滑动/动画流畅度 |
| CPU 占用 | 运行时 CPU 使用率 |

**白盒性能测试**：`@ohos/hypium` 集成性能采集能力，可在测试脚本中采集内存、CPU、帧率等指标。

DevEco Studio Profiler 也提供可视化性能分析工具。

---

## 官方参考链接

- 自动化测试框架使用指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkxtest-guidelines
- 单元测试框架使用指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/unittest-guidelines
- UI测试框架使用指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/uitest-guidelines
- @ohos/hypium ohpm 包：https://ohpm.openharmony.cn/#/cn/detail/@ohos%2Fhypium
- @ohos.UiTest API 参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-uitest
- DevEco Studio 测试指导：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-instrument-test
- aa test 命令指南：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/aa-tool
- AGC 云测试：https://developer.huawei.com/consumer/cn/service/josp/agc/