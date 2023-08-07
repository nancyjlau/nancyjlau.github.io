---
title: Intro to Proofs
date: 2023-08-07
description: intro to proofs notes
tags: [math]
---

## Proof Guidelines
- Always begin your proof with carefully restating, in words, the assumptions and the result(s) that needs to be proved.
- A written proof is the presentation of your mathematical ideas. Since it's a presentation, it needs to be narrative, so always replace logical symbols with their English counterparts (e.g. instead of
$\exist$ write `there exists", instead of $\or$
write `or' etc.)
- Since a written proof is a presentation, the reader is a part of this; therefore use the pronoun `we'.
- Always write the proof as if it's going to be read by a peer; that's your audience.
- Within your proof, always highlight or display important equations or calculations and mathematical expressions.
- Clearly indicate the various cases you may have to consider in a proof.
- Indicate the completion of your proof.
- Most importantly: examples do not constitute a proof.


## Lecture 4 - Prelecture

### Proof by Contrapositive

\[(P \implies Q) \equiv (\neg Q \implies \neg P)\]

$\neg Q \implies \neg P$ is called the *contrapositive* of the statement $P \implies Q$

Example:    
What is the contrapositive of the statement: if $x \neq 0$, then $|x| > 0$

Solution:    
Since $|x|$ is never negative, the negation of $|x| > 0$ is, in fact, $|x| = 0$. Therefore, the contrapositive of the given statement is: 

\[if \\ |x| = 0, then \\  x = 0\]

With this logical equivalence in hand, *proof by contrapositive* is that method of proof where instead of providng a direct proof of
\[ \text{for all } x \in S, if \\ P(x), \\ then \\ Q(x)\]

we provide a direct proof of tis contrapositive
\[ \text{for all } x \in S, if \\ \neg Q(x), \\ then \\ \neg P(x)\]

Example:   
Prove that if $n^2 + 1$ is odd, then $n$ is even. 

Proof:   
We provide proof by contrapositive. Assume n is odd, we need to show that $n^2 + 1$ is even. Since $n$ is odd, we may write n = 2k+ 1 for an integer k. Hence,

\[n^2 + 1 = (2k+1)^2 + 1 = (4k^2 + 4k + 1) + 1 = 4k^2 + 4k + 2 = 2(2k^2 + 2k + 1)\]

Since $2k^2 + 2k + 1$ is an integer, we obtain that $n^2 + 1$ is even; as needed to be shown.

If you try to provide a direct proof for the example above, you can see that proof by contrapositive provides a cleaner proof than a direct proof. 

Remember the [proof guidelines](https://nancyjlau.github.io/posts/intro-to-proofs/#proof-guidelines)!!
