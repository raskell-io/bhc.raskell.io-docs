+++
title = "bhc-parser"
description = "Parsing for BHC"
weight = 12
+++

# bhc-parser

Parser for the Basel Haskell Compiler.

## Overview

This crate parses Haskell source code into an abstract syntax tree. It implements a recursive descent parser with operator precedence parsing for expressions.

## Key Types

| Type | Description |
|------|-------------|
| `Parser` | The parser state |
| `ParseError` | Parse error with recovery |
| `ParseResult<T>` | Result of parsing |

## Supported Syntax

- Full Haskell 2010 syntax
- GHC2021/GHC2024 extensions
- H26 (Haskell 2026) features

## Usage

```rust
use bhc_parser::{parse_module, parse_expr};

// Parse a module
let module = parse_module(source)?;

// Parse a single expression
let expr = parse_expr(source)?;
```

## Error Recovery

The parser continues after errors to report multiple issues:

```
error: unexpected token
  --> src/Main.hs:5:10
   |
 5 |     let x =
   |           ^ expected expression

error: unexpected token
  --> src/Main.hs:8:3
   |
 8 |     in y +
   |        ^ expected expression
```

## Operator Precedence

Operators are parsed with correct precedence and associativity:

```haskell
-- Parsed correctly
1 + 2 * 3      -- 1 + (2 * 3)
a >>= b >>= c  -- (a >>= b) >>= c
```
