# 游戏服务（Game Service Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。兼容 API 14+。
> **Kit 导入**：`@kit.GameServiceKit`
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-overview-V5

---

## 概述

Game Service Kit 为游戏开发者提供成就、排行榜、游戏存档（云存档）、防沉迷、游戏事件等基础能力，帮助游戏快速接入华为游戏生态，提升玩家留存与活跃度。

### 核心能力

| 能力 | 说明 |
|------|------|
| 成就系统 | 定义/解锁/展示游戏成就 |
| 排行榜 | 全球/社交排行榜，实时排名 |
| 游戏存档 | 云端存档，多设备同步 |
| 防沉迷 | 实名认证与时长限制 |
| 游戏事件 | 自定义事件上报与分析 |

---

## 成就系统

### 前置条件

1. 在 AGC 控制台开通 Game Service 并配置成就
2. 定义成就列表（ID、名称、图标、解锁条件）
3. 玩家登录华为账号

### 成就列表与解锁

```typescript
import { gameService } from '@kit.GameServiceKit';

async function loadAchievements(): Promise<void> {
  const achievements = await gameService.getAchievementList();
  for (const item of achievements) {
    console.info(`id=${item.id} name=${item.name} state=${item.state}`);
  }
}

async function unlockAchievement(achievementId: string): Promise<void> {
  await gameService.revealAchievement(achievementId);
  await gameService.unlockAchievement(achievementId);
}

async function incrementAchievement(achievementId: string, step: number): Promise<void> {
  await gameService.incrementAchievement(achievementId, step);
}
```

### 成就展示 UI

```typescript
import { gameService } from '@kit.GameServiceKit';

async function showAchievementsUI(): Promise<void> {
  await gameService.showAchievementsUI(getContext(this));
}
```

---

## 排行榜

### 提交分数

```typescript
import { gameService } from '@kit.GameServiceKit';

async function submitScore(leaderboardId: string, score: number): Promise<void> {
  await gameService.submitScore(leaderboardId, score);
}
```

### 获取排名数据

```typescript
import { gameService } from '@kit.GameServiceKit';

async function getLeaderboardData(leaderboardId: string): Promise<void> {
  const scores = await gameService.getLeaderboardScores({
    leaderboardId: leaderboardId,
    timeSpan: gameService.TimeSpan.DAILY,
    maxResults: 10,
    isSocial: false
  });
  for (const entry of scores) {
    console.info(`rank=${entry.rank} score=${entry.score} displayName=${entry.displayName}`);
  }
}
```

### 排行榜展示 UI

```typescript
import { gameService } from '@kit.GameServiceKit';

async function showLeaderboardUI(leaderboardId: string): Promise<void> {
  await gameService.showLeaderboardUI(getContext(this), {
    leaderboardId: leaderboardId,
    timeSpan: gameService.TimeSpan.ALL_TIME
  });
}
```

---

## 游戏存档（云存档）

### 提交存档

```typescript
import { gameService } from '@kit.GameServiceKit';

async function saveGameArchive(description: string, data: string, coverUri: string): Promise<void> {
  await gameService.commitArchive({
    description: description,
    playedTime: 3600,
    progress: 50,
    coverUri: coverUri,
    archiveData: data
  });
}
```

### 读取存档

```typescript
import { gameService } from '@kit.GameServiceKit';

async function loadGameArchive(): Promise<void> {
  const archives = await gameService.getArchiveList({
    maxResults: 5
  });
  if (archives.length > 0) {
    const detail = await gameService.getArchiveDetail(archives[0].id);
    console.info(`data=${detail.archiveData} progress=${detail.progress}`);
  }
}
```

### 存档选择 UI

```typescript
import { gameService } from '@kit.GameServiceKit';

async function showArchiveUI(): Promise<void> {
  const selected = await gameService.showArchiveUI(getContext(this), {
    maxResults: 5,
    allowAdd: true,
    allowDelete: true
  });
  if (selected) {
    const detail = await gameService.getArchiveDetail(selected.id);
    console.info(`selected archive: ${detail.description}`);
  }
}
```

---

## 防沉迷

### 检查玩家状态

```typescript
import { gameService } from '@kit.GameServiceKit';

async function checkAntiAddiction(): Promise<void> {
  const status = await gameService.getAntiAddictionStatus();
  if (status.isRestricted) {
    console.info(`remainingTime=${status.remainingPlayTime} ageGroup=${status.ageGroup}`);
  }
}
```

### 防沉迷回调监听

```typescript
import { gameService } from '@kit.GameServiceKit';

function registerAntiAddictionListener(): void {
  gameService.on('antiAddictionEvent', (event) => {
    if (event.type === gameService.AntiAddictionEventType.TIME_LIMIT) {
      console.info(`play time limit reached, remaining=${event.remainingTime}`);
    } else if (event.type === gameService.AntiAddictionEventType.KICK_OFF) {
      console.info('player kicked off due to restriction');
    }
  });
}
```

---

## 游戏事件

### 上报自定义事件

```typescript
import { gameService } from '@kit.GameServiceKit';

async function reportGameEvent(eventId: string, params: Record<string, Object>): Promise<void> {
  await gameService.reportGameEvent(eventId, params);
}
```

---

## Game Controller Kit（游戏控制器服务）

### 概述

Game Controller Kit 支持游戏适配控制器外设（当前仅支持手柄），解决玩家操控性问题，保障用户体验。游戏开发者可通过接入该服务轻松实现游戏外设的上下线和按键及轴事件监听等功能。

### 核心能力

| 能力 | 说明 |
|------|------|
| 监听设备上下线 | 监听手柄等外设的连接与断开，查询所有在线设备的具体信息 |
| 监听按键和轴事件 | 监听游戏手柄的轴和按键事件，实现精准操控 |

### 开发方式

- 当前仅支持 C/C++ 接口
- 监听设备上下线：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-controller-monitor-device
- 监听手柄轴和按键事件：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-controller-monitor-pad

---

## 联机对战服务

### 概述

联机对战服务为多人联机游戏提供了房间管理、玩家匹配、队伍管理、消息通信等功能，具备优质的联网和服务端能力。游戏只需接入 SDK 即可快速实现多人联机对战，提升游戏体验，降低开发成本。

### 适用游戏类型

- 回合制（棋牌类）
- 实时对战（休闲对战、MOBA、FPS 类）

### 核心能力

| 能力 | 说明 |
|------|------|
| 房间管理 | 提供联机对战承载容器，支持加入房间、更新状态与属性、发送消息、离开/解散房间 |
| 玩家匹配 | 支持自定义匹配规则，提供房间匹配、在线匹配和组队匹配三种方式，支持自动填充机器人 |
| 队伍管理 | 支持组队匹配、离开队伍、解散队伍 |
| 消息通信 | 帧同步 + 帧数据存储与查询 + 端侧通信与交互，支持自动补帧 |
| 托管代码到实时服务器 | 支持在实时服务器调试、部署并运行游戏逻辑代码 |

### SDK 支持

| SDK 类型 | 支持平台 |
|---------|---------|
| JS SDK | HarmonyOS NEXT、Android、iOS、Web、华为快游戏、微信小游戏、字节跳动小游戏、macOS |
| C# SDK | HarmonyOS NEXT、Android、iOS、Windows、macOS、WebGL |

### 实现流程

1. 在 AGC 控制台开通服务
2. 配置服务（解散重连策略、匹配规则、帧同步管理、实时服务器托管）
3. 集成 SDK（JS / C#）
4. 初始化 SDK
5. 功能开发（创建/加入房间、匹配、帧同步、消息通信等）

### 关键概念

| 概念 | 说明 |
|------|------|
| 帧同步 | 客户端发送帧数据到服务器，服务器汇总后广播给所有客户端，支持补帧。通信协议支持 WebSocket 和 UDP |
| MOBA | 多人在线战术竞技类游戏 |
| FPS | 第一人称射击类游戏 |

---

## 游戏多媒体服务

### 概述

游戏多媒体服务是华为游戏中心推出的快速实现游戏内实时语音、实时信令（RTM）、语音消息等功能的服务。集成 SDK 即可为游戏提供实时语音对讲、全局聊天、语音/文本消息、语音转文本等能力。

### 核心能力

| 能力 | 说明 | SDK 支持 |
|------|------|---------|
| 实时语音 | 房间及语音管理，支持范围语音、3D 音效、语音变声 | HarmonyOS NEXT、Android、iOS、C#（Native） |
| RTM（实时信令） | 文本消息和二进制消息收发，实现实时通信、全局聊天、游戏通知、指令同步 | HarmonyOS NEXT、Android、iOS、JS（小游戏）、C#（Native/小游戏）、REST API |
| 语音消息 | 录制与播放语音消息，支持变声效果 | HarmonyOS NEXT、Android、iOS、JS（小游戏）、C#（Native/小游戏） |
| 效果音播放 | 简短音效播放与音量系数管理 | HarmonyOS NEXT、Android、iOS、C#（Native） |
| 语音转文本 | 语音转录成文本，用于语音输入场景 | HarmonyOS NEXT、Android、iOS、JS（小游戏）、C#（Native/小游戏） |
| 内容送检 | 内容检测能力，支持人工复审 | HarmonyOS NEXT、Android、iOS、Web、JS（小游戏）、C#（Native/小游戏） |

### 实现流程

1. 在 AGC 控制台开通游戏多媒体服务
2. 配置服务（语音转文本、安全加固、内容检测等可选功能）
3. 集成 SDK（HarmonyOS NEXT / Android / iOS / Web / C# 等）
4. 功能开发（实时语音、RTM、语音消息等）

### 关键概念

| 概念 | 说明 |
|------|------|
| 房间 | 音频空间，同一房间内的玩家可互相发送/接收实时音频数据 |
| 范围语音 | 在范围语音房间内，通过设置语音接收范围和上报位置信息，与一定距离内的玩家实时语音通话 |
| 3D 音效 | 将无方位感的声音进行方位和距离衰减渲染，增强沉浸感 |
| 频道 | 信令通道，用于玩家之间的实时消息通讯 |

---

## 权限配置

```json5
// module.json5
{
  "requestPermissions": [
    {
      "name": "ohos.permission.INTERNET"
    }
  ]
}
```

> Game Service Kit 依赖华为账号登录，需确保已集成华为账号服务。

---

## 官方参考

- **Game Service Kit 概述**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-overview-V5
- **成就开发指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-achievement-V5
- **排行榜开发指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-leaderboard-V5
- **游戏存档开发指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-archive-V5
- **防沉迷开发指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-service-anti-addiction-V5
- **API 参考**：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/game-service-api-overview
- **Game Controller Kit 简介**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/game-controller-introduction
- **联机对战服务简介**：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gameobe-introduction-0000001185429290
- **游戏多媒体服务简介**：https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/gamemme-introduction-0000001226565909
