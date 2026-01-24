+++
title = "bhc-diagnostics"
description = "Error reporting for BHC"
weight = 6
+++

# bhc-diagnostics

Error and warning reporting for the Basel Haskell Compiler.

## Overview

This crate provides structured diagnostics with source context, suggestions, and multiple severity levels.

## Key Types

| Type | Description |
|------|-------------|
| `Diagnostic` | A compiler message |
| `Severity` | Error, Warning, Note, Help |
| `DiagnosticEmitter` | Outputs diagnostics |
| `Suggestion` | A fix suggestion |

## Usage

```rust
use bhc_diagnostics::{Diagnostic, Severity};

let diag = Diagnostic::new(Severity::Error, "type mismatch")
    .with_span(span)
    .with_label(span, "expected `Int`, found `String`")
    .with_note("cannot unify Int with String")
    .with_suggestion("use `show` to convert", fix_span, "show x");

emitter.emit(diag);
```

## Output Format

```
error[E0308]: type mismatch
  --> src/Main.hs:10:5
   |
10 |     x + "hello"
   |     ^^^^^^^^^^^ expected `Int`, found `String`
   |
   = note: cannot unify Int with String
   = help: use `show` to convert: show x
```

## Features

- Rich source context with underlines
- Multiple labels per diagnostic
- Actionable suggestions with code fixes
- Colored terminal output
