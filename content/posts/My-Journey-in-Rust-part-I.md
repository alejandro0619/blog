---
title: "My journey in Rust: introduction"
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

## Why is it so popular lately

Rust was the most loved language for the last six years, by the annual [stackoverflow survey](https://insights.stackoverflow.com/survey/2021#most-loved-dreaded-and-wanted-language-love-dread), but why?
I think it'd be easier if I introduce myself, at least a bit.

As said [in my about-page](https://spaghettidev.tech/about). I'm a Javascript/Typescript developer and I've worked in shiping a brand new way to utilize applications right from your terminal. I learned Javascript back in 2020 when I started coding, in fact, it was the first time I was using my old laptop for something that wasn't Youtube or Google.

And I truly think that **Javascript is a great language** but as every interpreted language, when it comes to performance, it isn't the best option out there. Let's dig further into this.

Imagine that you're a startup's developer, your team plans to develop a web API, after knowing your client's requirements you are up to choose your tech stack, and there'll be a thought that will come to your mind.

> What should I choose?

In this case you need to think about what are your team's priorities. If your team need fast development you should go for a interpreted one, otherwise, you should pick up a compiled language (to aim performance).

So now we can divide this in two main sections:

- Rust vs an interpreted language.
- Rust vs a compiled language.

## Rust vs an interpreted language

Don't get me wrong, an interpreted language is a great option, specially if you don't want to spend too much time in the developing stage. You want to release your cool first application without that work that implies coding in a compiled one, such as C, C++, and Rust.

In fact, The only downfall I could point out is that is not too performant when runtime comes, otherwise, it does have other pitfalls such as the lack of type checking while compile time. The implementation of the static type checking help it to cuts open several risks that the developer will be fighting against along the developing if it's otherwise.

When rust gets into the scene, he opens a great section of options to choose from. I mentioned above that Rust highlights when it comes to performance and type checking, this post I won't extend myself too much to talk about performance because of two main reasons: People don't really care about the performance of your application with the exception of the those computer science areas where performance means it all, such as ML and developing apps to embedded devices. And the second reason is that I think you can find a lot of information and comparisions between languages in the web, e.g [this page](https://benchmarksgame-team.pages.debian.net/benchmarksgame/index.html) and if you want to know the comparission between **Rust**, and **C++** [check this out](https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/rust-gpp.html). So I'll focus on the type checking feature that burst Rust (and essentially every static typed language) over an interpreted (specially those that are duck typed) one.

### Examples

For the sake of this post, I will compare Javascript vs Rust, I know there're a bunch of programming languages inside of the **interpreted** group, such as Python, Ruby, PHP and so on. And of course is of my knowledge that you can implement statically typing for both Javascript and Python, but it gets out of this post scope.

Let's do a **simple and cliché add function:**

```javascript
function add(n1, n2){
    return n1 + n2;
}
add(5, 6) // Works, returns: 11.
add(5, '6') // Works, but returns '56'
```

Why is that happening? — you may ask yourself if you are not used to **Javascript's type coercion** let me explain it shortly.

Because of the nature of Javascript — being duck typed — the interpreter instead of showing up an error when you attempt to do some arithmetic operations between a character (or a group of chained characters: strings), it will try to do an implicit convertion (what we call coercion) on one type to able to do the mentioned operation. In the example above, it converts 5 to '5' in order to concat both strings: ``'5' + '6' = '56'`` which is not the operation we really mean, because we wanted to add two parameters, not to concat them.

However, not all the interpreted languages got this flaws, but it's worth to mention that compiled languages prevents you from committing this type of errors that eventually will lead you to encounter bugs that are hard to catch up!

Let's do the same function but in Rust:

```rust
fn add(n1: i32, n2: i32) -> i32{
    n1 + n2
}
add(5, 6); // Works, returns: 11.
add(5, '6'); // Err! can't pass char as a integer.
```

Also, it's worth to mention that code in a Rust brings you not only explicity explained warnings and type checking, but let you code being clearer by following it's conventions.

> The compiler will complain if you don't follow its rules.

### Elaborating further

#### Rust explicity

I know this will almost lies on personal opinions, but IHMO Rust brings you the power of explicity without being extra-verbose because adding features at the cost of complexity is not a great trade-off in long terms of maintainability.

For example, imagine a scenario where you are meant to satinise a string by removing it's whitespaces and adding each word to an array.

Using **Javascript** you could use the ``split`` method (And of course you can use any other own-made method to archieve this)

```javascript
function santiniseStr(str){
    let array = str.split("");
     return array;
}

console.log(sanitiseStr("Hello world!"))
```

Because doing this is a very usual task, the Rust's standard library (std) have one method to archieve this: ``split_whitespaces()``

```rust
fn sanitise_str(str: &str) -> Vec<&str>{
    str
    .split_whitespace()
    .collect::<Vec<&str>>()
}
fn main() {
    println!("{:?}", sanitise_str("Hello world!"));
}
```

And at first glance you will say "wtf is all that code", don't wory, I've said that too. The Javascript code will seem like it's clearer, and in fact, it is clearer in terms of fast-reading, but what if you have a (sadly very usual reality) undocumented codebase, and you want to update your ``satiniseStr`` function, **what does it receive as the ``str`` parameter?**, **what is stored in that ``array`` variable?**, maybe **What is the returned value data type?** All these questions could be solved by taking a look at the Javascript documentation, but we all know that we love that try-and-fail method to learn, so what if we avoid reading the doc for a while and see if Rust can solve this for us.

When looking at the ``sanitise_str`` function's signature we can see two important things: The type of the parameter and the type of the returned value.

If you look further you'll find this snippet:

```rust
    str
    .split_whitespace()
    .collect::<Vec<&str>>()
```

And inmediately you'll notice that the ``split_whitespace`` will split a string by whitespaces and ``collect::<Vec<&str>>()`` can have a very hard to understand looking but in matter it will collect the data returned by the ``split_whitespace``method, inside of a vector of strings (String slices to be specific).

This Rust code is way too self-explain than that Javascript code.

Now that we finish comparing interpreted vs Rust, taking by example Javascript vs Rust, we can proceed to start talking about compiled languages vs Rust.

## Rust vs a compiled language

At this point you may know that Rust, in fact, is considered a compiled language. This section will be a more likely a face to face comparision between languages that plays the same league. Also is a well-known thing that compiled languages are usually statically typed and are way performant than the interpreted ones, because of that you may come to the conclusion that Rust will not offer much more than what the C/C++ languages do offer. But that's a **mistold myth**

The advantage that Rust takes over other compiled languages such as C/C++ is that Rust will bring a closed perfomance but without any potential security breach code, and that's the matter when using another languages, C gives you full control of memory which cool but is also dangerous, because not taking the correct prevention will lead to many bugs and security problems.

When C++ did come into the low-level scenario it brough all the C features and an own set of features, but there´s one I'd like to mention is the gabage collector that free the programmer from managing the memory at hand, such thing help us to avoid memory leaks but at a cost: **performance** 