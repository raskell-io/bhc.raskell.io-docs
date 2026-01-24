+++
title = "bhc-driver"
description = "Compilation orchestration"
weight = 62
+++

# bhc-driver

Compilation orchestration for the Basel Haskell Compiler.

## Overview

This crate coordinates the compilation pipeline, managing the flow from source files through parsing, type checking, optimization, and code generation.

## Pipeline Stages

```
Source Files
     │
     ▼
┌─────────┐
│  Parse  │
└─────────┘
     │
     ▼
┌─────────┐
│  Lower  │  AST → HIR
└─────────┘
     │
     ▼
┌─────────┐
│TypeCheck│
└─────────┘
     │
     ▼
┌─────────┐
│  Lower  │  HIR → Core
└─────────┘
     │
     ▼
┌─────────┐
│ Codegen │
└─────────┘
     │
     ▼
┌─────────┐
│  Link   │
└─────────┘
     │
     ▼
Executable
```

## Driver API

```rust
let driver = Driver::new(session);

// Full compilation
driver.compile(&files, output)?;

// Type check only
driver.check(&files)?;

// Compile and run
driver.run(&files)?;
```

## Parallel Compilation

Multiple modules compile in parallel when dependencies allow:

```
       ┌─────┐
       │ A.hs│
       └──┬──┘
    ┌─────┴─────┐
    ▼           ▼
┌─────┐     ┌─────┐
│B.hs │     │C.hs │  ← Parallel
└──┬──┘     └──┬──┘
   └─────┬─────┘
         ▼
     ┌─────┐
     │D.hs │
     └─────┘
```
