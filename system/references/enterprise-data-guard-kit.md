# Enterprise Data Guard Kit（企业数据保护服务）

> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataguard-introduction

## 概述

Enterprise Data Guard Kit（企业数据保护服务）为企业安全管控类 MDM 应用提供关键信息资产（KIA）文件的识别、外发管控以及企业恢复密钥的管理能力。

## 核心能力

### 文件分级管控

- 扫描和分级标识功能
- 构建企业级资产地图
- 配置分级管控策略
- 灵活管控敏感文件外发权限

### 水印保护

基于策略和敏感文件清单，对文件外发等非法行为进行管控，打开时进行水印保护。

### 恢复密钥管理

提供企业恢复密钥的管理能力。

## 约束与限制

### 访问限制

文件扫描仅限于默认路径范围内的子目录，包括：

- `/data/service/el2/`
- `/data/app/el1~el5/`
- `/mnt/hmdfs/`

### 支持的国家/地区

当前仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。

### 支持的设备

PC/2in1（华为擎云系列）

## 模拟器支持情况

本 Kit 暂不支持模拟器。

## 相关 Kit

- MDM Kit：企业设备管理
- Core File Kit：文件管理
- Enterprise Space Kit：企业数字空间

## API 参考

| API | 说明 |
|-----|------|
| @ohos.enterpriseDataGuard | 企业数据保护 |
