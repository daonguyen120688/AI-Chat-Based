# NTG.Agent.AITools.SimpleTools

## Overview
Lightweight class library providing basic utility tools for AI agents. No external NuGet dependencies — pure .NET only.

## Tools

### `DateTimeTools`
Provides date and time utilities that agents can call during conversations.

| Tool | Description |
|---|---|
| Get current date/time | Returns current UTC and local date/time |

## Usage
Referenced directly by `NTG.Agent.Orchestrator` and registered into the agent pipeline at startup. Tools are exposed to agents as callable functions during conversation processing.

## Design
- No MCP dependency — tools are registered natively into the Microsoft.Agents.AI pipeline
- Stateless: all tools are pure functions with no side effects
- Expand this library by adding new static tool classes

## Adding a New Tool
1. Create a new class in this project
2. Annotate methods with the appropriate agent tool attributes
3. No registration needed — the Orchestrator scans the assembly at startup

## Dependencies (Project References)
None — referenced by `NTG.Agent.Orchestrator`.
