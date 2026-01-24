+++
title = "bhc-transformers"
description = "Monad transformers"
weight = 6
+++

# bhc-transformers

Monad transformers for the Basel Haskell Compiler.

## Overview

This crate provides monad transformers for composing monadic effects.

## Core Transformers

| Transformer | Base Effect |
|-------------|-------------|
| `StateT s m` | Mutable state |
| `ReaderT r m` | Read-only environment |
| `WriterT w m` | Accumulated output |
| `ExceptT e m` | Error handling |
| `MaybeT m` | Optional failure |
| `ContT r m` | Continuations |

## Usage

```haskell
import Control.Monad.Trans.State
import Control.Monad.Trans.Reader
import Control.Monad.Trans.Class (lift)

-- Compose transformers
type App = StateT Int (ReaderT Config IO)

runApp :: App a -> Config -> Int -> IO (a, Int)
runApp app config state =
    runReaderT (runStateT app state) config

-- Lift through layers
example :: App ()
example = do
    s <- get
    c <- lift ask
    lift $ lift $ putStrLn "IO action"
```

## mtl-style Classes

```haskell
class Monad m => MonadState s m where
    get :: m s
    put :: s -> m ()

class Monad m => MonadReader r m where
    ask :: m r
    local :: (r -> r) -> m a -> m a

class (Monoid w, Monad m) => MonadWriter w m where
    tell :: w -> m ()
    listen :: m a -> m (a, w)

class Monad m => MonadError e m where
    throwError :: e -> m a
    catchError :: m a -> (e -> m a) -> m a
```

## Lifting

```haskell
-- Lift any IO into a transformer stack
liftIO :: MonadIO m => IO a -> m a

-- Generic lift
lift :: (MonadTrans t, Monad m) => m a -> t m a
```
