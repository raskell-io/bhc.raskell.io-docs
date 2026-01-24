+++
title = "bhc-ast"
description = "Abstract syntax tree for BHC"
weight = 11
+++

# bhc-ast

Abstract syntax tree definitions for the Basel Haskell Compiler.

## Overview

This crate defines the abstract syntax tree that represents parsed Haskell source code. It preserves the full syntactic structure for error reporting and source transformations.

## Key Types

| Type | Description |
|------|-------------|
| `Module` | A complete module |
| `Decl` | Top-level declarations |
| `Expr` | Expressions |
| `Pat` | Patterns |
| `Type` | Type syntax |

## Expression Types

```rust
pub enum Expr {
    Lit(Literal),           // 42, "hello"
    Var(Name),              // x, foo
    App(Box<Expr>, Box<Expr>),  // f x
    Lam(Vec<Pat>, Box<Expr>),   // \x -> e
    Let(Vec<Bind>, Box<Expr>),  // let x = e in e'
    Case(Box<Expr>, Vec<Alt>),  // case e of { ... }
    If(Box<Expr>, Box<Expr>, Box<Expr>),
    Do(Vec<Stmt>),          // do { ... }
    List(Vec<Expr>),        // [1, 2, 3]
    Tuple(Vec<Expr>),       // (a, b, c)
    // ... more variants
}
```

## Pattern Types

```rust
pub enum Pat {
    Var(Name),              // x
    Lit(Literal),           // 42
    Con(Name, Vec<Pat>),    // Just x
    Tuple(Vec<Pat>),        // (a, b)
    List(Vec<Pat>),         // [x, y]
    Wild,                   // _
    As(Name, Box<Pat>),     // x@(Just y)
    // ... more variants
}
```

## Span Preservation

Every AST node carries its source span for error reporting:

```rust
pub struct Expr {
    pub kind: ExprKind,
    pub span: Span,
}
```
