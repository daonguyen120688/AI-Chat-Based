# NTG.Agent.Orchestrator

## Overview
Main REST API backend that orchestrates multi-agent AI conversations. Supports multiple LLM providers, streaming responses, document management, and anonymous/authenticated user sessions.

## Tech Stack
- .NET 10.0 / ASP.NET Core
- Entity Framework Core 10.0.5 + SQL Server
- Anthropic v12.11.0 (Claude)
- Azure.AI.OpenAI v2.8.0-beta
- Microsoft.Agents.AI v1.0.0
- Microsoft.KernelMemory.WebClient (RAG access)
- ModelContextProtocol.AspNetCore v1.2.0
- OpenTelemetry (traces + metrics)

## Controllers

| Controller | Responsibility |
|---|---|
| `AgentsController` | Streaming chat via agents; list published agents |
| `ConversationsController` | CRUD conversations with pagination |
| `DocumentsController` | Document upload and management |
| `AgentAdminController` | Admin agent CRUD |
| `TagsController` | Tag management |
| `FoldersController` | Folder organization |
| `SharedConversationsController` | Conversation sharing |
| `TokenUsageController` | Token consumption tracking |
| `PreferencesController` | User preferences |
| `FeaturesController` | Feature flags |
| `ErrorController` | Error handling |

## Key Services

| Service | Responsibility |
|---|---|
| `AgentService` | Multi-turn conversations; streaming; anonymous rate limits |
| `AgentFactory` | Creates agents for: GitHub, Gemini, OpenAI, AzureOpenAI, Anthropic |
| `KernelMemoryKnowledge` | RAG via Kernel Memory HTTP client |
| `IUserMemoryService` | Persistent conversation memory |
| `IDocumentAnalysisService` | Document parsing via Azure Form Recognizer |
| `ITokenTrackingService` | Token usage monitoring |
| `IAnonymousSessionService` | Anonymous user session management |

## Database Models (AgentDbContext)

- **Conversations** + **ChatMessages** (with sharing)
- **Agents** + **AgentTools** (multi-provider config)
- **Documents**, **Folders**, **Tags**, **DocumentTags**
- **User**, **Role**, **UserRole** (Identity)
- **UserPreferences**, **TokenUsage**
- **AnonymousSessions** (rate limiting)

## Anonymous User Limits
- 10 messages per session
- 50 messages per IP per day
- Sessions expire on configurable schedule

## Observability
- Custom metrics: `agent_interactions_total`, `agent_response_time_seconds`
- Traces exported to Aspire Dashboard via OTLP
- Service name: `Orchestrator`

## Key Configuration
```json
{
  "LongTermMemory": { "ConfidenceThreshold": 0.7, "MaxRetrievalCount": 5 },
  "AnonymousUser": { "MessagesPerSession": 10, "MessagesPerIpPerDay": 50 }
}
```

## Dependencies (Project References)
- `NTG.Agent.AITools.SimpleTools`
- `NTG.Agent.ServiceDefaults`
- `NTG.Agent.Common`
