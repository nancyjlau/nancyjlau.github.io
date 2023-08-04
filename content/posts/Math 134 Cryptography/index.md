---
title: Cryptography Notes
date: 2023-08-04
description: basic cryptography notes
tags: [math, cryptography]
---

## Cryptography
How to encode + decode messages securely. We will approach this from a mathematical standpoint to understand these algorithms, we must understand:  
- number theory (divisibility, primes, modular arithmetic)
- abstract algebra (groups + rings)  

## Chapter 1 - The Integers and the Euclidean Algorithm  

### 1.1 Notation
$\mathbb{N}:= (1, 2, 3, \ldots)$ the natural numbers  
$\mathbb{N}:= \{0, 1, 2, 3, \ldots\} = \mathbb{N} \cup (0)$ the integers

### 1.2 Definition  
Let a, b $\in \mathbb{Z}$. We say *a is a multiple of b* and *b divides a* if there exists a $q \in \mathbb{Z}$ such that  

$bq = a \\ \\ \\ \\ \\ \\ $  $2 * 3 = 6$

6 is a multiple of 2 (and 3).  
2 and 3 divide 6

(also works for -2 *  -3 = 6)

We denote this by `b | a`  
`|` -> "divides"  

Note that if $a \neq 0$, then $q \neq 0$, so 
\[ | b |  = |b|*1 \leq |b| * |q| = |bq| = |a| \rightarrow |b| \leq |a|\] 

