# NTG.Agent.Orchestrator.Tests

## Overview
Unit and integration test project for `NTG.Agent.Orchestrator`. Covers entity models, services, and controllers.

## Tech Stack
- NUnit 4.5.0
- Moq 4.20.72
- Microsoft.EntityFrameworkCore.InMemory (in-memory DB for tests)
- Coverlet 8.0.0 (code coverage)

## Test Categories

| Folder | What's Tested |
|---|---|
| `Entity/` | EF Core entity validation, relationship constraints |
| `Services/` | Business logic: AgentService, TokenTracking, AnonymousSession, etc. |
| `Controllers/` | HTTP layer: request routing, response codes, model binding |

## Conventions
- Test classes mirror the source namespace (e.g., `AgentServiceTests` tests `AgentService`)
- DB-dependent tests use `InMemoryDatabase` — no SQL Server required
- External dependencies (HTTP clients, external APIs) are mocked via Moq

## Running Tests
```bash
dotnet test NTG.Agent.Orchestrator.Tests
```

With coverage:
```bash
dotnet test NTG.Agent.Orchestrator.Tests --collect:"XPlat Code Coverage"
```

## Dependencies (Project References)
- `NTG.Agent.Orchestrator`
- `NTG.Agent.Common`
