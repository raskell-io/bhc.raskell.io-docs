+++
title = "bhc-rts-gc"
description = "Garbage collection"
weight = 4
+++

# bhc-rts-gc

Garbage collector for the Basel Haskell Compiler runtime.

## Overview

This crate implements a generational garbage collector optimized for functional programming workloads.

## Generational Design

```
┌─────────────────────────────────────────┐
│  Generation 0 (Nursery)                 │
│  - New allocations                      │
│  - Frequent collection                  │
│  - Copying collector                    │
├─────────────────────────────────────────┤
│  Generation 1 (Survivor)                │
│  - Survived Gen0                        │
│  - Less frequent collection             │
│  - Mark-compact                         │
├─────────────────────────────────────────┤
│  Generation 2 (Old)                     │
│  - Long-lived objects                   │
│  - Rare collection                      │
│  - Concurrent mark-sweep                │
└─────────────────────────────────────────┘
```

## Collection Algorithms

| Generation | Algorithm | Pause Type |
|------------|-----------|------------|
| Gen 0 | Copying | Stop-the-world |
| Gen 1 | Mark-compact | Stop-the-world |
| Gen 2 | Concurrent mark-sweep | Mostly concurrent |

## Write Barrier

```rust
// Remembered set for inter-generational pointers
fn write_barrier(old_obj: *mut Object, new_ref: *mut Object) {
    if generation(old_obj) > generation(new_ref) {
        remembered_set.insert(old_obj);
    }
}
```

## GC Roots

- Thread stacks
- Global variables
- Stable pointers
- Foreign references

## Tuning Parameters

```rust
GcConfig {
    nursery_size: 1 << 20,    // 1MB nursery
    gen1_threshold: 2,         // Promote after 2 survivals
    concurrent_threshold: 0.7, // Start concurrent GC at 70% full
}
```
