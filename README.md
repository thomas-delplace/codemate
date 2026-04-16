# CodeMate

> Local AI Code Assistant with Persistent Codebase Memory

---

## Overview

CodeMate is a local-first AI assistant designed to help developers interact with codebases through a persistent semantic understanding layer.

Instead of treating code as isolated files, CodeMate builds and maintains a **structured representation of the entire project**, enabling consistent, context-aware assistance across sessions.

The system is designed to behave like a **senior developer who has internalized the repository structure, dependencies, and intent over time**.

---

## Core Idea

Traditional LLM usage:

> Each prompt = fresh context, no memory of the project

CodeMate approach:

> Build a persistent model of the codebase → reuse it across all interactions

This model includes:

* file structure
* symbols (functions, classes, variables)
* dependency relationships
* semantic summaries of code modules

---

## Key Principles

* The model is **not trained on the codebase**
* The repository is transformed into a **queryable memory layer**
* All intelligence comes from **context assembly (RAG-style architecture)**
* The system is deterministic in state management (explicit commands)

---

## Architecture Overview

### 1. Codebase Indexing Layer

Builds a persistent representation of the project:

* file tree
* AST extraction
* symbol index
* dependency graph (light static analysis)
* semantic summaries (LLM-generated)

---

### 2. Context Builder

Selects relevant information from the index:

* repo-level summary
* file-level summaries
* focus scope (`/focus`)
* relevant dependencies

---

### 3. LLM Execution Layer

* sends structured prompt to selected model (Ollama)
* optionally orchestrates multiple models
* returns structured response

---

### 4. Persistence Layer

* SQLite or local JSON cache
* stores:

  * index
  * summaries
  * metadata hashes

---

## Mental Model

CodeMate behaves like:

> a developer who reads the repo once, builds a mental map, and then answers questions using that map instead of rereading everything

---

## Important Constraints

* No model fine-tuning
* No implicit memory
* No hidden state mutation
* All changes are explicit via commands

## Conseils PG

* [Open Viking](https://github.com/volcengine/OpenViking)
* [Duckling](https://github.com/facebook/duckling)
