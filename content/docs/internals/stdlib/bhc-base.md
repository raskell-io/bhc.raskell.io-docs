+++
title = "bhc-base"
description = "Base library"
weight = 2
+++

# bhc-base

Base library for the Basel Haskell Compiler.

## Overview

This crate provides the foundational library modules including I/O, exceptions, and system interfaces.

## Modules

| Module | Description |
|--------|-------------|
| `Data.List` | List operations |
| `Data.Maybe` | Optional values |
| `Data.Either` | Error handling |
| `Data.Tuple` | Tuple operations |
| `Control.Monad` | Monadic utilities |
| `System.IO` | Input/Output |
| `System.Environment` | Environment variables |

## I/O Operations

```haskell
-- File I/O
readFile :: FilePath -> IO String
writeFile :: FilePath -> String -> IO ()
appendFile :: FilePath -> String -> IO ()

-- Handle-based I/O
hGetContents :: Handle -> IO String
hPutStrLn :: Handle -> String -> IO ()
hClose :: Handle -> IO ()

-- Standard handles
stdin, stdout, stderr :: Handle
```

## Exception Handling

```haskell
-- Throwing exceptions
throw :: Exception e => e -> a
throwIO :: Exception e => e -> IO a

-- Catching exceptions
catch :: Exception e => IO a -> (e -> IO a) -> IO a
try :: Exception e => IO a -> IO (Either e a)
bracket :: IO a -> (a -> IO b) -> (a -> IO c) -> IO c
```

## Control.Monad

```haskell
when :: Applicative f => Bool -> f () -> f ()
unless :: Applicative f => Bool -> f () -> f ()
forM :: (Traversable t, Monad m) => t a -> (a -> m b) -> m (t b)
sequence :: (Traversable t, Monad m) => t (m a) -> m (t a)
```
