+++
title = "bhc-numeric"
description = "Numeric computing"
weight = 4
+++

# bhc-numeric

Numeric computing library for the Basel Haskell Compiler.

## Overview

This crate provides high-performance numeric computing with SIMD acceleration and GPU support.

## Array Types

| Type | Description |
|------|-------------|
| `Array sh a` | N-dimensional dense array |
| `Vector a` | 1D array |
| `Matrix a` | 2D array |
| `Tensor a` | N-dimensional tensor |

## SIMD Acceleration

Operations automatically vectorize:

```haskell
-- Element-wise operations use SIMD
v1 + v2        -- Uses AVX/NEON
v1 * v2        -- Vectorized multiply
map f arr      -- Fused loops
```

## Linear Algebra

```haskell
-- Matrix operations
transpose :: Matrix a -> Matrix a
matmul :: Num a => Matrix a -> Matrix a -> Matrix a
inverse :: Fractional a => Matrix a -> Matrix a

-- Decompositions
lu :: Matrix Double -> (Matrix Double, Matrix Double)
qr :: Matrix Double -> (Matrix Double, Matrix Double)
svd :: Matrix Double -> (Matrix Double, Vector Double, Matrix Double)
eigenvalues :: Matrix Double -> Vector (Complex Double)
```

## GPU Computing

```haskell
-- Transfer to GPU
toGPU :: Array sh a -> IO (GPUArray sh a)

-- GPU operations
gpuMatmul :: GPUArray sh a -> GPUArray sh a -> IO (GPUArray sh a)

-- Transfer back
fromGPU :: GPUArray sh a -> IO (Array sh a)
```

## BLAS Integration

Backed by optimized BLAS libraries:
- OpenBLAS
- Intel MKL
- Apple Accelerate
