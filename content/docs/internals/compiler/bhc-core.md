+++
title = "bhc-core"
description = "Core IR for BHC"
weight = 31
+++

# bhc-core

Core Intermediate Representation for the Basel Haskell Compiler.

## Overview

Core IR is the typed, explicit, optimizable heart of BHC. It makes all implicit operations explicit and serves as the foundation for optimization passes.

## Characteristics

- **Typed**: Every expression carries its type
- **Explicit**: Type applications, coercions visible
- **A-Normal Form**: Complex expressions are let-bound
- **Optimizable**: Designed for transformation

## Key Types

```rust
pub enum Expr {
    Var(Var),
    Lit(Literal, Ty),
    App(Box<Expr>, Box<Expr>),
    TyApp(Box<Expr>, Ty),        // f @Int
    Lam(Var, Box<Expr>),
    TyLam(TyVar, Box<Expr>),     // /\a -> e
    Let(Bind, Box<Expr>),
    Case(Box<Expr>, Vec<Alt>, Ty),
    Cast(Box<Expr>, Coercion),
}
```

## Example

```haskell
-- Source
id True

-- Core (explicit type application)
id @Bool True
```

## Evaluator

The crate includes a Core IR interpreter for the REPL and playground:

```rust
use bhc_core::eval::{Evaluator, Value};

let mut eval = Evaluator::new();
let result: Value = eval.eval(&core_expr)?;
```
