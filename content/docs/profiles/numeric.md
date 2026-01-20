+++
title = "Numeric Profile"
description = "Optimized for computational and numeric workloads"
weight = 3
+++

The **numeric** profile optimizes for computational workloads with strict evaluation in hot paths, unboxed numerics, and SIMD support.

## When to Use

Use the numeric profile when:

- Building data processing pipelines
- Working with numerical algorithms
- Performance-critical computations
- Machine learning or scientific computing

## Usage

```bash
bhc --profile=numeric Compute.hs -o compute
```

## Features

### Strict-by-Default Hot Paths

The numeric profile uses strictness analysis to automatically make hot paths strict:

```haskell
{-# LANGUAGE BHC.StrictDefault #-}
module Compute where

-- Hot paths are automatically strict
sumSquares :: [Double] -> Double
sumSquares = foldl' (\acc x -> acc + x * x) 0
```

### Tensor Operations

Native tensor support with automatic fusion:

```haskell
{-# LANGUAGE BHC.TensorIR #-}
module Compute where

import Data.Tensor

-- Matrix multiply: fused and vectorized
matmul :: Tensor Float -> Tensor Float -> Tensor Float
matmul a b = contract a b [1] [0]

-- Guaranteed fusion: no intermediate allocations
normalize :: Tensor Float -> Tensor Float
normalize t = t / sqrt (sum (t * t))
```

### SIMD Lowering

Element-wise operations are automatically lowered to SIMD instructions:

```haskell
-- This gets vectorized automatically
addVectors :: Vector Double -> Vector Double -> Vector Double
addVectors = zipWith (+)
```

## Runtime Characteristics

- **Evaluation**: Strict in hot paths, lazy elsewhere
- **Numerics**: Unboxed by default
- **Memory**: Reduced heap activity in tight loops
- **SIMD**: Automatic vectorization where possible
