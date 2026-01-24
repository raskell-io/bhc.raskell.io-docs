+++
title = "bhc-wasm"
description = "WebAssembly backend"
weight = 53
+++

# bhc-wasm

WebAssembly backend for the Basel Haskell Compiler.

## Overview

This crate generates WebAssembly binaries, enabling Haskell programs to run in browsers and WASI environments.

## Targets

| Target | Description |
|--------|-------------|
| `wasm32-wasi` | WASI for server-side/CLI |
| `wasm32-unknown-unknown` | Pure WASM for browsers |

## Usage

```bash
# Compile to WASM
bhc --target=wasi Main.hs -o app.wasm

# Run with wasmtime
wasmtime app.wasm
```

## Features

| Feature | Status |
|---------|--------|
| Basic I/O | ✅ |
| File system (WASI) | ✅ |
| Threads | 🔄 |
| SIMD128 | ✅ |
| GC (proposal) | 🔄 |

## Runtime

The WASM runtime is minimal (Edge Profile):
- Reduced GC
- Limited concurrency
- Smaller memory footprint

## Browser Usage

```javascript
import init, { run_main } from './app.js';

await init();
run_main();
```
