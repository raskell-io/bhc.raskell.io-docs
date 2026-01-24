+++
title = "bhc-text"
description = "Text processing"
weight = 5
+++

# bhc-text

Efficient text processing for the Basel Haskell Compiler.

## Overview

This crate provides efficient Unicode text handling with UTF-8 encoding.

## Text Type

```haskell
-- Strict text (UTF-8 encoded)
data Text

-- Lazy text (chunked)
data LazyText
```

## Basic Operations

```haskell
-- Construction
pack :: String -> Text
unpack :: Text -> String
empty :: Text
singleton :: Char -> Text

-- Query
length :: Text -> Int
null :: Text -> Bool

-- Transformation
map :: (Char -> Char) -> Text -> Text
filter :: (Char -> Bool) -> Text -> Text
reverse :: Text -> Text
```

## Slicing and Indexing

```haskell
take :: Int -> Text -> Text
drop :: Int -> Text -> Text
splitAt :: Int -> Text -> (Text, Text)
takeWhile :: (Char -> Bool) -> Text -> Text
```

## Encoding/Decoding

```haskell
-- UTF-8 encoding
encodeUtf8 :: Text -> ByteString
decodeUtf8 :: ByteString -> Text
decodeUtf8' :: ByteString -> Either UnicodeException Text

-- Other encodings
decodeLatin1 :: ByteString -> Text
decodeUtf16LE :: ByteString -> Text
```

## Text Builder

```haskell
-- Efficient construction
import Data.Text.Builder

build :: Builder -> Text
fromText :: Text -> Builder
fromString :: String -> Builder
(<>) :: Builder -> Builder -> Builder
```

## Performance

- O(1) slicing (views into original)
- SIMD-accelerated search
- Cache-efficient UTF-8 iteration
