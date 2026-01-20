+++
title = "Edge Profile"
description = "Minimal runtime for WASM and embedded targets"
weight = 4
+++

The **edge** profile minimizes runtime footprint for WebAssembly and embedded targets.

## When to Use

Use the edge profile when:

- Targeting WebAssembly (WASI)
- Building serverless functions
- Binary size is critical
- Running in resource-constrained environments

## Usage

```bash
bhc --profile=edge --target=wasm32-wasi Lambda.hs -o lambda.wasm
```

## Features

### Minimal Runtime

The edge profile includes only essential runtime components:

- Reduced GC (optimized for short-lived computations)
- No threading support (single-threaded only)
- Minimal base library

### WASM Export

Export functions for the WASM host to call:

```haskell
module Lambda where

-- Export for WASM host
foreign export ccall handler :: Int -> Int

handler :: Int -> Int
handler x = fibonacci x

fibonacci :: Int -> Int
fibonacci n
    | n <= 1    = n
    | otherwise = fibonacci (n-1) + fibonacci (n-2)
```

### Small Binary Size

The edge profile aggressively eliminates unused code:

```bash
# Typical sizes
bhc --profile=edge example.hs -o example.wasm
# ~50KB for simple functions
```

## Runtime Characteristics

- **Threading**: Single-threaded only
- **GC**: Minimal, optimized for request/response patterns
- **FFI**: WASI interface only
- **Memory**: Minimal heap, no runtime overhead

## Deployment

### AWS Lambda

```bash
# Build WASM binary
bhc --profile=edge --target=wasm32-wasi handler.hs -o handler.wasm

# Deploy with wasmtime runtime
```

### Cloudflare Workers

```bash
# Build for Cloudflare
bhc --profile=edge --target=wasm32-wasi worker.hs -o worker.wasm
```

### Fastly Compute@Edge

```bash
# Build for Fastly
bhc --profile=edge --target=wasm32-wasi compute.hs -o compute.wasm
```
