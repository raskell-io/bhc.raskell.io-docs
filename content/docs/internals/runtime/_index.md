+++
title = "Runtime Crates"
description = "BHC Runtime System crates"
weight = 2
sort_by = "weight"
+++

# Runtime Crates

The BHC Runtime System (RTS) provides the execution environment for compiled Haskell programs. It manages memory, garbage collection, thunk evaluation, and concurrency.

## Architecture

```
┌─────────────────────────────────────────────────┐
│              Compiled BHC Program               │
├─────────────────────────────────────────────────┤
│                    bhc-rts                       │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐           │
│  │ Memory  │ │   GC    │ │Scheduler│           │
│  └─────────┘ └─────────┘ └─────────┘           │
├─────────────────────────────────────────────────┤
│  ┌───────────┐  ┌───────────┐  ┌───────────┐   │
│  │ rts-alloc │  │  rts-gc   │  │rts-scheduler│  │
│  └───────────┘  └───────────┘  └───────────┘   │
│        │              │              │          │
│        └──────────────┴──────────────┘          │
│                       │                          │
│               ┌───────────────┐                  │
│               │   rts-arena   │                  │
│               └───────────────┘                  │
└─────────────────────────────────────────────────┘
```

## Memory Regions

The RTS manages three memory regions:

| Region | Purpose | Allocation | GC |
|--------|---------|------------|-----|
| **Hot Arena** | Kernel temporaries | Bump pointer | None |
| **Pinned Heap** | FFI/device IO | malloc-style | Never moved |
| **General Heap** | Boxed values | GC-managed | May move |

## Crate Reference

| Crate | Description |
|-------|-------------|
| [bhc-rts](@/docs/internals/runtime/bhc-rts.md) | Core runtime system |
| [bhc-rts-alloc](@/docs/internals/runtime/bhc-rts-alloc.md) | Memory allocation primitives |
| [bhc-rts-arena](@/docs/internals/runtime/bhc-rts-arena.md) | Hot arena allocator |
| [bhc-rts-gc](@/docs/internals/runtime/bhc-rts-gc.md) | Garbage collector |
| [bhc-rts-scheduler](@/docs/internals/runtime/bhc-rts-scheduler.md) | Task scheduler |

## Profile-Specific Behavior

| Profile | Evaluation | GC | Arena | Threading |
|---------|------------|-----|-------|-----------|
| Default | Lazy | Standard | Available | Green threads |
| Server | Lazy | Incremental | Available | Work-stealing |
| Numeric | Strict | Minimal | Primary | Parallel loops |
| Edge | Lazy | Minimal | Limited | Single-threaded |
