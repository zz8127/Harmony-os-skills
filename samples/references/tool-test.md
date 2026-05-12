# 工具与测试示例（Tool & Test）

> **适用版本**：HarmonyOS 6 / API 22（稳定）；API 23（稳定）

## DevEco Studio 工具

### 性能分析

- **Profiler**：CPU/内存/帧率/功耗分析
- **App Analyzer**：应用质量分析（内存泄漏、空指针等）
- 使用方式：DevEco Studio → Profile → Performance

### 模拟器与真机调试

```bash
# 连接真机（USB 调试）
hdc list targets  # 查看已连接设备
hdc shell         # 进入设备 shell

# 安装 HAP
hdc install entry/build/default/outputs/default/entry.hap

# 卸载应用
hdc uninstall com.example.myapp
```

---

## 应用异常处理（hiAppEvent）

**Gitee 示例**：https://gitee.com/HarmonyOS_Samples/ExceptionHandling

```typescript
import hiAppEvent from '@hiviewdfx.hiappevent';

// 开启事件打点
hiAppEvent.setEventBrushEnabled(true);

// 订阅异常事件
hiAppEvent.watch({
  onReceive: (domain, name, params) => {
    console.info('收到应用事件：' + domain + '/' + name);
    console.info('参数：' + JSON.stringify(params));
  }
});

// 手动打点
hiAppEvent.addEvent({
  domain: 'my_app',
  name: 'user_action',
  params: { key: 'value' }
});

// 获取崩溃日志
let dumpData = await hiAppEvent.queryEvent('crash', {
  size: 10,
  beginTime: Date.now() - 86400000, // 24小时内
  endTime: Date.now()
});
console.info('崩溃日志：' + JSON.stringify(dumpData));
```

---

## 单元测试（Hypium）

```typescript
// 导入测试框架
import Hypium from '@ohos/hypium';

// 同步测试
it('should add two numbers', 0, () => {
  expect(1 + 1).assertEqual(2);
});

// 异步测试
it('should wait for async operation', 0, async (done) => {
  setTimeout(() => {
    expect(true).assertTrue();
    done();
  }, 1000);
});

// 生命周期测试
describe('MyAbilityTest', () => {
  let abilityContext;

  beforeAll(async (done) => {
    // 初始化测试环境
    abilityContext = abilityAccessCtrl.createAtManager();
    done();
  });

  it('ability lifecycle test', 0, async (done) => {
    // 测试 UIAbility 生命周期
    done();
  });
});
```

**npm 包**：`@ohos/hypium`（已内置于 DevEco Studio）

---

## Mock 测试（HaMock）

```typescript
import mock from '@ohos/harmony-utils/mock';

// Mock 异步方法
mock.mockResource('deviceInfo').mock({
  brand: 'mockBrand',
  deviceType: 'phone'
});

// 使用 mock 后的值
let deviceInfo = deviceInfoModule.getDeviceInfo();
console.info('Brand: ' + deviceInfo.brand); // 输出 mockBrand
```

---

## 官方参考

- DevEco Studio 下载：https://developer.huawei.com/consumer/cn/develop/deveco/studio
- 应用异常处理：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hiappevent-guidelines
- Hypium 测试框架：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/hypium-guidelines
- HaMock：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/harmonyutils-guidelines
