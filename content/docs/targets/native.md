+++
title = "Native Targets"
description = "Compiling to native executables"
weight = 1
+++

BHC can compile Haskell code to native executables for multiple platforms.

## Supported Platforms

| Platform | Architecture | Status |
|----------|--------------|--------|
| Linux | x86_64 | Stable |
| Linux | aarch64 | Stable |
| macOS | x86_64 | Stable |
| macOS | aarch64 (Apple Silicon) | Stable |
| Windows | x86_64 | Beta |

## Usage

By default, BHC compiles for your current platform:

```bash
bhc Main.hs -o main
```

### Cross-Compilation

To cross-compile for a different target:

```bash
# Compile for Linux x86_64
bhc --target=x86_64-linux Main.hs -o main-linux

# Compile for macOS ARM
bhc --target=aarch64-darwin Main.hs -o main-macos-arm
```

## Optimization Levels

```bash
# Debug build (fast compilation, no optimizations)
bhc -O0 Main.hs -o main

# Default (balanced)
bhc -O1 Main.hs -o main

# Optimized (slower compilation, faster runtime)
bhc -O2 Main.hs -o main
```

## Linking

### Static Linking

```bash
bhc --static Main.hs -o main
```

### Dynamic Linking

```bash
bhc --dynamic Main.hs -o main
```

## Platform-Specific Notes

### Linux

BHC uses musl libc for static linking by default on Linux.

### macOS

Universal binaries (x86_64 + aarch64) can be created:

```bash
bhc --target=universal-darwin Main.hs -o main
```

### Windows

Windows builds require the MSVC toolchain to be installed.
