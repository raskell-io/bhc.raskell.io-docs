+++
title = "bhc-intern"
description = "String interning for BHC"
weight = 3
+++

# bhc-intern

String interning for the Basel Haskell Compiler.

## Overview

This crate provides string interning, which stores each unique string only once. Interned strings can be compared by pointer equality, making comparisons O(1).

## Key Types

| Type | Description |
|------|-------------|
| `Symbol` | An interned string |
| `Interner` | The interning table |
| `kw` | Pre-interned keywords |

## Usage

```rust
use bhc_intern::{Symbol, Interner};

let mut interner = Interner::new();

// Intern strings
let sym1 = interner.intern("hello");
let sym2 = interner.intern("hello");

// Same symbol (pointer equality)
assert!(sym1 == sym2);

// Get string back
let s: &str = interner.resolve(sym1);
```

## Pre-interned Keywords

```rust
use bhc_intern::kw;

// Common keywords are pre-interned
let if_kw = kw::IF;
let let_kw = kw::LET;
let where_kw = kw::WHERE;
```

## Benefits

- O(1) string comparison
- Reduced memory usage
- Cache-friendly for repeated lookups
