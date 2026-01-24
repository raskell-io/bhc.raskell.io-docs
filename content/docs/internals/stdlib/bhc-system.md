+++
title = "bhc-system"
description = "System interfaces"
weight = 8
+++

# bhc-system

System interfaces for the Basel Haskell Compiler.

## Overview

This crate provides interfaces to the operating system including file system, processes, and networking.

## File System

```haskell
-- Path operations
import System.FilePath
(</>) :: FilePath -> FilePath -> FilePath
takeDirectory :: FilePath -> FilePath
takeFileName :: FilePath -> FilePath
takeExtension :: FilePath -> String

-- Directory operations
import System.Directory
createDirectory :: FilePath -> IO ()
removeDirectory :: FilePath -> IO ()
listDirectory :: FilePath -> IO [FilePath]
doesFileExist :: FilePath -> IO Bool
doesDirectoryExist :: FilePath -> IO Bool
```

## Process Management

```haskell
import System.Process

-- Run command
callCommand :: String -> IO ()
callProcess :: FilePath -> [String] -> IO ()

-- With handles
createProcess :: CreateProcess -> IO (...)
readProcess :: FilePath -> [String] -> String -> IO String
readProcessWithExitCode :: ... -> IO (ExitCode, String, String)
```

## Environment

```haskell
import System.Environment

getArgs :: IO [String]
getEnv :: String -> IO String
lookupEnv :: String -> IO (Maybe String)
setEnv :: String -> String -> IO ()
```

## Networking

```haskell
import Network.Socket

-- Create socket
socket :: Family -> SocketType -> Protocol -> IO Socket

-- TCP client
connect :: Socket -> SockAddr -> IO ()
send :: Socket -> ByteString -> IO Int
recv :: Socket -> Int -> IO ByteString

-- TCP server
bind :: Socket -> SockAddr -> IO ()
listen :: Socket -> Int -> IO ()
accept :: Socket -> IO (Socket, SockAddr)
```
