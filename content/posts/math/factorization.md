---
author:
name: "Alejandro López"
title: "Factorization made easy"
date: 2022-04-24T13:10:24-04:00
linktitle: factorization
type:
- post
- posts
draft: false
toc: true
description: "Simplify is the solution to a lot of problems"
katex: true
tags:
  - Math
  - Introduction
  - elementary algebra
  - Factorization
series: 
  - Math
---

## Overview

Sometimes when we're trying to solve the unknown factor of an equation, an integral, the definition of derivative by limits or just rationalizing an expression and we need to simplify it; A very straightforward and popular technique is to factorize it to simplify the whole expression by converting addition/substraction into a product of factors.

There're multiple well-known patterns that we can recognize, such as common factor, binomials, difference of two squares, sum/difference of two cubes; We're gonna see how to resolve each of them step by step.

Remember that this post is meant to be as an easy introduction where a lot of mathematical rigorousness is lost.

## Common factor

Given the following expression: $$2a + \frac{1}{2}a^2 - b$$ We  notice there is a term that appears twice but we can't reduce them because they aren't similar (same variable but different powers). So in order to simplify this out we can extract the common factor (variables) with the highest power and multiply it (the common factor) by the quotient of each term and the factor, see:
$$ \text{The common factor is } a^2 \text{ so that: }$$
$$ \rightarrow a^2 \cdot (\frac{a^2}{a} + \frac{1}{2} \frac{a^2}{a^2} - \frac{a^2}{b})$$ 
$$ \rightarrow a^2 \cdot (a + \frac{1}{2} - \frac{a^2}{b})$$
