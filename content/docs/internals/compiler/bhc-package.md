+++
title = "bhc-package"
description = "Package management"
weight = 63
+++

# bhc-package

Package management for the Basel Haskell Compiler.

## Overview

This crate handles package manifests, dependency resolution, and package building.

## Package Manifest

`bhc.toml`:
```toml
[package]
name = "my-app"
version = "1.0.0"
edition = "H26"

[dependencies]
base = "1.0"
text = "2.0"
containers = "0.7"

[build]
profile = "default"
optimization = 2
```

## Commands

```bash
# Initialize new package
bhc init my-project

# Build package
bhc build

# Run tests
bhc test

# Add dependency
bhc add text
```

## Dependency Resolution

- Semantic versioning
- Version constraints
- Transitive dependencies
- Lock file for reproducibility
