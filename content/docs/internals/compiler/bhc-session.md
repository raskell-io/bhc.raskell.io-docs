+++
title = "bhc-session"
description = "Compilation session"
weight = 60
+++

# bhc-session

Compilation session management for the Basel Haskell Compiler.

## Overview

This crate manages the global state of a compilation session, including configuration, diagnostics, and resource management.

## Key Types

| Type | Description |
|------|-------------|
| `Session` | Global compilation state |
| `SessionConfig` | Configuration options |
| `Profile` | Runtime profile |
| `Edition` | Haskell edition |

## Session Configuration

```rust
let session = Session::new(SessionConfig {
    profile: Profile::Numeric,
    edition: Edition::H26,
    opt_level: 2,
    target: Target::native(),
    ..Default::default()
})?;
```

## Profiles

| Profile | Description |
|---------|-------------|
| Default | Standard lazy Haskell |
| Server | Bounded latency, incremental GC |
| Numeric | Strict, SIMD, fusion guaranteed |
| Edge | Minimal footprint |

## Editions

| Edition | Description |
|---------|-------------|
| Haskell2010 | Haskell 2010 standard |
| GHC2021 | GHC2021 extensions |
| GHC2024 | GHC2024 extensions |
| H26 | Haskell 2026 (default) |
