# 智能体框架（Agent Framework Kit）

> **适用版本**：HarmonyOS 6.1 / API 23（稳定）。API 23 新增。
> **Kit 导入**：`@kit.AgentFrameworkKit`（HMAF — HarmonyOS Multi-Agent Framework）
> **官方文档**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-overview-V5

---

## 概述

Agent Framework Kit（HMAF）是 HarmonyOS 6.1 新增的智能体开发框架，提供 Agent 创建、Tool 定义、任务规划与执行、多 Agent 协作等能力。可与 IntentsKit 集成，实现智能体能力的意图分发与系统级调用。

### 核心能力

| 能力 | 说明 |
|------|------|
| Agent 创建 | 定义智能体角色、能力与行为 |
| Tool 定义 | 为 Agent 注册可调用的工具函数 |
| 任务规划 | 自动分解复杂任务为可执行步骤 |
| 任务执行 | 按规划逐步执行，支持异常重试 |
| 多 Agent 协作 | 多个 Agent 分工协作完成复杂任务 |
| IntentsKit 集成 | 通过意图框架实现系统级智能分发 |

---

## Agent 创建

### 定义 Agent

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

const weatherAgent: agentFramework.AgentDefinition = {
  name: 'WeatherAssistant',
  description: '提供天气查询与预报服务',
  capabilities: ['weather_query', 'forecast'],
  systemPrompt: '你是一个天气助手，帮助用户查询天气信息。'
};
```

### 注册 Agent

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function registerAgent(definition: agentFramework.AgentDefinition): Promise<string> {
  const agentId = await agentFramework.registerAgent(definition);
  return agentId;
}
```

### 注销 Agent

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function unregisterAgent(agentId: string): Promise<void> {
  await agentFramework.unregisterAgent(agentId);
}
```

---

## Tool 定义

### 定义工具

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

const weatherTool: agentFramework.ToolDefinition = {
  name: 'get_weather',
  description: '查询指定城市的当前天气',
  parameters: {
    type: 'object',
    properties: {
      city: {
        type: 'string',
        description: '城市名称'
      }
    },
    required: ['city']
  }
};
```

### 注册工具与实现

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function registerWeatherTool(agentId: string): Promise<void> {
  await agentFramework.registerTool(agentId, {
    definition: weatherTool,
    handler: async (params: Record<string, string>) => {
      const city = params['city'];
      const weatherData = await fetchWeatherFromApi(city);
      return {
        city: city,
        temperature: weatherData.temperature,
        condition: weatherData.condition
      };
    }
  });
}
```

### 批量注册工具

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function registerMultipleTools(agentId: string): Promise<void> {
  const tools: agentFramework.ToolRegistration[] = [
    {
      definition: {
        name: 'get_weather',
        description: '查询天气',
        parameters: {
          type: 'object',
          properties: { city: { type: 'string', description: '城市' } },
          required: ['city']
        }
      },
      handler: async (params) => fetchWeather(params['city'])
    },
    {
      definition: {
        name: 'get_forecast',
        description: '查询未来3天预报',
        parameters: {
          type: 'object',
          properties: { city: { type: 'string', description: '城市' } },
          required: ['city']
        }
      },
      handler: async (params) => fetchForecast(params['city'])
    }
  ];
  await agentFramework.registerTools(agentId, tools);
}
```

---

## 任务规划与执行

### 创建任务

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function createTask(agentId: string, userIntent: string): Promise<string> {
  const taskId = await agentFramework.createTask(agentId, {
    intent: userIntent,
    maxSteps: 10,
    timeout: 30000
  });
  return taskId;
}
```

### 执行任务

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function executeTask(taskId: string): Promise<agentFramework.TaskResult> {
  const result = await agentFramework.executeTask(taskId);
  return result;
}
```

### 监听任务进度

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

function subscribeTaskProgress(taskId: string): void {
  agentFramework.on('taskProgress', taskId, (event: agentFramework.TaskProgressEvent) => {
    console.info(`step=${event.currentStep} status=${event.status} tool=${event.toolName}`);
  });
}
```

### 取消任务

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function cancelTask(taskId: string): Promise<void> {
  await agentFramework.cancelTask(taskId);
}
```

---

## 多 Agent 协作

### 创建协作组

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function createCollaboration(agentIds: string[]): Promise<string> {
  const groupId = await agentFramework.createCollaboration({
    agents: agentIds,
    strategy: agentFramework.CollaborationStrategy.SEQUENTIAL,
    maxRounds: 5
  });
  return groupId;
}
```

### 执行协作任务

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

async function executeCollaboration(groupId: string, task: string): Promise<agentFramework.CollaborationResult> {
  const result = await agentFramework.executeCollaboration(groupId, {
    task: task,
    context: {}
  });
  console.info(`final answer=${result.finalAnswer} rounds=${result.rounds}`);
  return result;
}
```

### 协作策略

| 策略 | 说明 |
|------|------|
| SEQUENTIAL | Agent 按顺序依次执行 |
| PARALLEL | Agent 并行执行，结果汇总 |
| ROUTER | 主 Agent 路由任务到最合适的子 Agent |
| DEBATE | 多 Agent 辩论，综合得出最优结果 |

---

## 与 IntentsKit 集成

### 注册意图

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';
import { intentsKit } from '@kit.IntentsKit';

async function registerIntentForAgent(agentId: string): Promise<void> {
  await agentFramework.bindIntent(agentId, {
    intentName: 'query_weather',
    intentDescription: '用户想查询天气信息',
    intentPatterns: ['查天气', '今天天气怎么样', '明天会下雨吗'],
    intentCategory: intentsKit.IntentCategory.INFORMATION
  });
}
```

### 处理意图触发

```typescript
import { agentFramework } from '@kit.AgentFrameworkKit';

function setupIntentHandler(agentId: string): void {
  agentFramework.on('intentTriggered', agentId, async (event: agentFramework.IntentEvent) => {
    const taskId = await agentFramework.createTask(agentId, {
      intent: event.query,
      maxSteps: 5,
      timeout: 15000
    });
    const result = await agentFramework.executeTask(taskId);
    await agentFramework.replyIntent(event.intentId, {
      answer: result.output,
      confidence: result.confidence
    });
  });
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

> Agent Framework Kit 为 API 23 新增能力，需 HarmonyOS 6.1 及以上版本。与 IntentsKit 集成时，需在 AGC 控制台同时开通 IntentsKit 与 Agent Framework 能力。

---

## 官方参考

- **Agent Framework Kit 概述**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-overview-V5
- **Agent 创建指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-create-agent-V5
- **Tool 定义指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-tool-definition-V5
- **多 Agent 协作指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-collaboration-V5
- **IntentsKit 集成指南**：https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agent-framework-intents-integration-V5
- **API 参考**：https://developer.huawei.com/consumer/cn/doc/harmonyos-references/agent-framework-api-overview