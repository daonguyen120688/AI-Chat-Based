# NTG.Agent.ServiceDefaults

## Overview
Shared infrastructure library applied to every ASP.NET Core service in the solution. Provides consistent observability, resilience, and service discovery configuration via a single `AddServiceDefaults()` extension call.

## Tech Stack
- .NET 10.0
- OpenTelemetry v1.15.0
- Microsoft.Extensions.Http.Resilience v10.4.0
- Microsoft.Extensions.ServiceDiscovery v10.4.0

## What It Configures

### OpenTelemetry
| Signal | Instrumentation |
|---|---|
| Traces | ASP.NET Core, HTTP Client |
| Metrics | ASP.NET Core, HTTP Client, .NET Runtime |
| Exporter | OTLP → Aspire Dashboard |

### HTTP Resilience
- Retry policies with exponential backoff
- Circuit breaker on outbound HTTP clients
- Applied automatically to all `IHttpClientFactory` registrations

### Service Discovery
- Resolves logical service names (e.g., `https://orchestrator`) to actual endpoints
- Works with Aspire's built-in DNS-based discovery

## Usage
Call once in each service's `Program.cs`:
```csharp
builder.AddServiceDefaults();
// ...
app.MapDefaultEndpoints(); // maps /health and /alive
```

## Applied To
All five runnable services:
- `NTG.Agent.Orchestrator`
- `NTG.Agent.Knowledge`
- `NTG.Agent.MCP.Server`
- `NTG.Agent.WebClient`
- `NTG.Agent.Admin`

## Dependencies
No project references — pure NuGet dependencies only.
