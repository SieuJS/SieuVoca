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
flowchart TD
    A[Repo doc] --> B[Linear task and acceptance criteria]
    B --> C[Branch with issue ID]
    C --> D[Code and local tests]
    D --> E[Draft PR and CI]
    E --> F{CI passes?}
    F -->|No| D
    F -->|Yes| G[Human review and smoke test]
    G -->|Changes| D
    G -->|Approve| H[Merge]
    H --> I[Post-merge check]
    I --> J[Linear: Done]
```
