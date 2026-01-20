+++
title = "WebAssembly"
description = "Compiling to WebAssembly with WASI"
weight = 2
+++

BHC can compile Haskell to WebAssembly using the WASI interface.

## Target

```bash
bhc --target=wasm32-wasi Main.hs -o main.wasm
```

## Requirements

WASM compilation works best with the [edge profile](/docs/profiles/edge/):

```bash
bhc --profile=edge --target=wasm32-wasi Main.hs -o main.wasm
```

## Running WASM Modules

### With wasmtime

```bash
wasmtime main.wasm
```

### With wasmer

```bash
wasmer run main.wasm
```

### In the Browser

For browser usage, you'll need a JavaScript wrapper:

```javascript
const { WASI } = require('@aspect-build/aspect-wasi');
const fs = require('fs');

const wasi = new WASI({
    args: ['main.wasm'],
    env: process.env,
});

const wasmBuffer = fs.readFileSync('main.wasm');
WebAssembly.instantiate(wasmBuffer, {
    wasi_snapshot_preview1: wasi.wasiImport,
}).then(({ instance }) => {
    wasi.start(instance);
});
```

## Exporting Functions

To export functions for the WASM host:

```haskell
module Handler where

foreign export ccall add :: Int -> Int -> Int
foreign export ccall multiply :: Int -> Int -> Int

add :: Int -> Int -> Int
add x y = x + y

multiply :: Int -> Int -> Int
multiply x y = x * y
```

Compile:

```bash
bhc --profile=edge --target=wasm32-wasi Handler.hs -o handler.wasm
```

## Limitations

WASM builds have some limitations compared to native builds:

- No threading (single-threaded only)
- Limited filesystem access (WASI sandbox)
- No network access in standard WASI
- Smaller maximum memory

## Binary Size

Tips for reducing WASM binary size:

```bash
# Use edge profile
bhc --profile=edge --target=wasm32-wasi Main.hs -o main.wasm

# Strip debug info
wasm-strip main.wasm

# Optimize with wasm-opt
wasm-opt -O3 main.wasm -o main-opt.wasm
```
