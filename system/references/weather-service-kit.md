# Weather Service Kit — 天气服务

> **适用版本**：HarmonyOS 6.0+。兼容 API 22+。

## 概述

Weather Service Kit（天气服务）是鸿蒙生态下的一个数据提供服务，融合了多家气象行业 TOP 供应商，提供专业、精准、稳定的超本地化天气预报服务，帮助开发者为用户提供更贴心的本地生活服务，支撑行业客户防灾减灾、降本增效。开发者可以轻松地在 HarmonyOS 应用/元服务中获取天气数据。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 天气预报 | 获取城市级和 POI 级天气预报，包括实况天气、48 小时逐小时预报（海外 24 小时）、10 日天气预报 |
| 分钟级降水预报 | 方圆 5km 范围内、未来 2 小时的分钟级降雨态势预报，包含降水形态、降水强度 |
| 天气预警 | 气象局实时发布的天气和环境预警信息 |
| 天气指数 | 未来 3 天的晾晒指数、穿衣指数、紫外线指数、路况指数、钓鱼指数等生活指数 |
| 天文数据 | 日出时间、日落时间、月出时间、月落时间、月相等数据 |
| 潮汐 | 全国主要港口和城市的潮汐数据 |

### 天气预报数据详情

- 天气状况
- 温度
- 风力
- 风向
- 湿度

---

## npm 包名

`@kit.WeatherServiceKit`

---

## 关键 API

| API | 说明 |
|-----|------|
| `weatherService` | 天气数据服务主模块 |
| 天气预报查询 | 获取城市级/POI 级天气预报数据 |
| 分钟降水查询 | 获取分钟级降水预报数据 |
| 天气预警查询 | 获取实时天气预警信息 |
| 天气指数查询 | 获取生活指数数据 |
| 天文数据查询 | 获取日出日落、月出月落等天文数据 |
| 潮汐数据查询 | 获取潮汐数据 |

---

## 权限要求

| 权限 | 说明 |
|------|------|
| `ohos.permission.GET_NETWORK_INFO` | 获取网络信息（系统授权） |
| `ohos.permission.APPROXIMATELY_LOCATION` | 获取粗略位置（用户授权），用于 POI 级天气查询 |

---

## 约束与限制

| 项目 | 说明 |
|------|------|
| 使用限制 | 当前仅面向系统应用开放，暂不对外开放 |
| 支持设备 | Phone、Tablet、PC/2in1、Wearable、TV |
| 模拟器 | 暂不支持模拟器 |

---

## 官方链接

- [Weather Service Kit 简介](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-introduction)
- [开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-preparations)
- [获取天气数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/weather-service-getweather)
- [weatherService API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/weather-service-weatherservice)
