# NTG.Agent Solution

Multi-agent AI chat platform built on .NET 10 and Aspire. Supports multiple LLM providers, RAG-based knowledge retrieval, extensible tools via MCP, and both authenticated and anonymous user sessions.

## Projects

| Project | Type | Purpose |
|---|---|---|
| [NTG.Agent.Orchestrator](NTG.Agent.Orchestrator.md) | API | Main REST API; agent orchestration; streaming chat |
| [NTG.Agent.Knowledge](NTG.Agent.Knowledge.md) | Service | Kernel Memory RAG service; document ingestion & search |
| [NTG.Agent.MCP.Server](NTG.Agent.MCP.Server.md) | Service | Model Context Protocol tool server |
| [NTG.Agent.WebClient](NTG.Agent.WebClient.md) | UI | Blazor user-facing chat application |
| [NTG.Agent.Admin](NTG.Agent.Admin.md) | UI | Blazor admin portal (agent/user management) |
| [NTG.Agent.AppHost](NTG.Agent.AppHost.md) | Infra | .NET Aspire orchestration host |
| [NTG.Agent.ServiceDefaults](NTG.Agent.ServiceDefaults.md) | Shared | OpenTelemetry, resilience, service discovery |
| [NTG.Agent.Common](NTG.Agent.Common.md) | Shared | DTOs, constants, enums |
| [NTG.Agent.AITools.SimpleTools](NTG.Agent.AITools.SimpleTools.md) | Library | DateTime and basic utility tools |
| [NTG.Agent.AITools.SearchOnlineTool](NTG.Agent.AITools.SearchOnlineTool.md) | Library | Google Custom Search MCP tool |
| [NTG.Agent.Orchestrator.Tests](NTG.Agent.Orchestrator.Tests.md) | Tests | Orchestrator unit + integration tests |
| [NTG.Agent.MCP.Server.Tests](NTG.Agent.MCP.Server.Tests.md) | Tests | MCP Server tests |

## Architecture

```
[Browser] → WebClient (Blazor + YARP) ──┐
[Admin]   → Admin    (Blazor + YARP) ──┤
                                        ▼
                              NTG.Agent.Orchestrator
                             /          |          \
                    Knowledge        MCP Server   AgentFactory
                   (RAG/KM)        (Tools/MCP)  (LLM Providers)
```

## LLM Providers Supported
GitHub Models · Google Gemini · OpenAI · Azure OpenAI · Anthropic (Claude)

## Quick Start
```bash
dotnet run --project NTG.Agent.AppHost
```
