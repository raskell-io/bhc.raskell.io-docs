+++
title = "bhc-loop-ir"
description = "Loop IR for vectorization"
weight = 33
+++

# bhc-loop-ir

Loop Intermediate Representation for the Basel Haskell Compiler.

## Overview

Loop IR makes iteration structure explicit, enabling SIMD vectorization and parallelization. It's the final IR before code generation for numeric workloads.

## Pipeline Position

```
Tensor IR  →  [Lower]  →  Loop IR  →  [Codegen]  →  LLVM IR
```

## Key Types

```rust
pub enum LoopIR {
    Loop {
        var: LoopVar,
        lo: Bound,
        hi: Bound,
        body: Box<LoopIR>,
    },
    Parallel {
        var: LoopVar,
        lo: Bound,
        hi: Bound,
        chunk: ChunkSize,
        body: Box<LoopIR>,
    },
    Vectorized {
        var: LoopVar,
        width: VectorWidth,
        body: Box<LoopIR>,
    },
    // ...
}
```

## Optimizations

| Optimization | Description |
|--------------|-------------|
| Vectorization | Convert scalar to SIMD |
| Parallelization | Multi-thread outer loops |
| Tiling | Cache-friendly blocking |
| Unrolling | Reduce loop overhead |

## Example

```
-- Tensor IR
sum (map (*2) xs)

-- Loop IR
parallel i in 0..n/8:
  vectorized j in 0..8:
    acc[i*8+j] = xs[i*8+j] * 2
reduce acc with (+)
```
