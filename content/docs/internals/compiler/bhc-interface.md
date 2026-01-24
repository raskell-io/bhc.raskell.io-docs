+++
title = "bhc-interface"
description = "Module interfaces"
weight = 64
+++

# bhc-interface

Module interface files for the Basel Haskell Compiler.

## Overview

This crate handles `.bhi` interface files, which store compiled module information for separate compilation.

## Interface Contents

| Section | Description |
|---------|-------------|
| Exports | Public declarations |
| Types | Type signatures |
| Instances | Type class instances |
| Inlinings | Unfoldings for inlining |
| Dependencies | Required modules |

## File Format

```
-- Module.bhi (binary format)
magic: "BHI\0"
version: 1
module_name: "Data.List"
exports: [map, filter, fold, ...]
types: [
  map :: (a -> b) -> [a] -> [b]
  ...
]
instances: [
  instance Functor []
  ...
]
```

## Benefits

- Fast compilation (no re-parsing dependencies)
- Separate compilation
- Cross-module inlining
- Parallel builds
