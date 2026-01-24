+++
title = "bhc-rts-scheduler"
description = "Thread scheduling"
weight = 5
+++

# bhc-rts-scheduler

Work-stealing scheduler for the Basel Haskell Compiler runtime.

## Overview

This crate implements a work-stealing scheduler for lightweight Haskell threads (sparks) across OS thread capabilities.

## Architecture

```
┌──────────────────────────────────────────┐
│              Scheduler                    │
├──────────┬──────────┬──────────┬─────────┤
│ Cap 0    │ Cap 1    │ Cap 2    │ Cap 3   │
│ ┌──────┐ │ ┌──────┐ │ ┌──────┐ │ ┌─────┐ │
│ │Queue │ │ │Queue │ │ │Queue │ │ │Queue│ │
│ └──────┘ │ └──────┘ │ └──────┘ │ └─────┘ │
│    ↓     │    ↓     │    ↓     │    ↓    │
│ Thread   │ Thread   │ Thread   │ Thread  │
└──────────┴──────────┴──────────┴─────────┘
        ←── Work Stealing ──→
```

## Capabilities

Each capability is an OS thread that can execute Haskell threads:

```rust
struct Capability {
    id: u32,
    run_queue: Deque<Thread>,
    current_thread: Option<Thread>,
    spark_pool: SparkPool,
}
```

## Work Stealing

When a capability's queue is empty, it steals work from others:

```rust
fn schedule(&mut self) -> Option<Thread> {
    // Try local queue first
    self.run_queue.pop()
        // Then try sparks
        .or_else(|| self.spark_pool.pop())
        // Then steal from others
        .or_else(|| self.steal_from_others())
}
```

## Thread States

| State | Description |
|-------|-------------|
| Running | Executing on a capability |
| Runnable | Ready to run |
| Blocked | Waiting on MVar/IO |
| Finished | Completed execution |

## Spark Pools

Sparks are potential parallelism from `par`:

```haskell
-- Creates a spark
x `par` y `pseq` (x + y)
```

Sparks are cheaper than threads and converted to threads when capacity is available.
