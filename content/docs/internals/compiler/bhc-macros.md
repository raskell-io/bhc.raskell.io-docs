+++
title = "bhc-macros"
description = "Procedural macros"
weight = 66
+++

# bhc-macros

Procedural macros for the Basel Haskell Compiler.

## Overview

This crate provides derive macros and other procedural macros used internally by the compiler.

## Available Derives

| Derive | Description |
|--------|-------------|
| `Internable` | Enable string interning |
| `AstNode` | AST node with span |
| `IrNode` | IR node boilerplate |
| `Idx` | Index type generation |

## Usage

```rust
use bhc_macros::{AstNode, Internable};

#[derive(AstNode)]
pub struct Expr {
    pub kind: ExprKind,
    pub span: Span,
}

#[derive(Internable)]
pub struct Symbol(u32);
```

## Generated Code

The `AstNode` derive generates:
- Span accessor methods
- Visitor pattern support
- Debug formatting with spans
