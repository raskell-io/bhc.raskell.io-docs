+++
title = "bhc-types"
description = "Type representation for BHC"
weight = 20
+++

# bhc-types

Type representation for the Basel Haskell Compiler.

## Overview

This crate defines the internal representation of types used throughout the compiler, from type checking through code generation.

## Key Types

| Type | Description |
|------|-------------|
| `Ty` | A monomorphic type |
| `TyScheme` | A polymorphic type (with foralls) |
| `TyVar` | A type variable |
| `TyCon` | A type constructor |
| `Constraint` | A type class constraint |

## Type Representation

```rust
pub enum Ty {
    Var(TyVar),                    // a
    Con(TyCon),                    // Int, Bool
    App(Box<Ty>, Box<Ty>),         // Maybe Int
    Fun(Box<Ty>, Box<Ty>),         // a -> b
    Tuple(Vec<Ty>),                // (a, b, c)
    Forall(TyVar, Box<Ty>),        // forall a. a -> a
}

pub struct TyScheme {
    pub vars: Vec<TyVar>,
    pub constraints: Vec<Constraint>,
    pub ty: Ty,
}
```

## Built-in Types

```rust
// Primitive types
Ty::INT    // Int
Ty::FLOAT  // Float
Ty::CHAR   // Char
Ty::BOOL   // Bool

// Type constructors
TyCon::LIST   // []
TyCon::MAYBE  // Maybe
TyCon::IO     // IO
```

## Kind System

Types are kinded to ensure well-formedness:

```rust
pub enum Kind {
    Star,                      // *
    Arrow(Box<Kind>, Box<Kind>), // * -> *
}
```
