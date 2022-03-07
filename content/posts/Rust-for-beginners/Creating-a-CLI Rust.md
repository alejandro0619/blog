---
title: "Creating a CLI with Rust"
date: 2022-03-07T15:35:15-04:00
draft: true
toc: true
images:
description: "Let's get a bit rusty!"
tags:
  - Rust
  - Introduction
  - CLI
---

## Dependency tree
Before getting right into our **hacker** mood,
let's install the packages we'll need:

So, open your Cargo.toml, and add this below ``[dependencies]``:
```Toml
[dependencies]
ansi_term = "0.12.1"
clap = { version = "3.1.6", features = ["derive"] }
    
```
Or, if you have [cargo edit](https://github.com/killercup/cargo-edit) (personally, I prefer using this), write rigth in your terminal:

```Bash
cargo add ansi_term 
cargo add clap --features derive
```
After it's installed, 
## Final code
We'll split it into parts to understand how it works.

```Rust
use ansi_term::{self, Colour::Red}; // 0.12.1

fn main() {
  const FERRIS: &'static str = r"
    .
     .
      .
       █ █           █ █
        ▀█  ▄█████▄  █▀
         ▀▄███▀█▀███▄▀ 
         ▄▀███▀▀▀███▀▄ 
         █ ▄▀▀▀▀▀▀▀▄ █
    ";
  println!("{}", format!("\"{}\"{}", "Hello world!", Red.paint(FERRIS)));
}
```

