# NTG.Agent.AppHost

## Overview
.NET Aspire orchestration host. Defines all services, their dependencies, startup order, and inter-service communication for the entire solution.

## Tech Stack
- .NET Aspire Hosting v13.2.1

## Service Dependency Graph
```
AppHost
├── NTG.Agent.Knowledge       (independent — starts first)
├── NTG.Agent.MCP.Server      (independent — starts first)
└── NTG.Agent.Orchestrator    (depends on Knowledge + MCP Server)
    ├── NTG.Agent.WebClient   (waits for Orchestrator)
    └── NTG.Agent.Admin       (waits for Orchestrator)
```

## What Aspire Provides
- **Service Discovery** — services reference each other by logical name
- **Observability Dashboard** — traces, metrics, logs aggregated in one UI
- **Configuration Injection** — connection strings and URLs injected at runtime
- **Health Monitoring** — startup probes per service

## Configuration
All services are declared as `ExternalHttpEndpoint` resources. OTEL exporter endpoints are auto-configured by Aspire when running locally.

## Usage
```bash
# Run the full solution locally
dotnet run --project NTG.Agent.AppHost
```

The Aspire Dashboard will be available at `https://localhost:17149` (or the configured port).

## Notes
- Only used for **local development** and **Aspire-based deployments**
- For standalone deployment, each service can be run independently
- `NTG.Agent.ServiceDefaults` must be applied to each service for full Aspire integration
