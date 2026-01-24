+++
title = "bhc-gpu"
description = "GPU code generation"
weight = 52
+++

# bhc-gpu

GPU code generation for the Basel Haskell Compiler.

## Overview

This crate generates GPU kernels from Tensor IR, targeting NVIDIA CUDA and AMD ROCm platforms.

## Supported Backends

| Backend | Target | IR Format |
|---------|--------|-----------|
| CUDA | NVIDIA GPUs | PTX |
| ROCm | AMD GPUs | AMDGCN |

## Pipeline

```
Tensor IR
    │
    ▼
┌────────────┐
│GPU Lowering│  Identify offloadable kernels
└────────────┘
    │
    ├──────────────┐
    ▼              ▼
┌──────┐      ┌───────┐
│ PTX  │      │AMDGCN │
└──────┘      └───────┘
```

## Kernel Offloading

Operations automatically offloaded to GPU:
- Matrix multiplication
- Element-wise operations on large tensors
- Reductions
- Convolutions

## Memory Management

```rust
// Automatic host/device transfer
let gpu_tensor = tensor.to_device()?;
let result = gpu_matmul(gpu_tensor, other)?;
let host_result = result.to_host()?;
```
