+++
title = "bhc-ffi"
description = "FFI support"
weight = 65
+++

# bhc-ffi

Foreign Function Interface support for the Basel Haskell Compiler.

## Overview

This crate implements FFI for calling C functions and exporting Haskell functions to C.

## Foreign Imports

```haskell
-- Import C function
foreign import ccall "sin"
  c_sin :: Double -> Double

-- Safe vs unsafe
foreign import ccall safe "blocking_read"
  safeRead :: CInt -> Ptr CChar -> IO CInt

foreign import ccall unsafe "fast_op"
  fastOp :: CInt -> CInt
```

## Foreign Exports

```haskell
-- Export Haskell function
foreign export ccall "hs_process"
  process :: CInt -> IO CInt

process :: CInt -> IO CInt
process n = pure (n * 2)
```

## Memory Safety

- Pinned memory for FFI buffers
- Stable pointers for callbacks
- Automatic marshalling

## BLAS Integration

```haskell
-- Use optimized BLAS
foreign import ccall "cblas_dgemm"
  c_dgemm :: ... -> IO ()
```
