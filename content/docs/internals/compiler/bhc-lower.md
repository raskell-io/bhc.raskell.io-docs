+++
title = "bhc-lower"
description = "AST to HIR lowering"
weight = 40
+++

# bhc-lower

AST to HIR lowering for the Basel Haskell Compiler.

## Overview

This crate transforms parsed AST into High-level IR (HIR), performing desugaring and name resolution.

## Key Transformations

### Do-Notation

```haskell
-- AST
do
  x <- getLine
  putStrLn x

-- HIR
getLine >>= \x -> putStrLn x
```

### List Comprehensions

```haskell
-- AST
[x * 2 | x <- xs, x > 0]

-- HIR
concatMap (\x -> if x > 0 then [x * 2] else []) xs
```

### Guards

```haskell
-- AST
f x | x > 0     = "positive"
    | otherwise = "other"

-- HIR
f x = case () of
  _ | x > 0     -> "positive"
    | otherwise -> "other"
```

## Name Resolution

The lowering pass also resolves names to their definitions:

- Local variables
- Top-level bindings
- Imported names
- Qualified names
