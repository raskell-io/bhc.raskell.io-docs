+++
title = "bhc-concurrent"
description = "Concurrency primitives"
weight = 7
+++

# bhc-concurrent

Concurrency primitives for the Basel Haskell Compiler.

## Overview

This crate provides lightweight threads and synchronization primitives for concurrent programming.

## Lightweight Threads

```haskell
-- Fork a new thread
forkIO :: IO () -> IO ThreadId

-- Wait for thread
killThread :: ThreadId -> IO ()

-- Thread delay
threadDelay :: Int -> IO ()  -- microseconds
```

## MVar (Mutable Variables)

```haskell
-- Create MVar
newEmptyMVar :: IO (MVar a)
newMVar :: a -> IO (MVar a)

-- Operations (blocking)
takeMVar :: MVar a -> IO a
putMVar :: MVar a -> a -> IO ()
readMVar :: MVar a -> IO a

-- Non-blocking
tryTakeMVar :: MVar a -> IO (Maybe a)
tryPutMVar :: MVar a -> a -> IO Bool
```

## STM (Software Transactional Memory)

```haskell
-- Transactional variables
newTVar :: a -> STM (TVar a)
readTVar :: TVar a -> STM a
writeTVar :: TVar a -> a -> STM ()

-- Run transaction
atomically :: STM a -> IO a

-- Retry and choice
retry :: STM a
orElse :: STM a -> STM a -> STM a
```

## Channels

```haskell
-- Unbounded channel
newChan :: IO (Chan a)
writeChan :: Chan a -> a -> IO ()
readChan :: Chan a -> IO a

-- Bounded channel
newTBQueue :: Natural -> STM (TBQueue a)
writeTBQueue :: TBQueue a -> a -> STM ()
readTBQueue :: TBQueue a -> STM a
```

## Async

```haskell
-- Run async
async :: IO a -> IO (Async a)
wait :: Async a -> IO a
cancel :: Async a -> IO ()

-- Concurrent operations
concurrently :: IO a -> IO b -> IO (a, b)
race :: IO a -> IO b -> IO (Either a b)
```
