
# CodeMate Command Palette

---

## Command System Overview

CodeMate is controlled through a structured CLI-style command system.

Each command:

* has a single responsibility
* triggers deterministic backend behavior
* may or may not interact with the LLM
* never directly “prompts the model” without preprocessing

---

# /codebase learn

## Purpose

Initialize a persistent representation of a codebase.

---

## Syntax

```bash
/codebase learn <path>
```

---

## Behavior

### Step 1: File system scan

* recursive directory traversal
* file type filtering (configurable)

---

### Step 2: AST parsing

Extract:

* functions
* classes
* variables
* imports/exports

(using Tree-sitter or equivalent)

---

### Step 3: Index building

Create:

* symbol map
* file → symbol mapping
* dependency approximation graph

---

### Step 4: Semantic summarization

LLM generates:

* file purpose
* module responsibility
* high-level architecture description

---

### Step 5: Persistence

Store results in local DB:

* SQLite or `.ask/` structure

---

## Output

* confirmation of indexing
* summary of repo structure
* stats (files, symbols, modules)

---

# /codebase update

## Purpose

Synchronize internal index with current repository state.

---

## Syntax

```bash
/codebase update
```

---

## Behavior

### Step 1: Change detection

* git diff
* git status
* file hash comparison

---

### Step 2: Selective re-indexing

Only affected components are recomputed:

* modified files → full re-parse
* impacted dependencies → partial update

---

### Step 3: Cache update

* update summaries
* update symbol graph

---

## Constraint

Never performs full re-index unless explicitly forced.

---

# /comment

## Purpose

Generate structured documentation for a code file.

---

## Syntax

```bash
/comment <file>
```

---

## Behavior

* reads file + context from codebase index
* generates documentation output

---

## Output modes (future extension)

* inline JSDoc
* diff patch
* full rewritten file

---

## Constraints

* no hallucinated logic
* only describes observable behavior

---

# /readme

## Purpose

Generate documentation for a repository or directory.

---

## Syntax

```bash
/readme [--quick | --full] [path]
```

---

## Modes

### --quick

* high-level architecture
* main modules
* entry points

---

### --full

* per-folder breakdown
* per-file summaries
* deeper architectural explanation

---

## Dependency

Relies on `/codebase learn` index.

---

# /focus

## Purpose

Define a working scope inside the codebase.

---

## Syntax

```bash
/focus <path>
```

---

## Behavior

* increases relevance of selected file/module
* filters context builder prioritization

---

## Reset

```bash
/focus clear
```

---

# /model

## Purpose

Select active LLM.

---

## Syntax

```bash
/model <name>
```

---

## Behavior

* switches backend model (Ollama)
* affects all subsequent queries

---

# /reprompt

## Purpose

Re-run last prompt with another model.

---

## Syntax

```bash
/reprompt <model>
```

---

## Behavior

* same prompt
* same context
* different model only

---

# /debate

## Purpose

Run multiple models in parallel.

---

## Syntax

```bash
/debate models=<list> judge=<model> mode=<strict|merge|vote>
```

---

## Modes

### strict

* independent answers

### merge

* synthesized answer

### vote

* judge selects best output

---

# /conclusion

## Purpose

Synthesize multiple model outputs.

---

## Syntax

```bash
/conclusion mode=<merge|vote>
```

---

# /private

## Purpose

Control persistence.

---

```bash
/private on|off
```

---

## Behavior

* on → no storage
* off → store session

---

# /history

## Purpose

Enable conversational memory injection.

---

```bash
/history on|off
```

---

# Global Rules

* Commands are parsed by backend (Rust), not LLM
* LLM only receives processed context
* No implicit state changes
* All memory is explicit and inspectable
