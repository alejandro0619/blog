---
author:
  name: "Alejandro López"
title: "Creating a CLI with Rust"
date: 2022-03-07T15:35:15-04:00
linktitle: Creating a New Theme
type:
- post
- posts
draft: true
toc: true"
description: "Let's get a bit rusty!"
tags:
  - Rust
  - Introduction
  - CLI
series: 
  - Rust tutorials
---

## Setup
Before getting  into our **hacker** mood,
let's create a cargo project and install the packages we'll need:

```Bash
cargo new ferris-say
```

Now, open your Cargo.toml, and add this below ``[dependencies]``:
```Toml
[dependencies]
ansi_term = "0.12.1"
clap = { version = "3.1.6", features = ["derive"] }
```
Or, if you have [cargo edit](https://github.com/killercup/cargo-edit) (which I prefer using), write right in your terminal:

```Bash
cargo add ansi_term 
cargo add clap --features derive
```
After it's installed, we're ready to go to the next step.

## Getting input from arguments 

```Rust
fn main(){
  #[derive(Parser, Debug)] 
  #[clap(author, version, about = "cowsay rusty version")]
    struct Args {
        /// Quote 
        #[clap(short, long)]
        quote: String,

        /// Ferri's color
        #[clap(short, long, default_value_t = "RED")]
        color: String,
    }
  let args = Args::parse();
  println!("Quote: {} Color: {}", args.quote, args.color);
}
```
Okay, let's split this down, and see what happens.

The ``Parser`` trait that our ``Args`` struct derives, parses the arguments provided by the user and turns it into our ``Args`` fields. So we can access to them through its instance. It also takes care to ensure the arguments provided are valid fields. Let's test 'em out:

```Bash
cargo build
target/debug/ferris-say.exe
```
Will result in:
```bash
error: The following required arguments were not provided:
    --quote <QUOTE>

USAGE:
    ferris_say.exe [OPTIONS] --quote <QUOTE>

For more information try --help
```
So yeah! We need to provide a **quote** argument in order to make it work!

```Bash
cargo build
target/debug/ferris-say.exe -q "Hello world!"
```
Now it works!
```bash
PS C:\Users\Aleja\...> target/debug/ferris_say.exe -q "Hello world!"
Quote: Hello world! Color: RED
```
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

