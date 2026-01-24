+++
title = "bhc-lexer"
description = "Tokenization for BHC"
weight = 10
+++

# bhc-lexer

Lexical analysis for the Basel Haskell Compiler.

## Overview

This crate tokenizes Haskell source code into a stream of tokens, handling layout rules, Unicode identifiers, and all Haskell 2026 lexical features.

## Key Types

| Type | Description |
|------|-------------|
| `Token` | A lexical token |
| `TokenKind` | Token type enumeration |
| `Lexer` | The tokenizer |

## Token Categories

| Category | Examples |
|----------|----------|
| Keywords | `let`, `where`, `case`, `of`, `do` |
| Operators | `+`, `->`, `=>`, `::`, `@` |
| Literals | `42`, `3.14`, `"hello"`, `'c'` |
| Identifiers | `foo`, `Bar`, `_unused` |
| Layout | Implicit braces and semicolons |

## Usage

```rust
use bhc_lexer::Lexer;

let source = "let x = 42 in x + 1";
let mut lexer = Lexer::new(source);

for token in lexer {
    println!("{:?}: {:?}", token.kind, token.span);
}
```

## Layout Handling

The lexer implements Haskell's layout rule, inserting virtual braces and semicolons:

```haskell
-- Source
do
  x <- getLine
  print x

-- Tokens include virtual { ; }
do { x <- getLine ; print x }
```
