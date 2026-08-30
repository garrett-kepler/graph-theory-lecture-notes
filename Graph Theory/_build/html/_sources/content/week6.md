---
author:
  - Garrett J. Kepler
date: Updated
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 6: Recurrence Relations & Generating Functions

## Week's Warmup

\hfill
Given the following expressions, we'll assume $n\geq 0$ is an integer.
Using the given values, we can plug in to the expression to find the
next term in the sequence. Conjecture a function $a_n=f(n)$ that does
depend on any terms before it in the sequence.

- $a_n=2a_{n-1}+1$ where $a_0=0$
- $a_{n+1}=a_n+a_{n-1}$ where $a_0=0$ and $a_1=1$
- $a_n=(a_{n-1})^{\frac{1}{n}}$ where $a_0=1$

\hfill

- Plugging in $a_0=0$ to obtain $a_1$, we get $a_1=2(0)+1=1$. We then
   use this to obtain $a_2$. We get $a_2=2(1)+1=3$. Repeating this
   process we get $7$ then $15$ then $31$ and so on. The sequence we
   get looks something $\{1,3,7,15,31,63,127,\dots\}$. You may notice
   these are almost powers of 2\... any conjectures for $f(n)$?
- Plugging in similar to before, we get $\{0,1,1,2,3,5,8,\dots\}$ the
   famous sequence we've been calling the "Fibonacci Sequence". What
   would $f(n)$ look like?
- A rather boring sequence, we get $\{1,1,1,1,\dots\}$. A simple
   formula for $f(n)$: $f(n)=1$.

But, how can we find $f(n)$ in general? That is the topic of this
section.

The mathematical object we have just interacted with is what we call a
*recurrence relation*. Firstly, note the following example.

\hfill
$a_{n+1}=3a_n-1$

This by itself does not generate a sequence. Notice in our warmup, we
were given some known values. These are necessary to determine a
sequence (otherwise why do we use them to count??).

\hfill
An equation relating the $n$-th term in a sequence as a combination of
the previous terms is called a *recurrence relation*. The given first
element (multiple elements) is called the initial value (values).

Once we have some initial values, the rest of the sequence is generated
uniquely. We will typically deal with integer valued recurrence
relations, but this need not be the case.

\hfill
$a_{n+1}=3a_n-1$ where $a_0=2$

So, how do we find the function $a_n=f(n)$? Though we may able to guess
at what this function may be, we need a mathematically rigorous way to
determine $f(n)$. What we will do is use a new type of machinery:
_generating functions_. Recall the following:

\hfill
The _geometric series_ $\sum\limits_{k=0}^{\infty}x^k$ converges to
$\frac{1}{1-x}$ when $|x|<1$. That is, if $|x|<1$, then
$$\begin{aligned}
\sum_{k=0}^{\infty}x^k=\frac{1}{1-x}\end{aligned}$$

Under this assumption $|x|<1$, we can find a simple, closed formula for
an infinite sum. We will implicitly assume this is satisfied for the
series we write. If we pretend we had $(cx)^k$ instead of $x^k$ for some
constant $c$, we will implicitly assume $|cx|<1$ so that we get a nice
formula for the infinite series.

\hfill
The _ordinary generating function_ (OGF) of some sequence
$\{a_0,a_1,a_2,a_3,a_4,\dots\}$ is the _power series_ of the form
$$\begin{aligned}
A(x)&=\sum_{k=0}^{\infty}a_kx^k
\end{aligned}$$

\hfill
Let the OGFs of $\{a_0,a_1,a_2,a_3,a_4,\dots\}$ and
$\{b_0,b_1,b_2,b_3,b_4,\dots\}$ be $A(x)$ and $B(x)$ respectively. Also,
let $c$ be some scalar. Then,

- $A(x)+B(x)$ generates
   $\{a_0+b_0,a_1+b_1,a_2+b_2,a_3+b_3,a_4+b_4,\dots\}$
- $c A(x)$ generates
   $\{c\cdot a_0,c\cdot a_1,c\cdot a_2,c\cdot a_3,c\cdot a_4,\dots\}$
- $x^kA(x)$ generates
   $\{\underbrace{0,0,\dots,0}_{k~zeroes},a_0,a_1,a_2,a_3,a_4,\dots\}$
- $\frac{d}{dx}(A(x))=A'(x)$ generates
   $\{a_1,2a_2,3a_3,4a_4,5a_5,\dots\}$
- $A(x)\cdot B(x)$ generates $\{c_0,c_1,c_2,c_3,c_4,\dots\}$ is where
   $c_n=a_0b_n+a_1b_{n-1}+a_2b_{n-2}+\cdots+a_nb_0$
- $\frac{A(x)}{1-x}$ generates $\{s_0,s_1,s_2,s_3,s_4,\dots\}$ where
   $s_n=\sum\limits_{k=0}^na_k$

\hfill
Consider $ax^2+bx+c$. Let $$\begin{aligned}
q_1(x)&= \frac{-b+\sqrt{b^2-4ac}}{2x}\\
q_2(x)&= \frac{-b-\sqrt{b^2-4ac}}{2x}\\
\end{aligned}$$ Then, we can factor $ax^2+bx+c$ in the following
ways $$\begin{aligned}
ax^2+bx+c&= a(x-q_1(a))(x-q_2(a))\\
&=c(1-q_1(c)x)(1-q_2(c)x)
\end{aligned}$$

+-----------------------+-----------------------+-----------------------+
| Formula               | Series                | Sequence              |
+:=====================:+:=====================:+:=====================:+
| $\frac{1}{1-x}$       | $\sum\limits_{k=0}^{\ | $\{1,1,1,\dots\}$     |
|                       | infty}x^k$            |                       |
+-----------------------+-----------------------+-----------------------+
| \[2ex\]               | $\sum\limits_{k=0}^{\ | $\{c\cdot b^0,c\cdot  |
| $\frac{c}{1-bx}$      | infty}cb^kx^k$        | b^1, c\cdot b^2,\dots |
|                       |                       | \}$                   |
+-----------------------+-----------------------+-----------------------+
| \[2ex\]               | $\sum\limits_{k=0}^{n | $\{\underbrace{1,1,1, |
| $\frac{1-x^n}{1-x}$   | -1}x^k$               | \dots,1}_{n~ones}, 0, |
|                       |                       |  0, \dots\}$          |
+-----------------------+-----------------------+-----------------------+
| \[2ex\]               | $\sum\limits_{k=n}^{\ | $\{\underbrace{0,0,\d |
|                       | infty}x^k$            | ots,0}_{n~zeroes},1,1 |
| \hline                |                       | ,1,\dots\}$           |
| $\frac{x^n}{1-x}$     |                       |                       |
+-----------------------+-----------------------+-----------------------+
| \[2ex\]               | $\sum\limits_{k=1}^{\ | $\{1,2,3,4,\dots\}$   |
| $\frac{d}{dx}\left(\f | infty}kx^{k-1}$       |                       |
| rac{1}{1-x}\right)$   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| \[2ex\]               |                       |                       |
+-----------------------+-----------------------+-----------------------+
