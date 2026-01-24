+++
title = "bhc-hir-to-core"
description = "HIR to Core lowering"
weight = 41
+++

# bhc-hir-to-core

HIR to Core IR lowering for the Basel Haskell Compiler.

## Overview

This crate transforms typed HIR into Core IR, making type classes and patterns explicit.

## Key Transformations

### Dictionary Passing

```haskell
-- HIR (implicit)
show :: Show a => a -> String

-- Core (explicit dictionary)
show :: forall a. ShowDict a -> a -> String
```

### Instance Resolution

```haskell
-- Source
show 42

-- Core
show @Int showIntDict 42
```

### Pattern Compilation

Complex patterns become efficient decision trees:

```haskell
-- HIR
f (Just (x:xs)) = ...
f (Just [])     = ...
f Nothing       = ...

-- Core (nested case)
f arg = case arg of
  Just tmp -> case tmp of
    (:) x xs -> ...
    []       -> ...
  Nothing -> ...
```

### Newtype Coercions

```haskell
-- Source
newtype Age = Age Int
toAge :: Int -> Age
toAge = Age

-- Core (zero-cost coercion)
toAge = \x -> x |> CoAge
```
