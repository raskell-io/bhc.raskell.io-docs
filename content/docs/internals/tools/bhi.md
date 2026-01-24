+++
title = "bhi"
description = "Bytecode interpreter"
weight = 3
+++

# bhi

Bytecode interpreter for the Basel Haskell Compiler.

## Overview

`bhi` executes compiled bytecode files (`.bhb`) for rapid development and testing without full native compilation.

## Usage

```bash
# Run bytecode file
bhi program.bhb

# With arguments
bhi program.bhb arg1 arg2

# Verbose mode
bhi -v program.bhb
```

## Bytecode Generation

```bash
# Compile to bytecode
bhc --emit-bytecode Main.hs -o program.bhb

# Compile and run
bhc --run Main.hs
```

## Interpreter Features

| Feature | Description |
|---------|-------------|
| Stack-based VM | Efficient execution |
| Lazy evaluation | Standard Haskell semantics |
| GC integration | Proper memory management |
| FFI support | Call C functions |

## Bytecode Format

```
.bhb file structure:
┌─────────────────┐
│ Header          │
│ - Magic: "BHB"  │
│ - Version       │
│ - Entry point   │
├─────────────────┤
│ Constant Pool   │
│ - Strings       │
│ - Numbers       │
│ - Names         │
├─────────────────┤
│ Code Sections   │
│ - Instructions  │
│ - Debug info    │
├─────────────────┤
│ Metadata        │
│ - Types         │
│ - Dependencies  │
└─────────────────┘
```

## Performance

Bytecode is slower than native code but offers:
- Fast compilation
- Portable execution
- Easy debugging
- Smaller file size
