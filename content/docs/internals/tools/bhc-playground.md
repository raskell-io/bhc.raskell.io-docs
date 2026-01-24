+++
title = "bhc-playground"
description = "Web playground"
weight = 4
+++

# bhc-playground

Web-based playground for experimenting with the Basel Haskell Compiler.

## Overview

The playground provides an interactive web environment for writing, compiling, and running Haskell code without local installation.

## Features

| Feature | Description |
|---------|-------------|
| Live compilation | Compile as you type |
| Syntax highlighting | Haskell-aware editor |
| Error diagnostics | Inline error display |
| Sharing | Share code via URL |
| Examples | Pre-built examples |

## Architecture

```
┌─────────────────────────────────────────┐
│            Browser                       │
│  ┌────────────────────────────────────┐ │
│  │   Monaco Editor                    │ │
│  │   ┌──────────────────────────────┐ │ │
│  │   │ Haskell Source               │ │ │
│  │   └──────────────────────────────┘ │ │
│  └────────────────────────────────────┘ │
│             │                            │
│             ▼                            │
│  ┌────────────────────────────────────┐ │
│  │   WASM Compiler                   │ │
│  │   (bhc compiled to WebAssembly)   │ │
│  └────────────────────────────────────┘ │
│             │                            │
│             ▼                            │
│  ┌────────────────────────────────────┐ │
│  │   Output / Execution              │ │
│  └────────────────────────────────────┘ │
└─────────────────────────────────────────┘
```

## Local Development

```bash
# Build playground
cd tools/bhc-playground
npm install
npm run dev

# Build for production
npm run build
```

## URL Sharing

Code can be shared via URL parameters:

```
https://playground.bhc.raskell.io/?code=base64_encoded_code
```

## Embedding

Embed the playground in documentation:

```html
<iframe
  src="https://playground.bhc.raskell.io/embed"
  width="100%"
  height="400">
</iframe>
```
