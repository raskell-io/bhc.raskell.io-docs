+++
title = "bhc-span"
description = "Source location tracking for BHC"
weight = 1
+++

# bhc-span

Source location tracking for the Basel Haskell Compiler.

## Overview

This crate provides types for tracking source locations throughout the compilation pipeline. It enables accurate error messages with source context.

## Key Types

| Type | Description |
|------|-------------|
| `Span` | A range in source code (start to end) |
| `Pos` | A single position (line, column, offset) |
| `FileId` | Identifier for a source file |
| `SourceMap` | Maps FileIds to source content |

## Usage

```rust
use bhc_span::{Span, Pos, FileId};

// Create a span
let start = Pos::new(1, 1, 0);
let end = Pos::new(1, 10, 9);
let span = Span::new(file_id, start, end);

// Combine spans
let combined = span1.merge(span2);

// Get source text
let text = source_map.span_to_snippet(span);
```

## Features

- Zero-copy span representation
- Efficient span merging
- Source snippet extraction
- Line/column computation
