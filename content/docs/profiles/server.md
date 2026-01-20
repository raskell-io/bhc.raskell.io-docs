+++
title = "Server Profile"
description = "Structured concurrency and observability for services"
weight = 2
+++

The **server** profile adds structured concurrency primitives, cancellation support, and observability hooks for building production services.

## When to Use

Use the server profile when:

- Building web services or APIs
- You need structured concurrency with cancellation
- Observability (tracing, metrics) is important
- Building long-running services

## Usage

```bash
bhc --profile=server Server.hs -o server
```

## Features

### Structured Concurrency

The server profile provides scoped concurrency primitives:

```haskell
{-# LANGUAGE BHC.StructuredConcurrency #-}
module Server where

import Control.Concurrent.Scoped

handler :: Request -> Scoped Response
handler req = withScope $ do
    -- Tasks are automatically cancelled if scope exits
    userData  <- async $ fetchUser req.userId
    orderData <- async $ fetchOrders req.userId

    user   <- await userData
    orders <- await orderData

    return $ Response user orders
```

### Deadlines and Timeouts

```haskell
import Control.Concurrent.Deadline

handler :: Request -> Scoped Response
handler req = withTimeout 5000 $ do  -- 5 second timeout
    result <- performWork
    return result
```

### Observability Hooks

The server profile automatically instruments your code for:

- Distributed tracing (OpenTelemetry compatible)
- Metrics collection
- Structured logging

## Runtime Characteristics

- **Concurrency**: Structured scopes with automatic cancellation
- **GC**: Optimized for low-latency workloads
- **Scheduling**: Preemptive with deadline awareness
- **Memory**: Higher baseline, optimized for throughput
