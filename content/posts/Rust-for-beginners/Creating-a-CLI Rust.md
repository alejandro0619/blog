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

```toml
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

The crate [clap](https://github.com/clap-rs/clap) that we just installed and used in the snippet below, helps us not only to parse but to validate the an input given by the user. Let's see how to implement and use it into our application.

First thing is to create a function called ``input`` here we'll handle and parse the arguments provided; Our Cli will request only two arguments to work with: ``quote`` and ``color`` but for ``color`` we need a enum as we'll only allow to use a few types of colors (but a cool ones). Let's stop talking and start coding:

### The function signature

```Rust
fn input() -> (String, Colors)
```

### Parsing the input

```Rust
  #[derive(Parser, Debug)]
  #[clap(author, version, about = "cowsay rusty version")]
    struct Args {
        /// Name of the person to greet
        #[clap(short, long)]
        quote: String,

        /// Number of times to greet
        #[clap(arg_enum)]
        color: Colors,
    }
```

The ``Parser`` trait that our ``struct`` derives, parses all the arguments provided by the user and turns it into that struct fields. As you can see, we only have two fields, so it means, we'll only receive two arguments, as we state before.

Note that ``quote`` is the type of ``String`` and ``color`` is the type of ``Colors``, but it doesn't exist yet, so let's create it.

```Rust
  #[derive(Copy, Clone, PartialEq, Eq, PartialOrd, Ord, ArgEnum, Debug)]
    enum Colors {
        // Not black because it's the our background color
        Red,
        Green,
        Yellow,
        Blue,
        Purple,
        Cyan,
        White,
    }
```

Focus on that ``ArgEnum`` derived trait, that means: "Hey, this enum's variants are the only few valid types for a argument" and clap will ensure that the argument provided fits into it.

Once we have our ``Colors`` enum, let's handle each variant using the classic **match** statement:

### Handling the colors

At this point we need to bring into scope the other crate we installed: ``ansi_term``, let's do so:

```Rust
// Imports
use clap::{ArgEnum, Parser};
use ansi_term::{self, Colour} // -> This one

// fn input(){...} bla bla bla
```

Okay, let's split this down, and see what happens.

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
