+++
title = "bhc-containers"
description = "Data structures"
weight = 3
+++

# bhc-containers

Efficient data structures for the Basel Haskell Compiler.

## Overview

This crate provides efficient implementations of common data structures including maps, sets, sequences, and graphs.

## Data Structures

| Type | Description | Complexity |
|------|-------------|------------|
| `Map k v` | Balanced binary tree map | O(log n) |
| `Set a` | Balanced binary tree set | O(log n) |
| `IntMap v` | Int-keyed map | O(min(n, W)) |
| `IntSet` | Int set | O(min(n, W)) |
| `Seq a` | Finger tree sequence | O(log n) ends |
| `Graph` | Adjacency list graph | Varies |

## Map Operations

```haskell
import qualified Data.Map as M

-- Construction
empty :: Map k v
singleton :: k -> v -> Map k v
fromList :: Ord k => [(k, v)] -> Map k v

-- Query
lookup :: Ord k => k -> Map k v -> Maybe v
member :: Ord k => k -> Map k v -> Bool
size :: Map k v -> Int

-- Modification
insert :: Ord k => k -> v -> Map k v -> Map k v
delete :: Ord k => k -> Map k v -> Map k v
adjust :: Ord k => (v -> v) -> k -> Map k v -> Map k v
```

## Sequence Operations

```haskell
import qualified Data.Sequence as Seq

-- O(1) operations on both ends
(<|) :: a -> Seq a -> Seq a    -- cons
(|>) :: Seq a -> a -> Seq a    -- snoc

-- O(log(min(i,n-i))) indexing
index :: Seq a -> Int -> a
update :: Int -> a -> Seq a -> Seq a
```

## Graph Algorithms

```haskell
-- Traversals
dfs :: Graph -> [Vertex] -> [Vertex]
bfs :: Graph -> [Vertex] -> [Vertex]

-- Analysis
topSort :: Graph -> [Vertex]
scc :: Graph -> [[Vertex]]
```
