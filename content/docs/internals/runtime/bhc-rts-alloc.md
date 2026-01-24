+++
title = "bhc-rts-alloc"
description = "Memory allocation"
weight = 2
+++

# bhc-rts-alloc

Memory allocation subsystem for the Basel Haskell Compiler runtime.

## Overview

This crate provides the memory allocation layer, managing heap regions and allocation strategies for different object types.

## Memory Regions

| Region | Purpose | Characteristics |
|--------|---------|-----------------|
| Hot Arena | Short-lived allocations | Bump allocation, no GC |
| Pinned Heap | FFI/stable pointers | Manual management |
| General Heap | Standard objects | GC managed |

## Allocation Flow

```
Allocation Request
       │
       ▼
┌──────────────┐
│ Check Arena  │──── Fits? ───► Bump allocate
└──────────────┘                     │
       │ No                          │
       ▼                             │
┌──────────────┐                     │
│ Check TLAB   │──── Fits? ───► Fast path
└──────────────┘                     │
       │ No                          │
       ▼                             │
┌──────────────┐                     │
│ Slow Path    │◄────────────────────┘
│ (may GC)     │
└──────────────┘
```

## Thread-Local Allocation

```rust
// Each capability has a TLAB
struct ThreadLocalAllocBuffer {
    start: *mut u8,
    end: *mut u8,
    cursor: *mut u8,
}

impl ThreadLocalAllocBuffer {
    fn alloc(&mut self, size: usize) -> Option<*mut u8> {
        if self.cursor + size <= self.end {
            let ptr = self.cursor;
            self.cursor += size;
            Some(ptr)
        } else {
            None // Refill needed
        }
    }
}
```

## Large Object Space

Objects larger than a threshold (typically 3KB) go directly to the Large Object Space (LOS), avoiding nursery overhead.
