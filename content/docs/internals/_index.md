+++
title = "Internals"
description = "BHC compiler internals and crate documentation"
weight = 10
sort_by = "weight"
+++

# Compiler Internals

This section documents the internal architecture of the Basel Haskell Compiler. BHC is implemented in Rust and organized as a collection of crates, each responsible for a specific part of the compilation pipeline.

## Architecture Overview

```
Source Code
    │
    ▼
┌─────────────┐
│   Parser    │  bhc-lexer, bhc-parser, bhc-ast
└─────────────┘
    │
    ▼
┌─────────────┐
│    HIR      │  bhc-lower, bhc-hir
└─────────────┘
    │
    ▼
┌─────────────┐
│  Type Check │  bhc-types, bhc-typeck
└─────────────┘
    │
    ▼
┌─────────────┐
│   Core IR   │  bhc-hir-to-core, bhc-core
└─────────────┘
    │
    ├─────────────────┐
    │                 │ (Numeric Profile)
    ▼                 ▼
┌─────────────┐  ┌─────────────┐
│  Codegen    │  │  Tensor IR  │  bhc-tensor-ir
└─────────────┘  └─────────────┘
    │                 │
    │                 ▼
    │            ┌─────────────┐
    │            │   Loop IR   │  bhc-loop-ir
    │            └─────────────┘
    │                 │
    └────────┬────────┘
             │
             ▼
      ┌─────────────┐
      │   Backend   │  bhc-codegen, bhc-gpu, bhc-wasm
      └─────────────┘
             │
             ▼
      ┌─────────────┐
      │   Linker    │  bhc-linker
      └─────────────┘
             │
             ▼
        Executable
```

## Crate Categories

### [Compiler Crates](@/docs/internals/compiler/_index.md)

The main compiler implementation, including parsing, type checking, IR transformations, and code generation.

### [Runtime Crates](@/docs/internals/runtime/_index.md)

The BHC Runtime System (RTS), which provides memory management, garbage collection, and concurrency support for compiled programs.

### [Standard Library](@/docs/internals/stdlib/_index.md)

Rust-side support for the BHC standard library, including numeric primitives, text processing, and system interfaces.

### [Tools](@/docs/internals/tools/_index.md)

Command-line tools including the compiler driver, interactive REPL, and IR inspector.

## Key Design Principles

- **Modularity**: Each crate has a focused responsibility with clean interfaces
- **Type Safety**: Extensive use of Rust's type system to prevent bugs
- **Performance**: Zero-cost abstractions and efficient data structures
- **Transparency**: Clear IR representations for debugging and optimization
