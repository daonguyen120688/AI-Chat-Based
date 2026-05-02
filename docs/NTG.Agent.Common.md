# NTG.Agent.Common

## Overview
Shared class library containing DTOs, constants, and enumerations used across all projects in the solution. Has no external NuGet dependencies.

## Structure

```
NTG.Agent.Common/
├── Dtos/
│   ├── Agents/          — Agent and AgentTool DTOs
│   ├── Chats/           — Chat message request/response
│   ├── Conversations/   — Conversation list/detail
│   ├── Documents/       — Document upload/metadata
│   ├── Folders/         — Folder hierarchy
│   ├── Tags/            — Tag management
│   ├── UserPreferences/ — User settings
│   ├── TokenUsage/      — Token consumption records
│   ├── AnonymousSessions/ — Session state
│   ├── Tools/           — MCP tool descriptors
│   └── Upload/          — File upload contracts
├── Constants/
│   ├── Pagination        — Default page sizes
│   └── Auth              — Role names, claim types
└── Enums/               — Shared enumerations
```

## Usage
Referenced by:
- `NTG.Agent.Orchestrator` (server-side)
- `NTG.Agent.WebClient.Client` (WASM)
- `NTG.Agent.Admin.Client` (WASM)
- `NTG.Agent.Orchestrator.Tests`

Because this library is referenced by WASM client projects, it must remain compatible with the **browser runtime** — no server-only APIs (file system, environment variables, etc.).

## Dependencies
- `Microsoft.Extensions.Logging.Abstractions` only
