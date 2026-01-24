+++
title = "bhc-rts-arena"
description = "Arena allocation"
weight = 3
+++

# bhc-rts-arena

Arena-based memory allocation for the Basel Haskell Compiler runtime.

## Overview

This crate provides arena allocators for efficient bulk allocation and deallocation of short-lived objects.

## Arena Types

| Arena | Use Case | Lifetime |
|-------|----------|----------|
| Hot Arena | Compilation temps | Per-phase |
| Eval Arena | Thunk evaluation | Per-expression |
| FFI Arena | Foreign calls | Per-call |

## API

```rust
// Create and use an arena
let arena = Arena::new(1 << 20); // 1MB

let ptr = arena.alloc::<MyStruct>();
let slice = arena.alloc_slice::<u8>(1024);

// All memory freed at once
drop(arena);
```

## Bump Allocation

```
Arena Layout:
┌────────────────────────────────────┐
│ Allocated ──►   │   Free Space     │
│ Objects         │                  │
└────────────────────────────────────┘
                  ▲
               Cursor
```

## Benefits

- **Fast allocation**: Simple pointer bump
- **No fragmentation**: Contiguous allocation
- **Bulk deallocation**: Single operation frees all
- **Cache friendly**: Sequential memory access

## Nested Arenas

```rust
// Checkpoint for partial rollback
let checkpoint = arena.checkpoint();

// Allocate temporary data
arena.alloc::<TempData>();

// Restore to checkpoint
arena.restore(checkpoint);
```
