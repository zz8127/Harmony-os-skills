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