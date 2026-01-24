+++
title = "bhc-codegen"
description = "Native code generation"
weight = 51
+++

# bhc-codegen

Native code generation for the Basel Haskell Compiler.

## Overview

This crate generates native code via LLVM, transforming Core IR (or Loop IR for numeric code) into efficient machine code.

## Pipeline

```
Core IR / Loop IR
       │
       ▼
   ┌─────────┐
   │  Lower  │  IR to LLVM IR
   └─────────┘
       │
       ▼
   ┌─────────┐
   │  LLVM   │  Optimization & codegen
   └─────────┘
       │
       ▼
   Object File
```

## Key Components

| Component | Description |
|-----------|-------------|
| IR Lowering | Core/Loop IR to LLVM IR |
| Runtime Calls | Links to RTS functions |
| GC Integration | Safe point insertion |
| SIMD Codegen | Vector instruction emission |

## Calling Convention

- Uses C calling convention for RTS interop
- Tail call optimization where possible
- Register allocation via LLVM

## Optimization Levels

| Level | Description |
|-------|-------------|
| `-O0` | No optimization (fast compile) |
| `-O1` | Basic optimizations |
| `-O2` | Standard optimizations |
| `-O3` | Aggressive optimizations |
