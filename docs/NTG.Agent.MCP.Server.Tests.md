# NTG.Agent.MCP.Server.Tests

## Overview
Unit and integration test project for `NTG.Agent.MCP.Server` and its registered tools.

## Tech Stack
- NUnit 4.5.0
- Moq 4.20.72
- Coverlet 8.0.0 (code coverage)

## What's Tested
- MCP tool registration and discovery
- Tool invocation logic (inputs, outputs, error handling)
- `SearchOnlineTool` behavior (with mocked Google Search HTTP client)
- `MonkeyService` functionality

## Running Tests
```bash
dotnet test NTG.Agent.MCP.Server.Tests
```

With coverage:
```bash
dotnet test NTG.Agent.MCP.Server.Tests --collect:"XPlat Code Coverage"
```

## Dependencies (Project References)
- `NTG.Agent.MCP.Server`
