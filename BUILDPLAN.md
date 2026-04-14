# CodeMate

> Build plan for a local AI code assistant with persistent repository memory

---

# Objective

Deliver CodeMate as a usable developer tool in 3 phases:

* **MVP (0 → 6 months)** → usable CLI tool
* **V1 (6 → 12 months)** → desktop dev companion
* **V2 (12 → 18 months)** → advanced AI code intelligence platform

The core principle across all phases:

> The system builds and maintains a persistent semantic representation of a codebase and uses it to enhance LLM reasoning.

---

# GLOBAL STRATEGY

## 1. Build memory first (not UI)

The hardest part is not the interface, but:

* code indexing
* incremental updates
* context building

---

## 2. LLM is a consumer, not the core

LLM is used for:

* summarization
* explanation
* reasoning

But never for:

* state management
* memory persistence

---

## 3. Everything is explicit

No hidden magic:

* `/codebase learn`
* `/codebase update`
* `/focus`
* `/comment`

---

# MVP (0 → 6 months)

## Goal

A CLI tool that can:

* ingest a repo
* understand its structure
* explain files with context awareness

---

## Scope

### Core features

* `/codebase learn`
* `/codebase update`
* `/comment`
* `/readme --quick`
* `/focus`
* Ollama integration (single model)

---

## Technical milestones

### Phase 1 — CLI foundation (Month 1–2)

#### Deliverables

* Rust CLI app
* Command parser
* File system traversal
* Basic logging system

#### Exit criteria

* Can run:

```bash
/codebase learn ./repo
```

---

### Phase 2 — Code indexing (Month 2–3)

#### Deliverables

* Tree-sitter integration
* AST extraction:

  * functions
  * classes
  * imports
* file → symbol mapping

#### Exit criteria

* Index stored locally
* queryable structure exists

---

### Phase 3 — Persistence layer (Month 3–4)

#### Deliverables

* SQLite or JSON cache system
* file hash tracking
* incremental update foundation

#### Exit criteria

* `/codebase update` works incrementally

---

### Phase 4 — LLM integration (Month 4–5)

#### Deliverables

* Ollama integration
* prompt templates:

  * comment
  * readme
* semantic summaries per file

#### Exit criteria

* `/comment file.ts` produces structured output

---

### Phase 5 — Context builder (Month 5–6)

#### Deliverables

* prompt assembly system
* focus filtering
* repo-level context injection

#### Exit criteria

* answers depend on repo context (not raw file only)

---

## MVP success definition

A developer can:

> load a repo once and get consistent explanations of any file without re-explaining context every time

---

# V1 (6 → 12 months)

## Goal

Turn CLI tool into a **real development companion app**

---

## Scope

* Tauri desktop UI
* file explorer
* chat interface
* `/focus` UI integration
* `/reprompt`, `/debate`
* improved context ranking system

---

## Technical milestones

### Phase 1 — UI shell (Month 6–7)

* Tauri app
* split view:

  * chat
  * file tree
* CLI bridge integration

---

### Phase 2 — smarter context engine (Month 7–9)

* improved relevance scoring
* better file selection heuristics
* dependency graph refinement

---

### Phase 3 — multi-model system (Month 9–10)

* `/debate`
* `/reprompt`
* model switching layer

---

### Phase 4 — memory persistence upgrade (Month 10–12)

* structured `.ask` DB evolution
* better summarization caching
* faster update system

---

## V1 success definition

The app behaves like:

> a persistent senior developer sitting next to your editor

---

# V2 (12 → 18 months)

## Goal

Make CodeMate a **code intelligence platform**

---

## Scope

* vector database integration
* semantic search across codebase
* multi-repo support
* advanced reasoning orchestration
* background precompute system

---

## Technical milestones

### Phase 1 — semantic layer (Month 12–14)

* embeddings for code + summaries
* vector DB (Qdrant or similar)
* `/search` capability (semantic)

---

### Phase 2 — background intelligence (Month 14–16)

* `/codebase precompute`
* background indexing daemon
* live file watching

---

### Phase 3 — advanced reasoning (Month 16–18)

* multi-step reasoning pipelines
* advanced `/debate` modes
* architecture inference layer

---

## V2 success definition

CodeMate can:

> understand multiple repos, reason across them, and assist like a real engineering team member

---

# ⚙️ CORE TECH DECISIONS

## Backend

* Rust (mandatory for performance + control)

---

## LLM runtime

* Ollama (local-first)
* optional cloud fallback later

---

## Indexing

* Tree-sitter AST parsing
* Git-based diff detection
* incremental cache invalidation

---

## Storage

* MVP: JSON or SQLite
* V1+: structured SQLite schema
* V2: hybrid + vector DB

---

# RISK ANALYSIS

## 1. Context explosion

Too much repo data → degraded LLM performance

### mitigation:

* smart filtering
* focus system
* summaries instead of raw code

---

## 2. Overengineering CLI DSL

Risk of building a “language instead of a product”

### mitigation:

* commands must stay minimal and deterministic

---

## 3. LLM hallucination

Even with good context

### mitigation:

* explicit source tagging
* separation “observed vs inferred”

---

# FINAL PRODUCT PRINCIPLE

CodeMate must always follow:

> Memory is external. Intelligence is contextual. Behavior is deterministic.

---

# ONE-LINE SUMMARY

CodeMate is:

> a persistent, incremental, structured memory system for codebases that feeds optimized context to LLMs to simulate senior-level understanding
