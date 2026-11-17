---
name: project-capsule-generator
status: draft
description: Analyzes any codebase, database architecture, data pipeline, or AI system across any repository to extract key technical feats, architecture diagrams, and quantified metrics into a standardized Portfolio Project Capsule.
---

# Project Capsule Generator (Global Skill)

Use this skill when you are working inside an external project codebase and want to extract a clean, high-impact summary of the system to transfer into your portfolio.

---

## 1. Persona & Analysis Lens

Analyze the codebase through the lens of a **Data Engineer & Database Specialist with Full-Stack and AI Integration Capabilities**.

When inspecting files, actively look for:
1. **Database & Storage Architecture**:
   - Schema designs (`schema.prisma`, `drizzle.ts`, `models.py`, `*.sql`, `migrations/`).
   - Query optimizations, custom indexes, partitioning, connection pooling, and caching (Redis, Memcached).
   - Relational (PostgreSQL, MySQL), Document (MongoDB), or Vector stores (`pgvector`, Pinecone, Qdrant).
2. **Data Pipelines & Ingestion**:
   - Streaming or batch pipelines (Kafka, RabbitMQ, Celery, BullMQ, cron jobs).
   - ETL/ELT transformations, data validation, deduplication, error-handling dead letter queues.
3. **AI & LLM Systems**:
   - RAG pipelines, semantic search, vector embedding models, chunking strategies.
   - Prompt caching, token efficiency, model inference routing, fallback handling.
4. **Full-Stack & Systems Engineering**:
   - REST/GraphQL/gRPC APIs, microservices, edge handlers, authentication, rate limiting.
   - Frontend dashboards (React, Astro, Next.js, Tailwind), real-time WebSockets, telemetry.

---

## 2. Extraction & Audit Protocol

1. **Scan the Repository**:
   - Identify backend frameworks, database ORMs, pipeline workers, and frontend structure.
2. **Identify the Core Problem & Bottleneck**:
   - What challenge does this system solve? (e.g. *high-concurrency writes, unindexed slow joins, expensive LLM calls, real-time sync*).
3. **Isolate 3 Technical Highlights**:
   - Concrete implementations (e.g., *"Engineered composite B-tree indexes reducing join times by 80%"*, *"Implemented local-first vector caching with pgvector"*, *"Built streaming WebSocket telemetry with zero DOM reflows"*).
4. **Quantify Metrics**:
   - Extract or formulate real technical metrics (e.g., throughput `10k events/sec`, query latency `< 15ms`, memory footprint `-45%`, test coverage `95%`).

---

## 3. Output Format: The Portfolio Project Capsule

When invoked, generate a markdown artifact or response block matching this exact structure:

```markdown
# Portfolio Capsule: [Project Name]

## Metadata
- **Project Title**: [Clear, Professional Title]
- **Category**: [e.g. Data Pipeline & AI | Distributed Database | Full-Stack Telemetry]
- **Role**: [e.g. Lead Data Architect | Full-Stack & AI Engineer]
- **Timeline**: [e.g. 3 Months | 2025 — 2026]
- **Core Metric / Impact**: [e.g. 10k writes/sec • <20ms p99 query latency]
- **Tech Stack**: [PostgreSQL, pgvector, Python, Astro, Kafka, Redis]
- **Repo / Prototype Link**: [URL or GitHub repo]

## High-Level Summary
[1-2 punchy sentences describing what the system is and its core value proposition]

## The Architecture Challenge & Problem Statement
[2-3 sentences explaining the bottleneck, scale challenge, or business constraint that necessitated this architecture]

## Key Engineering Feats
1. **[Database / Storage Feat]**: [Detailed technical summary of schema, indexing, or storage engine]
2. **[Pipeline / AI Integration Feat]**: [Detailed technical summary of ETL, vector search, or LLM orchestration]
3. **[Full-Stack / Systems Feat]**: [Detailed technical summary of API resilience, UI latency, or data streaming]

## Recommended Visuals & Tactile Tokens
- **Architecture Blueprint Concept**: [Brief description of the component flow or ER diagram]
```

---
