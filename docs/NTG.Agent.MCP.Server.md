# NTG.Agent.MCP.Server

## Overview
Model Context Protocol (MCP) server that exposes reusable tools to AI agents. Tools are loaded dynamically from assembly and made available over HTTP transport.

## Tech Stack
- .NET 10.0 / ASP.NET Core
- ModelContextProtocol.AspNetCore v1.2.0

## Transport
HTTP-based MCP protocol — agents connect and invoke tools over standard HTTP.

## Registered Tools
Tools are loaded via `WithToolsFromAssembly()` from:
- `NTG.Agent.AITools.SearchOnlineTool` — Google Custom Search

## Configuration
```json
{
  "GoogleSearch": {
    "ApiKey": "<your-key>",
    "SearchEngineId": "<your-cx>"
  }
}
```

## Services
- `MonkeyService` — singleton utility service (registered in DI)

## How Agents Use This
The Orchestrator connects to the MCP Server at startup and makes tool definitions available to all configured agents. When an agent decides to call a tool (e.g., `search_online`), the Orchestrator forwards the call to this server.

## Dependencies (Project References)
- `NTG.Agent.AITools.SearchOnlineTool`
- `NTG.Agent.ServiceDefaults`

## Test Project
`NTG.Agent.MCP.Server.Tests` — NUnit + Moq
