# NTG.Agent.WebClient

## Overview
Blazor-based web frontend for end users. Provides the interactive AI chat experience, conversation management, and document uploads. Proxies API calls to the Orchestrator via YARP.

## Tech Stack
- .NET 10.0
- Blazor Server + WebAssembly (interactive components)
- BootstrapBlazor v10.5.0
- YARP Reverse Proxy v2.3.0
- ASP.NET Core Identity (SQL Server)

## Architecture
```
Browser
  └── WebClient (Blazor Server)
        ├── /api/* → YARP → NTG.Agent.Orchestrator
        └── Identity DB (SQL Server)
```

Interactive Blazor WASM components are hosted in `NTG.Agent.WebClient.Client`.

## Authentication
- ASP.NET Core Identity with SQL Server storage
- Identity cascade auth state passed to Blazor components
- Users must authenticate to access full functionality (anonymous sessions have limited quota)

## Key Features
- Real-time streaming chat (SSE / IAsyncEnumerable)
- Conversation history with pagination
- Document management UI
- Markdown rendering (BootstrapBlazor.Markdown)
- Responsive UI via BootstrapBlazor component library

## Routing
| Pattern | Destination |
|---|---|
| `/api/**` | Orchestrator API (YARP proxy) |
| `/**` | Blazor pages |

## Dependencies (Project References)
- `NTG.Agent.WebClient.Client` (WASM project)
- `NTG.Agent.ServiceDefaults`

## Client Sub-project (`NTG.Agent.WebClient.Client`)
- Blazor WASM interactive components
- References `NTG.Agent.Common` for shared DTOs
