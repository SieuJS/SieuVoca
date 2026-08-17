---
title: "Architecture Summary"
sidebarTitle: "Architecture Summary"
description: "Compact system, microservice, application, and delivery workflow diagrams."
---

# Architecture Summary

A compact map of the IELTS extension system. See [System Architecture](./system-architecture.md), [Backend Clean Architecture](./backend-clean-architecture.md), [Microservices Architecture](./microservices-architecture.md), and [Workflow](../../workflow/index.md) for details.

## System Architecture

```mermaid
flowchart LR
    EXT[Chrome Extension] --> GW[API Gateway]
    WEB[Website] --> GW
    GW --> SYNC[Extension Sync API]
    GW --> WEBAPI[Website API]
    SYNC --> SVC[Domain Services]
    WEBAPI --> SVC
    SVC <--> EVT[(Events)]
    SVC --> DATA[(Service-owned Data)]
    SVC --> PROVIDERS[Dictionary, AI, Speech]
    OBS[Logs, Traces, Health] -.-> GW
    OBS -.-> SVC
```

## Microservices

```mermaid
flowchart LR
    ID[Identity Profile] --> EVT[(Event Bus)]
    PC[Practice Capture] --> EVT
    VOC[Vocabulary] --> DICT[Dictionary]
    VOC --> EVT
    DICT --> EVT
    REV[Review] --> EVT
    PARSER[Parser Health] --> EVT
    EVT --> REV
    EVT --> DASH[Dashboard Analytics]
    DICT --> AI[AI Speech]
    REV --> AI
```

## Application Workflow

```mermaid
flowchart LR
    A[Practice] --> B[Capture word, context, unsure]
    B --> C[Save locally]
    A --> D[Submit test]
    D --> E[Validate and capture result]
    E --> C
    C --> F{Connected?}
    F -->|Yes| G[Background sync]
    F -->|No| H[Keep local]
    H --> I[Connect later]
    I --> G
    G --> J[Website]
    J --> K[Vocabulary review]
    J --> L[Scores and mistakes]
```

## Code And Task Workflow

```mermaid
flowchart LR
    A[Scope change] --> B[Update repo doc]
    B --> C[Linear task if needed]
    C --> D[Implement change]
    D --> E[Run tests]
    E --> F[Open pull request]
    F --> G{Approved?}
    G -->|No| D
    G -->|Yes| H[Merge and publish]
    B -->|If affected| I[Update Mintlify and/or Penpot]
    I --> F
    A -. small-change exception .-> D
```
