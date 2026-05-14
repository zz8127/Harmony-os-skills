# Enterprise Threat Protection Kit

## 概述

Enterprise Threat Protection Kit（企业威胁防护服务）为企业开发者提供构建安全防护类应用的核心能力，核心在于文件访问与处置功能。通过对文件进行安全高效地扫描以识别潜在威胁，并对已识别的威胁文件执行隔离、恢复或删除等操作，实现从检测到处置的全流程防护，保护企业设备上的数据安全。

## 核心能力

### 文件扫描与威胁识别

启动应用目录文件扫描任务，打开设备文件进行安全扫描，识别潜在威胁文件。

### 文件隔离

将检测到的威胁文件安全转移至隔离区，防止威胁扩散。

### 文件隔离恢复

将误判文件从隔离区还原至原位置，支持误报恢复。

### 文件隔离删除

永久删除隔离区中的威胁文件，彻底清除威胁。

### 隔离文件查询

提供已隔离文件信息的查询功能，便于安全管理。

## 文件访问范围

| 目录 | 访问 | 处置 |
|---|---|---|
| 用户公共目录 | 支持 | 支持 |
| 云盘目录 | 支持（建议只访问本地文件） | 仅支持处置本地文件 |
| 外卡目录 | 支持 | 不支持处置，建议调用方自行处置 |
| 应用 el2 级别加密数据目录 | 支持 | 支持 |
| 应用安装包目录 | 仅支持调试类型应用及企业应用 | 不支持处置，建议通过应用运行禁止名单或卸载应用方式处置 |

## npm 包名

`@kit.EnterpriseThreatProtectionKit`

## 关键 API

| API | 说明 |
|---|---|
| 文件扫描接口 | 启动应用目录文件扫描任务 |
| 文件打开接口 | 打开指定文件进行安全扫描 |
| 文件隔离接口 | 将威胁文件转移至隔离区 |
| 文件恢复接口 | 将误判文件从隔离区还原 |
| 文件删除接口 | 永久删除隔离区中的威胁文件 |
| 隔离查询接口 | 查询已隔离文件信息 |

## 权限要求

| 权限 | 说明 |
|---|---|
| `ohos.permission.SCAN_REMEDIATE_VIRUS` | 文件访问与处置权限，仅面向企业杀毒软件开放申请 |

在 module.json5 中声明：

```json
{
  "requestPermissions": [
    {
      "name": "ohos.permission.SCAN_REMEDIATE_VIRUS"
    }
  ]
}
```

## 约束与限制

- 仅适用于 PC/2in1 设备
- 仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）
- 访问和处置操作受限于应用类型，需确保应用为调试类型或企业应用
- 暂不支持模拟器
- 需完成企业开发者实名认证、申请企业应用发布证书和 Profile

## 官方链接

- [Enterprise Threat Protection Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/enterprisethreatprotection-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/enterprisethreatprotection-prepare)
- [文件访问与处置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nterprisethreatprotection-virusremediation-content)
- [文件隔离](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/nterprisethreatprotection-virusremediation-isolate)
- [常见问题](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/terprisethreatprotection-virusremediation-question)
