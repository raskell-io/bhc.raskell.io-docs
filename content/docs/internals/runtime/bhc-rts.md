+++
title = "bhc-rts"
description = "Runtime system core"
weight = 1
+++

# bhc-rts

Core runtime system for the Basel Haskell Compiler.

## Overview

This crate provides the main runtime system that coordinates all RTS components including memory management, scheduling, and I/O.

## Runtime Profiles

| Profile | Use Case | Characteristics |
|---------|----------|-----------------|
| Default | General purpose | Balanced performance |
| Server | Long-running services | Low latency GC |
| Numeric | Scientific computing | Large heap, batch GC |
| Edge | Embedded/WASM | Minimal footprint |

## Architecture

```
┌─────────────────────────────────────┐
│           Application               │
├─────────────────────────────────────┤
│            bhc-rts                  │
├──────────┬──────────┬───────────────┤
│ Scheduler│    GC    │    Alloc      │
│          │          │               │
│  bhc-rts │ bhc-rts  │  bhc-rts      │
│ scheduler│   -gc    │  -alloc       │
├──────────┴──────────┴───────────────┤
│             Arena                   │
│           bhc-rts-arena             │
└─────────────────────────────────────┘
```

## Initialization

```rust
// Runtime startup sequence
fn main() {
    bhc_rts::init(RuntimeConfig::default());
    bhc_rts::run_main(hs_main);
    bhc_rts::shutdown();
}
```

## Configuration

```rust
RuntimeConfig {
    heap_size: 1 << 30,      // 1GB
    nursery_size: 1 << 20,   // 1MB
    num_capabilities: 4,      // Worker threads
    gc_threads: 2,
    profile: Profile::Server,
}
```
