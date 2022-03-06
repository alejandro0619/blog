---
title: "My Journey in Rust Part I"
date: 2022-03-05T13:43:30-04:00
draft: false
toc: true
description: "Is Rust really that worth?"
images:
tags:
    - Rust
---
## Introduction
If you have been in a cave for the last year, you might not notice there's a language that's **been rising** and **gathering power**, it's name is **Rust**.
If I had to describe it in one phrase, I'd  totally agree with it's brief but true description shown in  [the official page](https://www.rust-lang.org/):

> A language empowering everyone
to build reliable and efficient software.

## Why is it so popular lately?
Rust was the most loved language for the last six years, by [stackoverflow survey](https://insights.stackoverflow.com/survey/2021#most-loved-dreaded-and-wanted-language-love-dread), but why ?
I think it'd be easier if I introduce myself, at least a bit.

I'm a Javascript developer, I've worked with technologies such as Nodejs and Typescript, creating mostly CLIs utilities trying to prove that Javascript is not stuck to a web browser anymore. 

Coming from a interpreted and duck typed language, I really avoided any low-level approach to problems, why? 
C was, seriously, giving me hard times while I was trying to learn it. Maybe so many new terms, so many things to worry about, a weird syntax even if Javascript is part of the  C-like programming language family.

C++ was kind of the same, a weird compiler's errors, data types I've never seen in my life. In short, it was the hell, IMO. (mad respects those who came from any dinamically-typed language and went to any statically one).

I was the kind of guy that was not interested in a statically-typed language and of course, the low-level was not my field.

But let's be honest, when you are working on a large codebase, eventually that type hints turns out to be a **need** instead of a boost. And if you just said "alejandro just forgot about these useful tools (or languages) such as Typescript that brings you type safety out of the box" I did not forgot about it, but afterall your code will be transpiled to Javascript, and all that help that TS brought to you, it's over. 

Don't get me wrong, I'm not killing Typescript by saying "It's not enough" what I mean is that sometimes you need something that will remain until that binary is shipped or the server is up.

So..The need of a type-safe codebase will push you to choose a statically-language? Yes, eventually it will.

There's too many languages out there that meets this requirements, why to choose Rust? Let's divide this in 2 sections as follow:

1. Rust vs a high-level language.
2. Rust vs a low-level language

## Rust vs a high-level language
What were the super acclaimed benefits Rust brought to made me switch?

### Performance.
On many occasions, you don't worry about your performance, because the computer that runs your application is very likely to run it smoothly, but what to do when you want to squeeze the best from it? You should start using a programming language that is closer to the machine, because it means it will be faster.

Other thing that consumes a lot of resources is the GC (Garbage Collector), in short, is a program that runs when your code runs, and is in charge to check which data is not in use anymore to free its memory space, in order to make it available for other variable to store it's value.

### Type Safety
If you came from Javascript, you are very used to something like this.

Javascript simple code snippet:
```javascript
function add(numerOne, numberTwo){
  return numberOne + numberTwo;
}
// let's add two numbers:
add(4, 6); // Expected output: 10;

// what if the user is a QA in their free time and want to generate undefined behavior in our great app?
add(6, "abc"); // Expected output: Error! you can't do arithmethic operations with non-numerical parameters
// Real ouput: "6abc"
```
Rust simple code snippet:

```rust
fn add(number_one: i32, number_two: i32) {
  number_one + number_two
}

add(4, 6) // Expected output: 10

// Not this time QA tester, we have no type coercion here!
add(6, "abc") // Expected ouput: Error! because you cannot pass a &str as a parameter if that function signature doesn't request it!
```




