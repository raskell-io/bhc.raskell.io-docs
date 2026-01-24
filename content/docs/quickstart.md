+++
title = "Quick Start"
description = "Get started with BHC in minutes"
weight = 2
+++

This guide will help you compile your first Haskell program with BHC.

## Your First Program

Create a file called `Main.hs`:

```haskell
module Main where

main :: IO ()
main = putStrLn "Hello from BHC!"
```

## Compile and Run

Compile with BHC:

```bash
bhc Main.hs -o hello
```

Run the compiled program:

```bash
./hello
```

You should see:

```
Hello from BHC!
```

## Using Runtime Profiles

BHC supports different runtime profiles optimized for various use cases. To compile with a specific profile:

```bash
# Server profile (structured concurrency, observability)
bhc --profile=server Server.hs -o server

# Numeric profile (optimized for computational workloads)
bhc --profile=numeric Compute.hs -o compute

# Edge profile (minimal runtime for WASM)
bhc --profile=edge --target=wasm32-wasi Lambda.hs -o lambda.wasm
```

## Working with Existing Projects

BHC works with existing `.cabal` files:

```bash
# In a directory with a .cabal file
bhc build
```

## Next Steps

- Learn about [Runtime Profiles](/docs/profiles/) in detail
- Explore [Compilation Targets](/docs/targets/)
- Review [GHC Compatibility](/docs/compatibility/)
- Browse the [API Reference](https://bhc.raskell.io/docs/api/) for function signatures and documentation
