# NTG.Agent.Knowledge

## Overview
Kernel Memory service responsible for document ingestion, text chunking, embedding generation, and semantic search (RAG). Consumed by the Orchestrator via HTTP client.

## Tech Stack
- .NET 10.0 / ASP.NET Core
- Microsoft.KernelMemory.Service.AspNetCore v0.98.250508.3
- Microsoft.SemanticKernel.Core v1.74.0

## Endpoints
| Path | Purpose |
|---|---|
| `/` | Service status |
| `/health` | Health check |
| `/swagger` | API docs (configurable) |

## Ingestion Pipeline
Steps executed per document:
1. `TextExtraction` — extract raw text
2. `TextPartitioning` — chunk into segments (max 1000 tokens, 100-token overlap)
3. `GenerateEmbeddings` — embed chunks
4. `SaveRecords` — persist to vector store
5. `Summarization` — optional summary
6. `DeleteDocument` — cleanup handler

Orchestration: `SimpleQueues` (in-memory; swap for durable queues in production)

## Storage Backends

| Type | Default | Alternatives |
|---|---|---|
| Vector Store | SimpleVectorDb (volatile) | AzureAISearch, Qdrant, Postgres, Redis, SqlServer |
| Document Store | SimpleFileStorage (volatile) | AzureBlobs, AWSS3 |

## AI Provider Support
- Anthropic (`claude-3-haiku`) — embeddings + generation
- AzureOpenAI
- OpenAI
- Ollama / LlamaSharp (local models)

## Search Configuration
- Max matches per query: 100
- Answer token limit: 300
- Moderation: AzureAIContentSafety (configurable)

## Security
- Optional API key authentication
- Content safety moderation pipeline

## Dependencies (Project References)
- `NTG.Agent.ServiceDefaults`
