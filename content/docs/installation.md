+++
title = "Installation"
description = "How to install the Basel Haskell Compiler"
weight = 1
+++

## System Requirements

BHC runs on the following platforms:

- **Linux** (x86_64, aarch64)
- **macOS** (x86_64, Apple Silicon)
- **Windows** (x86_64)

## Install via Script

The recommended way to install BHC is using the install script:

```bash
curl -fsSL https://bhc.raskell.io/install.sh | sh
```

This will download the latest release and add `bhc` to your PATH.

## Install via Cargo

If you have Rust installed, you can install BHC via Cargo:

```bash
cargo install bhc
```

## Verify Installation

After installation, verify that BHC is correctly installed:

```bash
bhc --version
```

You should see output like:

```
bhc 0.1.0 (alpha)
```

## Next Steps

- Read the [Quick Start](/docs/quickstart/) guide to compile your first program
- Learn about [Runtime Profiles](/docs/profiles/) to optimize for your use case
- Explore [Compilation Targets](/docs/targets/) for WASM and native builds
