# NTG.Agent.AITools.SearchOnlineTool

## Overview
MCP-compatible tool that enables AI agents to perform Google Custom Search queries for real-time online information retrieval.

## Tech Stack
- .NET 10.0
- ModelContextProtocol.AspNetCore v1.2.0
- Microsoft.SemanticKernel.Plugins.Web v1.72.0-alpha
- System.Memory.Data v10.0.5

## Structure
```
NTG.Agent.AITools.SearchOnlineTool/
├── SearchOnlineTool.cs    — MCP tool implementation
├── Services/              — HTTP search service wrappers
└── Enums/                 — Search result type enumerations
```

## Tool: `search_online`
Accepts a query string and returns ranked search results from Google Custom Search API.

**Input:** `{ "query": "string" }`  
**Output:** Array of search results with title, snippet, and URL.

## Configuration (via MCP Server)
| Key | Description |
|---|---|
| `GoogleSearch:ApiKey` | Google API key |
| `GoogleSearch:SearchEngineId` | Custom Search Engine (CX) ID |

## How It's Exposed
This library is loaded by `NTG.Agent.MCP.Server` via `WithToolsFromAssembly()`. The MCP server registers the tool over HTTP so any connected agent can call it.

## Dependencies (Project References)
Referenced by `NTG.Agent.MCP.Server`.
