+++
title = "Tools"
description = "BHC command-line tools"
weight = 4
sort_by = "weight"
+++

# Tools

BHC provides several command-line tools for compilation, interactive development, and debugging.

## Tool Reference

| Tool | Description |
|------|-------------|
| [bhc](@/docs/internals/tools/bhc.md) | Main compiler driver |
| [bhci](@/docs/internals/tools/bhci.md) | Interactive REPL |
| [bhi](@/docs/internals/tools/bhi.md) | IR and kernel inspector |
| [bhc-playground](@/docs/internals/tools/bhc-playground.md) | Browser-based interpreter |

## Quick Reference

### bhc - Compiler

```bash
# Compile to executable
bhc Main.hs -o main

# Type check only
bhc check Main.hs

# Compile with profile
bhc --profile=numeric Main.hs

# Target WebAssembly
bhc --target=wasi Main.hs
```

### bhci - REPL

```bash
# Start REPL
bhci

# With profile
bhci --profile=numeric
```

```
bhci:001> let double x = x * 2
bhci:002> double 21
42
bhci:003> :type double
double :: Num a => a -> a
```

### bhi - Inspector

```bash
# Inspect IR
bhi ir program.core

# View kernel report
bhi kernel report.json --failures-only

# Analyze memory
bhi memory alloc.log
```
