+++
title = "bhc-hir"
description = "High-level IR for BHC"
weight = 30
+++

# bhc-hir

High-level Intermediate Representation for the Basel Haskell Compiler.

## Overview

HIR is the first IR in the compilation pipeline, produced after desugaring. It removes syntactic sugar while preserving the high-level structure needed for type checking.

## Pipeline Position

```
AST  →  [Lower]  →  HIR  →  [TypeCheck]  →  Typed HIR  →  Core
```

## Key Transformations

| From | To |
|------|-----|
| Do-notation | Bind chains (`>>=`) |
| List comprehensions | `concatMap` |
| Guards | Case expressions |
| Where clauses | Let bindings |
| Operator sections | Lambdas |
| Record syntax | Accessor functions |

## Key Types

```rust
pub enum HirExpr {
    Var(Name),
    Lit(Literal),
    App(Box<HirExpr>, Box<HirExpr>),
    Lam(Vec<HirPat>, Box<HirExpr>),
    Let(Vec<HirBind>, Box<HirExpr>),
    Case(Box<HirExpr>, Vec<HirAlt>),
    // Simplified compared to AST
}
```

## Example

```haskell
-- AST
do
  x <- getLine
  print x

-- HIR
getLine >>= (\x -> print x)
```
