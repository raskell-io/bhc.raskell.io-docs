+++
title = "bhci"
description = "Interactive REPL"
weight = 2
+++

# bhci

Interactive Read-Eval-Print Loop for the Basel Haskell Compiler.

## Overview

`bhci` provides an interactive environment for exploring Haskell code, testing expressions, and debugging.

## Starting the REPL

```bash
# Start REPL
bhci

# Load a file
bhci Main.hs

# With package
bhci -package containers
```

## REPL Commands

| Command | Description |
|---------|-------------|
| `:load FILE` | Load a module |
| `:reload` | Reload current modules |
| `:type EXPR` | Show type of expression |
| `:info NAME` | Show info about name |
| `:browse MODULE` | List module exports |
| `:quit` | Exit REPL |

## Interactive Session

```
bhci> :load Example.hs
[1 of 1] Compiling Example

bhci> :type map
map :: (a -> b) -> [a] -> [b]

bhci> map (+1) [1,2,3]
[2,3,4]

bhci> :info Functor
class Functor f where
  fmap :: (a -> b) -> f a -> f b
  (<$) :: a -> f b -> f a
  ...
```

## Debugging

```
bhci> :set -fbreak-on-error
bhci> :trace factorial 5
Stopped at factorial.hs:3:5
  3 | factorial n = n * factorial (n - 1)
                    ^^^^^^^^^^^^^^^^^^^^^^^
bhci> :print n
n = 5
bhci> :step
```

## Multi-line Input

```
bhci> :{
bhci| let fibonacci n =
bhci|       case n of
bhci|         0 -> 0
bhci|         1 -> 1
bhci|         _ -> fibonacci (n-1) + fibonacci (n-2)
bhci| :}
bhci> fibonacci 10
55
```
