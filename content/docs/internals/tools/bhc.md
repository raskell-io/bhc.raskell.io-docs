+++
title = "bhc"
description = "Main compiler"
weight = 1
+++

# bhc

The main Basel Haskell Compiler command-line interface.

## Overview

`bhc` is the primary compiler executable that orchestrates all compilation phases from source to executable.

## Basic Usage

```bash
# Compile a single file
bhc Main.hs -o main

# Compile with optimizations
bhc -O2 Main.hs -o main

# Type check only
bhc --check Main.hs

# Generate LLVM IR
bhc --emit-llvm Main.hs
```

## Common Options

| Flag | Description |
|------|-------------|
| `-o FILE` | Output file name |
| `-O0/1/2/3` | Optimization level |
| `--check` | Type check only |
| `-c` | Compile only (no link) |
| `-v` | Verbose output |
| `--help` | Show help |

## Build Modes

```bash
# Debug build
bhc --debug Main.hs -o main

# Release build
bhc --release Main.hs -o main

# Profile build
bhc --profile Main.hs -o main
```

## Target Selection

```bash
# Native (default)
bhc Main.hs -o main

# WebAssembly
bhc --target wasm32 Main.hs -o main.wasm

# Cross-compile
bhc --target x86_64-linux Main.hs -o main
```

## Package Integration

```bash
# Initialize project
bhc init my-project

# Build project
bhc build

# Run tests
bhc test

# Add dependency
bhc add containers
```
