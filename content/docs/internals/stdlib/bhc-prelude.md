+++
title = "bhc-prelude"
description = "Standard prelude"
weight = 1
+++

# bhc-prelude

Standard Prelude for the Basel Haskell Compiler.

## Overview

This crate provides the default imports available in every Haskell module, including fundamental types, type classes, and common functions.

## Core Types

| Type | Description |
|------|-------------|
| `Bool` | Boolean values |
| `Char` | Unicode characters |
| `Int` | Fixed-precision integers |
| `Integer` | Arbitrary-precision integers |
| `Float`, `Double` | Floating-point numbers |
| `Maybe a` | Optional values |
| `Either a b` | Sum type for errors |
| `[]` | Lists |
| `()` | Unit type |

## Core Type Classes

```haskell
class Eq a where
    (==), (/=) :: a -> a -> Bool

class Eq a => Ord a where
    compare :: a -> a -> Ordering
    (<), (<=), (>), (>=) :: a -> a -> Bool

class Show a where
    show :: a -> String

class Read a where
    read :: String -> a

class Functor f where
    fmap :: (a -> b) -> f a -> f b

class Functor f => Applicative f where
    pure :: a -> f a
    (<*>) :: f (a -> b) -> f a -> f b

class Applicative m => Monad m where
    (>>=) :: m a -> (a -> m b) -> m b
```

## Common Functions

```haskell
-- List operations
map, filter, foldr, foldl :: ...
head, tail, init, last :: [a] -> ...
(++), concat, reverse :: ...

-- Function composition
(.) :: (b -> c) -> (a -> b) -> a -> c
($) :: (a -> b) -> a -> b
id :: a -> a
const :: a -> b -> a

-- Numeric
(+), (-), (*), (/) :: Num a => ...
```
