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

So any nonzero number a has finitely many divisors.
(on the other hand, all $x \in \mathbb{Z}$ divide zero, since $x*0 = 0$)

### 1.3 Lemma: (Division with remainder)

Let $a \in \mathbb{Z}$ and $m \in \mathbb{N}$. Then there exist *unique* elements $r, q \in \mathbb{Z}$ satisfying \[a = q*m +r \text{ and } r \in (0, ..., m-1)\]
The number r is the remainder of *a modulo m*.  

Proof: (existence) Let q be the integer with the property that $q \leq \frac{a}{m} < q + 1$. Set $r:=a-q*m$

Then $q, r \in \mathbb{Z}$, and: $$r = a-qm(=)qm+r=a$$
\[r \geq a = \frac{a}{m}*m = 0\]
\[r - m = a - (q+1)m\]
\[ \\ \\  < a - \frac{a}{m}m\]

(Uniqueness) Assume that $q'$ and $r'$ also satisfy the conitions. Then 
\[m > |r - r'|\]

$(a = qm +r , a = q'm + r  => r + qm = r' + q'm => r - r' = m(q*q'))$

So m divides $r-r' => r - r' = 0$. So $r = r'$, and thus $q=q'$

### 1.4 Example
For $a = -8$ and $m = 3$, $a=-3*m+1$ so $q=-3
 and $r=1$

 For $a =8$ and $m = 3, $a=2*m+2$ so $q=2, r =2$

### 1.5 Remark
Let $a \in \mathbb{Z}, m \in \mathbb{N}$, and let r be the only remainder of a modulo m, the $m|a$ if and only if $r=0$.

### 1.4 Definition
 Let $a, b \in \mathbb{Z}$ not both zero, the GCD of a and b is the larget number $d \in \mathbb{N}$ with $d|a$ and $d|b$.

write $gcd(a,b) = d$

### 1.7 Remark: From the definition, we can note:
- $gcd(a,b) = gcd(b,a)$
- if $a \neq 0, gcd (a,0) = |a|$