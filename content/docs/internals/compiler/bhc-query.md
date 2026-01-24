+++
title = "bhc-query"
description = "Incremental compilation"
weight = 61
+++

# bhc-query

Query-based incremental compilation for the Basel Haskell Compiler.

## Overview

This crate implements a demand-driven, incremental compilation system. Queries are memoized and only recomputed when dependencies change.

## Key Concepts

| Concept | Description |
|---------|-------------|
| Query | A computation with inputs and outputs |
| Memoization | Cache query results |
| Invalidation | Detect stale results |
| Demand-driven | Compute only what's needed |

## Query Examples

```rust
// Parse a file (memoized)
let ast = db.parse(file_id)?;

// Type check a module (depends on parsing)
let typed = db.type_check(module_id)?;

// Only recomputes if source changed
db.set_source(file_id, new_source);
let ast = db.parse(file_id)?;  // Recomputed
```

## Benefits

- Fast incremental rebuilds
- Parallel query execution
- Minimal recomputation
- Reproducible builds
