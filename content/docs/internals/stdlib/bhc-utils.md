+++
title = "bhc-utils"
description = "Utility functions"
weight = 9
+++

# bhc-utils

Utility functions and common patterns for the Basel Haskell Compiler.

## Overview

This crate provides miscellaneous utility functions, debugging tools, and common patterns.

## Debugging

```haskell
import Debug.Trace

-- Print and return
trace :: String -> a -> a
traceShow :: Show a => a -> b -> b
traceShowId :: Show a => a -> a

-- Monadic tracing
traceM :: Applicative f => String -> f ()
traceShowM :: (Show a, Applicative f) => a -> f ()
```

## Unsafe Operations

```haskell
import System.IO.Unsafe

-- Escape hatch (use with caution)
unsafePerformIO :: IO a -> a
unsafeInterleaveIO :: IO a -> IO a
unsafeDupablePerformIO :: IO a -> a
```

## Data.Function

```haskell
-- Function utilities
(&) :: a -> (a -> b) -> b      -- flip ($)
on :: (b -> b -> c) -> (a -> b) -> a -> a -> c
fix :: (a -> a) -> a           -- fixed point
```

## Data.Bifunctor

```haskell
class Bifunctor p where
    bimap :: (a -> b) -> (c -> d) -> p a c -> p b d
    first :: (a -> b) -> p a c -> p b c
    second :: (b -> c) -> p a b -> p a c

-- Works with (,) and Either
bimap (+1) (*2) (1, 2)    -- (2, 4)
first show (Left 42)       -- Left "42"
```

## Data.Coerce

```haskell
-- Safe coercion between newtypes
coerce :: Coercible a b => a -> b

-- Example
newtype Age = Age Int
coerce (42 :: Int) :: Age    -- Age 42
```

## GHC.Generics

```haskell
-- Generic programming support
class Generic a where
    type Rep a :: Type -> Type
    from :: a -> Rep a x
    to :: Rep a x -> a
```
