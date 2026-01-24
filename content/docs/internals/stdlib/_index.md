+++
title = "Standard Library"
description = "BHC standard library crates"
weight = 3
sort_by = "weight"
+++

# Standard Library Crates

The BHC standard library provides Rust-side support for Haskell's standard library. The high-level APIs are implemented in Haskell, while these Rust crates provide FFI primitives and performance-critical operations.

For function signatures, type documentation, and usage examples, see the [API Reference](https://bhc.raskell.io/docs/api/).

## Architecture

```
┌─────────────────────────────────────────────────┐
│              Haskell Standard Library            │
│  (Prelude, Data.*, Control.*, System.*)         │
├─────────────────────────────────────────────────┤
│                    FFI Boundary                  │
├─────────────────────────────────────────────────┤
│              Rust Support Crates                 │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐        │
│  │ prelude  │ │  base    │ │containers│        │
│  └──────────┘ └──────────┘ └──────────┘        │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐        │
│  │ numeric  │ │  text    │ │transformers│       │
│  └──────────┘ └──────────┘ └──────────┘        │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐        │
│  │concurrent│ │ system   │ │  utils   │        │
│  └──────────┘ └──────────┘ └──────────┘        │
└─────────────────────────────────────────────────┘
```

## Crate Reference

### Core Libraries

| Crate | Description |
|-------|-------------|
| [bhc-prelude](@/docs/internals/stdlib/bhc-prelude.md) | Minimal Prelude support |
| [bhc-base](@/docs/internals/stdlib/bhc-base.md) | Character and base primitives |
| [bhc-containers](@/docs/internals/stdlib/bhc-containers.md) | Container data structures |

### Performance-Critical Libraries

| Crate | Description |
|-------|-------------|
| [bhc-numeric](@/docs/internals/stdlib/bhc-numeric.md) | SIMD, BLAS, tensor primitives |
| [bhc-text](@/docs/internals/stdlib/bhc-text.md) | SIMD-accelerated text processing |

### Abstractions

| Crate | Description |
|-------|-------------|
| [bhc-transformers](@/docs/internals/stdlib/bhc-transformers.md) | Monad transformers |
| [bhc-concurrent](@/docs/internals/stdlib/bhc-concurrent.md) | Concurrency and STM |

### System Libraries

| Crate | Description |
|-------|-------------|
| [bhc-system](@/docs/internals/stdlib/bhc-system.md) | System and IO primitives |
| [bhc-utils](@/docs/internals/stdlib/bhc-utils.md) | Time, random, JSON utilities |

## Design Philosophy

- **Minimal Rust**: Most logic is in Haskell; Rust only for FFI and performance
- **Zero-Copy**: Views and slices preferred over copying
- **Profile-Aware**: Behavior adapts to the active runtime profile
- **Fusion-Friendly**: Operations designed to compose and fuse
