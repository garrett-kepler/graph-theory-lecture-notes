---
author:
  - Garrett J. Kepler
date: Updated
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 7: Principle of Inclusion-Exclusion (P.I.E.) & the D.I.E. Method

## Principle of Inclusion-Exclusion

Thus far, we've covered a very simple counting problem using set theory:
For two sets $A,B$, if they are disjoint $(|A\cap B|=0)$, we know that
$|A\cup B|=|A|+|B|$. For example, recall the problem of disjoint sets of
students: "How many people are in Math 325 or Physics 533 if they occur
at the same time?". That is, to count the number of things in the set
$A\cup B$ we could just count the number of things in $A$ once, count
the number of things in $B$ once, and sum them.

\centering
[\[fig:my\_label\]]{#fig:my_label label="fig:my_label"}

However, in the case that $A$ and $B$ are not disjoint, we run into a
problem. If we count the number of elements in $A$, then count the
number of elements in $B$, we end up counting their shared elements
twice!\

\centering
So, to count $|A\cup B|$, we must correct this over counting by
*excluding* a copy of the set we over-counted. Counting $A$, we get
$|A|$. Counting $B$, we get $|B|$. Since we count $|A\cap B|$ twice, we
can count $A\cup B$ in a straightforward way:
$|A\cup B|=|A|+|B|-|A\cap B|$. That is, by counting $A$ and $B$, we
over-count $A\cap B$, so we correct this to find $|A\cup B|$ (see Figure
[\[fig:simplepie\]](#fig:simplepie){reference-type="ref"
reference="fig:simplepie"} for a visual aid).\

\centering
[\[fig:my\_label\]]{#fig:my_label label="fig:my_label"}

\newpage
This is the idea of the *Principle of Inclusion-Exclusion (P.I.E.)*: We
want to count the union of sets so\...

- Include count of the individuals
- Exclude count of the pairwise intersections Include count of the
   triple-wise intersections
- Exclude count of the quadruple-wise intersections
- Include count of the quintuple-wise intersections $$\begin{aligned}
   \vdots\\
   \vdots
   \end{aligned}$$

For those who are curious, there is a formula: $$\begin{aligned}
\left|\bigcup_{i=1}^nA_i \right|&=\sum_{i=1}|A_i|-\sum_{1\leq i<j\leq n}|A_i\cap A_j|+\sum_{1\leq i<j<k\leq n}|A_i\cap A_j\cap A_k|-\cdots+(-1)^{n+1}|A_1\cap \cdots\cap A_n|\\
&=\sum_{\emptyset\neq I\subseteq\{1,2,\dots, n\}}(-1)^{|I|+1}\left|\bigcap_{i\in I}A_i\right|\end{aligned}$$

though this is algebraic formulation is not often used in practice.

## D.I.E. Method

Oftentimes we are faced with a sum of the following form:
$$\begin{aligned}
\sum_{k=1}^n(-1)^kf_k&=(-1)^nf_{n-1}\end{aligned}$$ where $f_k$ is
the $k$-th Fibonacci number. Luckily, we have been equipped with
experience with these numbers. We may even have an idea of rephrasing
this sum combinatorially. For example, we know that $f_k$ counts the
number of ways to tile a $1\times k$ board with squares and dominos.
This alternating seems to define a relationship between the tilings. How
might we prove such a sum?  
Thinking this specific example through, we see for even $k$, we have a
coefficient $1$. For odd $k$, we have a coefficient $-1$. It is almost
like the even tilings are naturally assigned 1 and odd tilings are
naturally assigned -1. This sum seems to tell us that the set of tilings
of every size has been split in two. But, for some reason they haven't
been paired up all the way (i.e. why is there a $(-1)^nf_{n-1}$ on the
right hand side?).  
This vein of thinking led to the useful cousin of inclusion and
exclusion called the D.I.E. method. It proceeds as follows:

1. : Describe what the sum counts *ignoring* the alternating
2. : Define a sign-reversing involution between the sets of opposite
   parity
3. : Count how many exclusions occur

Without defining involution yet, we'll discuss how a result might be
proven. We already have a combinatorial model set up, so let's try the
D.I.E. method out:

\hfill
Prove that $$\begin{aligned}
\sum_{k=1}^n(-1)^kf_k&=(-1)^nf_{n-1}
\end{aligned}$$

\hfill

1. : Ignoring the alternating, $\sum\limits_{k=1}^nf_k$ counts the
   number of ways to tile $1\times k$ boards of size $1$ through $n$
   using squares and dominos.
2. : Recall that even tilings are assigned 1 by our sum and odd tilings
   assigned -1. Consider "toggling" the last tile of a tiling by
   replacing it with the opposite tile. That is, if the tiling ends in
   a square, remove it and place a domino. Likewise, if the tiling ends
   in a domino, remove it and place a square. Since removing a square
   and replacing it with a domino increases the size by 1, the tiling
   length changes from even to odd or odd to even. Likewise, replacing
   a domino with a square changes the length of the tiling from even to
   odd or odd to even. So, no matter what, we change "parity" (even/odd
   switch) and are "sign-reversing" (1/$-1$ switching). Also, if we
   toggle the last tile twice, we result in the same tiling and are an
   "involution".
3. : What could go wrong? Well, if we have a tiling of the $n$ board
   that ends in a square, we will toggle it and end up with a tiling of
   the $n+1$ board. But, we don't care about these tilings because our
   sum ends at $n$-sized boards. So, how many are there? Well, if our
   $n$ board tiling ends in a square and we remove it, what do we have?
   A tiling of the $n-1$ board. There are $f_{n-1}$ such tilings. So,
   whatever $n$ is assigned, we have not paired up $f_{n-1}$ tilings in
   that assignment. That is, we have $(-1)^nf_{n-1}$ as a leftover
   term.
4. : We have paired up each odd tilings with an even tilings via a sign
   reversing involution _except_ $f_{n-1}$ tilings assigned $(-1)^n$.
   So, $$\begin{aligned}
   \sum_{k=1}^n(-1)^kf_k&=(-1)^nf_{n-1}
   \end{aligned}$$

Voilà! We have cleverly paired up our tilings to prove an otherwise hard
to intuit sum. This is the idea of D.I.E. method. Another example for
clarity:

\hfill
Prove that $$\begin{aligned}
\sum_{k=0}^n(-1)^k\binom{n}{k}=0
\end{aligned}$$

\hfill

1. : Ignoring the alternating, $\sum\limits_{k=0}^n\binom{n}{k}$ counts
   the number of subsets of $\{1,2,\dots, n\}$ of sizes 1 through $n$.
2. : Note that for even $k$, we have a coefficient of 1. Meanwhile, odd
   $k$ gives a coefficient of -1. So, even sized subsets are
   assigned 1. Meanwhile, odd subsets are assigned -1. Consider
   "toggling" the element 1 in a subset. That is, if 1 is in the
   subset, remove it. If not, add it. Then, the parity of the subset
   will change (even to odd or odd to even) and so the assignment (1 to
   -1 or -1 to 1). So, this operation is sign-reversing. Removing 1
   then including 1 will result in the same subset. Likewise with
   including 1 and then removing it again. So, this operation is an
   involution.
3. : If a subset has 1 in it and we remove it, we obtain a subset of
   opposite parity. Otherwise, the subset does not have 1 and we add it
   to obtain a subset of opposite parity. So, each subset is paired up
   and we have no exceptions.
4. : We have paired up each odd sized subsets of $\{1,2,\dots,n\}$ with
   even sized subsets of $\{1,2,\dots, n\}$ via a sign reversing
   involution with no exceptions. So, $$\begin{aligned}
   \sum_{k=0}^n(-1)^k\binom{n}{k}=0
   \end{aligned}$$

Pretty clever! Hopefully by now you have some idea for what a
"sign-reversing involution" does. Formally, this is what we are after:

\hfill
A function $f:A\to B$ is an *involution* if $f(f(a))=a$ for all
$a\in A$. The involution $f$ is then *sign-reversing* if $f(a)$ and $a$
differ in sign for all $a\in A$.
