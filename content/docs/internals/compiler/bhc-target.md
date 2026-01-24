+++
title = "bhc-target"
description = "Target specifications"
weight = 50
+++

# bhc-target

Target platform specifications for the Basel Haskell Compiler.

## Overview

This crate defines target platforms and their characteristics, enabling cross-compilation and platform-specific code generation.

## Supported Targets

| Target | Triple | Status |
|--------|--------|--------|
| Linux x86_64 | `x86_64-unknown-linux-gnu` | ✅ |
| macOS x86_64 | `x86_64-apple-darwin` | ✅ |
| macOS ARM64 | `aarch64-apple-darwin` | ✅ |
| Windows | `x86_64-pc-windows-msvc` | 🔄 |
| WebAssembly | `wasm32-wasi` | ✅ |
| CUDA | `nvptx64-nvidia-cuda` | 🔄 |

## Target Properties

```rust
pub struct Target {
    pub triple: String,
    pub arch: Architecture,
    pub os: OperatingSystem,
    pub pointer_width: u32,
    pub endian: Endianness,
    pub features: TargetFeatures,
}

pub struct TargetFeatures {
    pub simd: SimdSupport,    // SSE, AVX, NEON
    pub atomics: bool,
    pub threads: bool,
    pub fpu: bool,
}
```

## Usage

```bash
# Native (auto-detected)
bhc Main.hs

# Cross-compile
bhc --target=wasm32-wasi Main.hs
bhc --target=aarch64-apple-darwin Main.hs
```
