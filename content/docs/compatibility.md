+++
title = "GHC Compatibility"
description = "BHC compatibility with GHC and Haskell standards"
weight = 3
+++

BHC aims for high compatibility with existing Haskell code. This page documents the compatibility status.

## Language Standards

| Standard | Status |
|----------|--------|
| Haskell 2010 | Full support |
| GHC2021 | Partial support |
| GHC2024 | Planned |

## GHC Extensions

BHC supports many common GHC extensions. The following table shows the current status:

### Fully Supported

- `OverloadedStrings`
- `LambdaCase`
- `TypeApplications`
- `ScopedTypeVariables`
- `DeriveFunctor`
- `DeriveGeneric`
- `GeneralizedNewtypeDeriving`
- `FlexibleInstances`
- `FlexibleContexts`
- `MultiParamTypeClasses`
- `GADTs`
- `TypeFamilies`
- `DataKinds`
- `KindSignatures`
- `RankNTypes`
- `ExistentialQuantification`
- `BangPatterns`
- `StrictData`

### Partial Support

- `TemplateHaskell` - Limited macro support
- `QuasiQuotes` - Basic support

### Not Yet Supported

- `UnboxedTuples`
- `UnboxedSums`
- `MagicHash`
- `LinearTypes`

## Base Library

BHC includes its own implementation of `base` that is API-compatible with GHC's base library. Most code using `base` should work without modification.

## Hackage Packages

BHC can use packages from Hackage. Compatibility depends on:

1. Extensions used by the package
2. Dependencies on GHC-specific internals
3. Use of Template Haskell

Many pure Haskell packages work out of the box.

## Reporting Compatibility Issues

If you encounter compatibility issues, please report them on [GitHub](https://github.com/raskell-io/bhc/issues) with:

1. The code that fails to compile
2. The error message from BHC
3. Whether the code compiles with GHC
