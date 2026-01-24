+++
title = "bhc-index"
description = "Type-safe indices for BHC"
weight = 4
+++

# bhc-index

Type-safe index types for the Basel Haskell Compiler.

## Overview

This crate provides strongly-typed index types that prevent mixing up different kinds of IDs. A `VarId` cannot be accidentally used where a `TypeId` is expected.

## Key Types

| Type | Description |
|------|-------------|
| `Idx<T>` | Generic index type with phantom type |
| `IndexVec<I, T>` | Vector indexed by `Idx<I>` |

## Usage

```rust
use bhc_index::{Idx, IndexVec, define_index};

// Define custom index types
define_index!(VarId);
define_index!(TypeId);

// Create indices
let var: VarId = VarId::new(0);
let ty: TypeId = TypeId::new(0);

// Type-safe - this won't compile:
// let wrong: VarId = ty;

// Indexed vectors
let mut vars: IndexVec<VarId, String> = IndexVec::new();
let id = vars.push("x".to_string());
assert_eq!(vars[id], "x");
```

## Benefits

- Compile-time prevention of ID mixups
- Zero runtime overhead (newtypes)
- Convenient indexed collections
