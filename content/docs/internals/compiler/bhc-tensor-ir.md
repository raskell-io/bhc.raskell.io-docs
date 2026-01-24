+++
title = "bhc-tensor-ir"
description = "Tensor IR for numeric optimization"
weight = 32
+++

# bhc-tensor-ir

Tensor Intermediate Representation for the Basel Haskell Compiler.

## Overview

Tensor IR is the key to BHC's numeric performance. It captures shape, stride, and layout information needed for fusion and vectorization.

## When Used

Tensor IR is used only in the Numeric Profile, for operations on arrays and tensors.

## Tracked Properties

| Property | Description |
|----------|-------------|
| `dtype` | Element type (Float32, Float64, etc.) |
| `shape` | Dimension sizes |
| `strides` | Byte strides per dimension |
| `layout` | Memory layout |
| `alias` | Aliasing information |

## Operations

```rust
pub enum TensorOp {
    TMap(Fn, TensorRef),           // map f t
    TZipWith(Fn, TensorRef, TensorRef),
    TReduce(ReduceOp, Axis, TensorRef),
    TReshape(Shape, TensorRef),
    TSlice(SliceSpec, TensorRef),
    TMatMul(TensorRef, TensorRef),
    // ... more
}
```

## Guaranteed Fusion

These patterns **must** fuse (per H26-SPEC Section 8):

```haskell
map f (map g xs)           -- Single traversal
zipWith f (map g a) (map h b)
sum (map f xs)
foldl' op z (map f xs)
```

Fusion failure in Numeric Profile is a compiler bug.
