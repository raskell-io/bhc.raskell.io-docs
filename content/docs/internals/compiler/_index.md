+++
title = "Compiler Crates"
description = "BHC compiler implementation crates"
weight = 1
sort_by = "weight"
+++

# Compiler Crates

The BHC compiler is implemented as a collection of Rust crates, each handling a specific stage of compilation.

## Foundation Crates

These crates provide core infrastructure used throughout the compiler:

| Crate | Description |
|-------|-------------|
| [bhc-span](@/docs/internals/compiler/bhc-span.md) | Source location tracking |
| [bhc-arena](@/docs/internals/compiler/bhc-arena.md) | Arena memory allocation |
| [bhc-intern](@/docs/internals/compiler/bhc-intern.md) | String interning |
| [bhc-index](@/docs/internals/compiler/bhc-index.md) | Type-safe indices |
| [bhc-data-structures](@/docs/internals/compiler/bhc-data-structures.md) | Shared data structures |
| [bhc-diagnostics](@/docs/internals/compiler/bhc-diagnostics.md) | Error reporting |

## Frontend Crates

These crates handle parsing and syntax processing:

| Crate | Description |
|-------|-------------|
| [bhc-lexer](@/docs/internals/compiler/bhc-lexer.md) | Tokenization |
| [bhc-ast](@/docs/internals/compiler/bhc-ast.md) | Abstract syntax tree |
| [bhc-parser](@/docs/internals/compiler/bhc-parser.md) | Parsing |

## Type System Crates

These crates implement type checking and inference:

| Crate | Description |
|-------|-------------|
| [bhc-types](@/docs/internals/compiler/bhc-types.md) | Type representation |
| [bhc-typeck](@/docs/internals/compiler/bhc-typeck.md) | Type inference and checking |

## IR Crates

These crates define the intermediate representations:

| Crate | Description |
|-------|-------------|
| [bhc-hir](@/docs/internals/compiler/bhc-hir.md) | High-level IR |
| [bhc-core](@/docs/internals/compiler/bhc-core.md) | Core IR |
| [bhc-tensor-ir](@/docs/internals/compiler/bhc-tensor-ir.md) | Tensor IR (Numeric Profile) |
| [bhc-loop-ir](@/docs/internals/compiler/bhc-loop-ir.md) | Loop IR (vectorization) |

## Lowering Crates

These crates transform between representations:

| Crate | Description |
|-------|-------------|
| [bhc-lower](@/docs/internals/compiler/bhc-lower.md) | AST to HIR lowering |
| [bhc-hir-to-core](@/docs/internals/compiler/bhc-hir-to-core.md) | HIR to Core lowering |

## Backend Crates

These crates handle code generation:

| Crate | Description |
|-------|-------------|
| [bhc-target](@/docs/internals/compiler/bhc-target.md) | Target specifications |
| [bhc-codegen](@/docs/internals/compiler/bhc-codegen.md) | Native code generation (LLVM) |
| [bhc-gpu](@/docs/internals/compiler/bhc-gpu.md) | GPU code generation |
| [bhc-wasm](@/docs/internals/compiler/bhc-wasm.md) | WebAssembly backend |
| [bhc-linker](@/docs/internals/compiler/bhc-linker.md) | Linking |

## Infrastructure Crates

These crates support compilation orchestration:

| Crate | Description |
|-------|-------------|
| [bhc-session](@/docs/internals/compiler/bhc-session.md) | Compilation session |
| [bhc-query](@/docs/internals/compiler/bhc-query.md) | Incremental compilation |
| [bhc-driver](@/docs/internals/compiler/bhc-driver.md) | Compilation orchestration |
| [bhc-package](@/docs/internals/compiler/bhc-package.md) | Package management |
| [bhc-interface](@/docs/internals/compiler/bhc-interface.md) | Module interfaces |
| [bhc-ffi](@/docs/internals/compiler/bhc-ffi.md) | FFI support |
| [bhc-macros](@/docs/internals/compiler/bhc-macros.md) | Procedural macros |
