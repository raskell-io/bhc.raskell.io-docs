+++
title = "bhc-arena"
description = "Arena memory allocation for BHC"
weight = 2
+++

# bhc-arena

Arena-based memory allocation for the Basel Haskell Compiler.

## Overview

This crate provides arena allocation for AST nodes and other compiler data structures. Arenas enable efficient bulk allocation and deallocation.

## Key Types

| Type | Description |
|------|-------------|
| `Arena<T>` | Typed arena for allocating values |
| `DropArena` | Arena that runs destructors |

## Usage

```rust
use bhc_arena::Arena;

let arena = Arena::new();

// Allocate values
let node1 = arena.alloc(AstNode::new(...));
let node2 = arena.alloc(AstNode::new(...));

// Values live until arena is dropped
// No individual deallocation needed
```

## Benefits

- **Fast allocation**: O(1) bump pointer allocation
- **Cache-friendly**: Sequential memory layout
- **Bulk deallocation**: All memory freed when arena drops
- **No fragmentation**: No holes in allocated memory
