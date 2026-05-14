# FAST Kit

## 概述

FAST Kit（算法加速服务）以理论计算机为基础，面向开发者提供算法加速能力。当前开放高阶数据结构（线段表、并发哈希表）、规划求解（矩形划分求解器）与数字信号处理（向量运算、二阶 IIR 滤波器）接口，支撑应用的开发体验和用户体验提升。

## 核心能力

### 高阶数据结构（Advanced Data Structure）

融合理论计算机科学中具有理论保证的高级数据结构与现代硬件特性。

#### 线段表（SegmentMap）

用于高效处理区间段信息的数据结构，支持数据序列区间段的快速更新和快速查询。

典型场景：
- 数据可视化：股票 K 线图标记价格/时间区间、甘特图/时间轴渲染
- 资源监控与日志分析：记录卡顿/异常时间区间、用户停留时间区间分析
- 游戏开发：管理持续生效的技能/状态、碰撞检测区间筛选

#### 并发哈希表（ConcurrentHashMap）

专为高并发场景设计的数据结构，支持多线程环境下安全高效的键值对插入、删除与查找。

典型场景：
- 分布式系统与中间件：分布式缓存集群键值管理、消息队列消费者偏移量维护
- 实时缓存与数据库：高频交易系统行情数据缓存、数据库连接池路由
- 网络与网关服务：API 网关 IP 限流计数、Web 服务器并发会话管理

### 规划求解（Solver）

将理论计算机科学与运筹学中的优化求解能力运用到鸿蒙生态各类场景。

#### 矩形划分求解器（RectPartition）

接收若干彼此不相交的矩形作为输入，计算覆盖相同区域的矩形划分方案，使输出矩形数量尽可能少。

典型场景：
- UI 渲染与布局优化：合并相邻 UI 控件背景减少 GPU 绘制调用、合并虚拟列表渲染区域
- 游戏开发：合并相邻地形/可通行区域优化碰撞检测、合并光照影响区域简化计算
- 文档与表格处理：自动合并相邻相同格式单元格、合并多个文本标注区域

### 数字信号处理（Digital Signal Processing）

提供高性能向量运算与二阶 IIR 滤波器能力，支持单精度和双精度算术运算。

#### 向量运算

高性能向量算术运算，支持加减乘除、点积、归一化等操作。

#### 二阶 IIR 滤波

二阶无限脉冲响应滤波器，支持低通/高通/带通滤波。

典型场景：
- 音频信号处理：降噪、均衡器、滤波、多通道音频处理
- 传感器数据分析：加速度计/陀螺仪数据滤波与特征提取
- 通信与信号分析：复数信号格式转换、向量点积、信号能量计算
- 机器学习推理：特征向量计算、向量归一化、统计特征提取

## 基本概念

**不透明配置（Opaque Configuration）**：一种 ABI 稳定的配置抽象机制，库以不完整类型前向声明配置对象，外部代码仅通过指针句柄进行传递与操作，对象的大小、字段布局及解释规则完全由库内部定义，将实现细节与调用者彻底隔离，保证后续版本可在不破坏二进制兼容性的前提下变更存储格式与语义。

## npm 包名

`@kit.FASTKit`

## 关键 API

| API | 说明 |
|---|---|
| SegmentMap | 线段表数据结构，区间段快速更新与查询 |
| ConcurrentHashMap | 并发哈希表，多线程安全键值操作 |
| RectPartition | 矩形划分求解器，最小化矩形数量 |
| 向量运算接口 | 高性能向量加减乘除、点积、归一化等 |
| 二阶 IIR 滤波接口 | 低通/高通/带通数字滤波 |

## 权限要求

无额外权限要求。

## 约束与限制

- 支持设备：Phone、Tablet、PC/2in1
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 支持模拟器（与真机存在通用差异）

## 官方链接

- [FAST Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-introduction)
- [使用 SegmentMap 查询维护区间信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-segment-map)
- [使用并发哈希表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-concurrent-hashmap)
- [矩形划分求解器](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-rect-partition)
- [向量运算](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-dsp-vector-calculation)
- [二阶 IIR 滤波](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/fast-dsp-iir-filter)
- [FAST API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/fast-kit-fast)
