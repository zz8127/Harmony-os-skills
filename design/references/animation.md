# 动效规范

> **适用版本**：HarmonyOS 6 / HarmonyOS NEXT

## 动效核心原则

| 原则 | 说明 |
|------|------|
| 有意义 | 动效服务于交互和信息传达，不是装饰 |
| 自然流畅 | 符合物理规律的运动轨迹 |
| 快速响应 | 交互反馈及时，减少等待感知 |
| 性能优先 | 避免复杂动画影响流畅度 |

---

## 动画类型

| 类型 | 说明 | 典型场景 |
|------|------|---------|
| 属性动画 | 绑定组件具体属性，属性变化自动触发 | 透明度、缩放、位置变化 |
| 转场动画 | 组件或页面切换时的过渡效果 | 页面跳转、模态框弹出/关闭 |
| 显式动画 | 通过代码显式触发和控制 | 复杂交互动效 |
| 微动效 | 细腻的视觉反馈增强体验 | 加载状态、hover 效果 |

---

## 时长规范

| 动画类型 | 推荐时长 |
|---------|---------|
| 快速反馈 | 100-200 ms |
| 通用过渡 | 300-500 ms |
| 强调动效 | 500-800 ms |
| 复杂转场 | 800-1200 ms |

**帧率**：推荐 60 FPS（1帧 ≈ 16.67ms）

---

## 动画曲线

### 推荐曲线

| 曲线名称 | 特点 | 适用场景 |
|---------|------|---------|
| Linear | 匀速 | 匀速运动，如进度条 |
| Ease | 自然加速减速 | 通用过渡 |
| Ease-in | 先慢后快 | 元素进入 |
| Ease-out | 先快后慢 | 元素退出 |
| Ease-in-out | 两端慢中间快 | 来回运动 |
| Fast-out-slow-in | 快速启动缓慢停止 | 自然物理感运动 |
| Friction | 摩擦阻尼感 | 弹性效果 |

---

## 动效设计要素

| 要素 | 说明 |
|------|------|
| 时长（Duration） | 动画持续时间，单位 ms |
| 曲线（Curve） | 动画速度变化曲线 |
| 延迟（Delay） | 动画启动前的等待时间 |
| 迭代（Iteration） | 动画重复次数 |

---

## 转场动效

### 常见转场场景

| 场景 | 说明 |
|------|------|
| 层级转场 | 页面层级间的导航 |
| 搜索转场 | 搜索结果切换 |
| 新建转场 | 新建页面滑入 |
| 编辑转场 | 编辑状态切换 |
| 通用转场 | 通用页面切换 |
| 跨应用转场 | 应用间跳转 |

### 转场设计要点

- 前后相邻界面的切换**必须**存在转场动效
- 避免一帧跳转（无过渡的直接切换）
- 转场时长建议 300-500ms
- 转场曲线建议使用 ease-in-out

---

## 微动效设计

| 类型 | 说明 |
|------|------|
| 加载动效 | 进度指示、骨架屏 |
| 反馈动效 | 点击反馈、状态切换 |
| 氛围动效 | 背景微妙变化 |

---

## 沉浸光感视效（API 23 新增）

HarmonyOS 6.1 新增「沉浸光感」材质效果，HDS 组件支持 `systemMaterialEffect`：

| 效果类型 | 说明 |
|---------|------|
| **AUTO（系统自适应）** | 系统根据设备算力自动选择（SMOOTH/EXQUISITE/GENTLE） |
| **SMOOTH** | 流畅效果，适合性能较低的设备 |
| **EXQUISITE** | 精致效果，适合高性能设备 |
| **GENTLE** | 温和效果，平衡体验 |

**系统自适应（推荐）**：
```typescript
// 自动适配性能和显示效果
HdsTabsFloatingStyle({
  systemMaterialEffect: 'AUTO'
});
```

**手动控制**：
```typescript
// 查询设备支持的材质类型
import { hdsMaterial } from '@hms.hds.hdsMaterial';
let types = hdsMaterial.getSystemMaterialTypes();
if (types.includes('IMMERSIVE')) {
  // 可选用 EXQUISITE 或 GENTLE
}
```

参考：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-hds-tabs-bar-floating

---

## 动效性能优化

| 要点 | 说明 |
|------|------|
| 减少重排 | 避免动画过程中触发布局重排 |
| GPU加速 | 优先使用 transform/opacity 等 GPU 加速属性 |
| 控制数量 | 同一界面避免过多同时播放的动画 |
| 降低复杂度 | 复杂动画考虑使用帧动画替代 |

---

## 官方动效规范

- 官方动效文档：https://developer.huawei.com/consumer/cn/doc/design-guides/animation-attributes-0000001797117229
- 动效使用指导：https://developer.huawei.com/consumer/cn/doc/best-practices/bpta-fair-use-animation
