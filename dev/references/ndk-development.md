# NDK 开发

## 概述

NDK（Native Development Kit）是HarmonyOS SDK提供的Native API、相应编译脚本和编译工具链的集合，方便开发者使用C或C++语言实现应用的关键功能。NDK只覆盖了HarmonyOS一些基础的底层能力，没有提供ArkTS/JS API的完整能力。

## 适用场景

### 适合使用NDK的场景

- 性能敏感的场景，如游戏、物理模拟等计算密集型场景
- 需要复用已有C或C++库的场景
- 需要针对CPU特性进行专项定制库的场景，如Neon加速

### 不建议使用NDK的场景

- 纯C或C++的应用
- 希望在尽可能多的HarmonyOS设备上保持兼容的应用

## 核心能力

### NDK常用模块

| 模块 | 说明 |
|---|---|
| 标准C库 | 基于musl提供的标准C库接口 |
| 标准C++库 | C++运行时库接口，提供C++运行时能力 |
| 日志 | 提供向系统输出HiLog日志接口 |
| Node-API | 支持ArkTS/JS和C/C++之间的交互接口 |
| FFRT | 基于任务的并发编程框架 |
| libuv | 第三方异步IO库 |
| zlib | 提供基础数据压缩与解压功能 |
| Rawfile | 提供访问应用内置资源的接口 |
| XComponent | ArkUI XComponent组件，提供surface与触屏事件等接口 |
| Drawing | 系统提供的2D图形库，支持在surface进行绘制 |
| OpenGL | 系统提供的OpenGL 3D图形接口 |
| OpenSL ES | 支持2D、3D音频加速的接口 |

## NDK目录结构

- **build目录**：放置预定义的toolchain脚本文件hmos.toolchain.cmake，CMake编译时通过CMAKE_TOOLCHAIN_FILE指定
- **build-tools文件夹**：放置NDK提供的编译工具（CMake 3.16.5等）
- **llvm文件夹**：放置NDK提供的编译器（Clang/LLVM）

## 前置知识

- Linux C语言编程知识（内核、libc基础库基于POSIX等标准扩展）
- CMake使用知识（HarmonyOS默认支持的构建系统）
- Node Addons开发知识（ArkTS采用Node-API作为跨语言调用接口）
- Clang/LLVM编译器使用知识
- Node-API（曾用名NAPI，基于Node.js的Node-API扩展而来，但不完全兼容）

## npm 包名

NDK不属于某个Kit，使用C/C++直接开发，通过Node-API与ArkTS交互。

## 关键 API

| API | 说明 |
|---|---|
| Node-API (napi) | ArkTS/JS与C/C++跨语言调用接口 |
| Drawing API | 2D图形绘制接口 |
| XComponent API | surface与触屏事件接口 |
| Rawfile API | 应用内置资源访问接口 |
| HiLog API | 系统日志输出接口 |
| FFRT API | 基于任务的并发编程框架接口 |

## 权限要求

无特殊权限要求，但Native代码受系统安全沙箱约束。

## 官方链接

- [NDK开发导读](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ndk-development-overview)
- [创建NDK工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/create-with-ndk)
- [NDK工程构建概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/build-with-ndk-overview)
- [Node-API简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/napi-introduction)
