+++
title = "bhc-linker"
description = "Linking support"
weight = 54
+++

# bhc-linker

Linker support for the Basel Haskell Compiler.

## Overview

This crate handles linking of compiled object files with the RTS and external libraries to produce executables.

## Linking Stages

1. **Object collection**: Gather compiled modules
2. **RTS linking**: Link runtime system
3. **Library linking**: Link external libraries
4. **Symbol resolution**: Resolve all references
5. **Executable generation**: Produce final binary

## Platform Linkers

| Platform | Linker |
|----------|--------|
| Linux | `ld` / `lld` |
| macOS | `ld64` |
| Windows | `link.exe` / `lld-link` |
| WASM | `wasm-ld` |

## RTS Components Linked

- Memory allocator
- Garbage collector
- Scheduler (if concurrent)
- I/O primitives
- FFI support

## External Libraries

```bash
# Link with system libraries
bhc Main.hs -lm -lpthread

# Link with pkg-config
bhc Main.hs $(pkg-config --libs openssl)
```
