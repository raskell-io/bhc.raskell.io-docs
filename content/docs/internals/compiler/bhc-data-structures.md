+++
title = "bhc-data-structures"
description = "Shared data structures for BHC"
weight = 5
+++

# bhc-data-structures

Shared data structures for the Basel Haskell Compiler.

## Overview

This crate provides efficient data structures used throughout the compiler, optimized for common compiler workloads.

## Key Types

| Type | Description |
|------|-------------|
| `FxHashMap<K, V>` | Fast hash map (FxHash) |
| `FxHashSet<T>` | Fast hash set |
| `ThinVec<T>` | Memory-efficient vector |
| `SmallVec<[T; N]>` | Stack-allocated small vector |
| `Graph<N, E>` | Directed graph |
| `WorkQueue<T>` | Work-list for fixed-point iteration |

## Usage

```rust
use bhc_data_structures::{FxHashMap, SmallVec, Graph};

// Fast hash map
let mut map: FxHashMap<Symbol, Type> = FxHashMap::default();
map.insert(sym, ty);

// Small vec (avoids heap for small sizes)
let mut args: SmallVec<[Expr; 4]> = SmallVec::new();
args.push(expr);

// Graph operations
let mut graph = Graph::new();
let a = graph.add_node("a");
let b = graph.add_node("b");
graph.add_edge(a, b, ());
```

## Performance

- FxHash is faster than SipHash for small keys
- SmallVec avoids allocation for common cases
- ThinVec uses less memory for empty/single-element cases
