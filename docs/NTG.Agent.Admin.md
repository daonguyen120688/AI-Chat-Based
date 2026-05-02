# NTG.Agent.Admin

## Overview
Administration portal for managing agents, users, and system configuration. Restricted to users with the `Admin` role.

## Tech Stack
- .NET 10.0
- Blazor Server + WebAssembly (interactive components)
- BootstrapBlazor v10.5.0
- YARP Reverse Proxy v2.3.0
- ASP.NET Core Identity (SQL Server)

## Architecture
```
Admin Browser
  └── NTG.Agent.Admin (Blazor Server)
        ├── /api/* → YARP → NTG.Agent.Orchestrator
        └── Identity DB (SQL Server)
```

Interactive components live in `NTG.Agent.Admin.Client` (Blazor WASM).

## Authorization
- Requires `Admin` role (enforced via policy)
- Identity + SQL Server for admin accounts
- All admin API operations route through Orchestrator's `AgentAdminController`

## Key Features
- Agent CRUD (create, edit, delete, publish agents)
- Agent tool configuration (bind MCP tools to agents)
- User management
- System configuration
- Token usage reporting

## Routing
| Pattern | Destination |
|---|---|
| `/api/**` | Orchestrator API (YARP proxy) |
| `/**` | Blazor admin pages |

## Dependencies (Project References)
- `NTG.Agent.Admin.Client` (WASM project)
- `NTG.Agent.ServiceDefaults`

## Client Sub-project (`NTG.Agent.Admin.Client`)
- Blazor WASM interactive admin components
- References `NTG.Agent.Common` for shared DTOs
