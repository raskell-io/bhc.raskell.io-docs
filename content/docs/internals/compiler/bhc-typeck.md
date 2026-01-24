+++
title = "bhc-typeck"
description = "Type checking for BHC"
weight = 21
+++

# bhc-typeck

Type inference and checking for the Basel Haskell Compiler.

## Overview

This crate implements Hindley-Milner type inference with extensions for type classes, GADTs, and other advanced features.

## Key Types

| Type | Description |
|------|-------------|
| `TypeChecker` | The type checking engine |
| `TypeEnv` | Type environment |
| `Substitution` | Type variable substitution |
| `TypeError` | Type error with context |

## Type Inference Algorithm

1. **Constraint Generation**: Walk AST, generate constraints
2. **Unification**: Solve equality constraints
3. **Generalization**: Quantify free variables
4. **Defaulting**: Apply defaulting rules

## Usage

```rust
use bhc_typeck::TypeChecker;

let mut tc = TypeChecker::new();

// Infer type of expression
let ty = tc.infer_expr(&expr)?;

// Check against expected type
tc.check_expr(&expr, expected_ty)?;
```

## Type Class Resolution

```haskell
-- Source
show 42

-- Inferred
show @Int $dShowInt 42
-- where $dShowInt is the Show Int dictionary
```

## Error Messages

```
error[E0308]: type mismatch
  --> src/Main.hs:10:5
   |
10 |     x + "hello"
   |     ^^^^^^^^^^^
   |     expected: Int
   |     found: String
   |
   = note: cannot unify Int with String
```
