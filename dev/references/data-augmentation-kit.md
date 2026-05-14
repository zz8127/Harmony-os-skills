# Data Augmentation Kit

## 概述

Data Augmentation Kit（数据增强套件）提供知识库、知识检索、RAG（检索增强生成）、端侧问答模型能力，打造个性化智慧数据平台，实现个性化智慧体验。

## 核心能力

### RAG（检索增强生成）

结合检索与生成技术的自然语言处理方案，通过动态从外部知识库中检索相关信息，辅助生成更准确、可靠的文本内容。

- 知识实时性：无需重新训练模型即可动态更新知识库，适用于新闻、政策等高频变化领域
- 可信度增强：生成内容基于检索结果，减少模型"幻觉"，支持答案溯源
- 灵活适配：同一模型可快速切换不同领域知识库，降低跨场景部署成本
- 长尾问题覆盖：通过外挂知识库补充模型未训练到的细分领域知识

### 智慧化数据检索

基于多路召回和重排序，提供知识检索框架。

- 智慧化数据构建：将应用数据通过加工转换为知识，存储在倒排数据库、向量数据库、图数据库等存储引擎中
- 智慧化数据检索：针对图片、文本等多种数据或多种数据库的融合查询，支持条件过滤、语义理解的复杂数据检索场景
- 基于RAG的知识问答：将检索和大模型生成技术结合，提高大模型回答问题的准确性

### 端侧问答模型

提供接入端侧模型问答的方法，以及使用鸿蒙AI模型管家对接LLM，实现数据不出端智能问答的效果。

- 数据处理不出端，用户安全隐私有保障

### 知识加工

将原始数据加工为结构化知识，支持文本拆分（chunk，默认3072字符/单元）、向量化、索引构建等流程。

## npm 包名

`@kit.DataAugmentationKit`

## 关键 API

| API | 说明 |
|---|---|
| RAG API | 检索增强生成，通过streamChat对用户问题解析，检索知识库后融合生成输出 |
| 智慧化数据检索 API（ArkTS） | 基于多路召回和重排序的检索框架 |
| 智慧化数据检索 API（C++） | C++版本的智慧化数据检索接口 |
| 端侧问答模型 API | 接入端侧模型进行本地问答 |
| 知识加工 API | 文本拆分、向量化、索引构建 |

## 基本概念

- **LLM**：Large Language Model（大语言模型），基于深度学习的AI模型，能理解和生成人类语言
- **chunk**：知识加工时文本被拆分后的逻辑或结构单元，默认包含3072个字符
- **检索召回**：通过特定策略或算法从海量数据中快速筛选出候选结果集

## 权限要求

无特殊权限要求，但需注意数据访问合规性。

## 约束与限制

- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- RAG：仅支持PC/2in1设备
- 智慧化数据检索：支持Phone、PC/2in1、Tablet设备
- 端侧问答模型：仅支持PC/2in1设备
- 暂不支持模拟器

## 官方链接

- [Data Augmentation Kit简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataaugmentation-introduction)
- [知识加工](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/data-augmentation-knowledge-processing)
- [RAG开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataaugmentation-rag)
- [智慧化数据检索](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataaugmentation-retrieval)
- [端侧问答模型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/dataaugmentation-localchatmodel)
