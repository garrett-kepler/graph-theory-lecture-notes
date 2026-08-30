---
author:
  - Garrett J. Kepler
date: Updated
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 4: Combinatorial Models

## Week's Warmups

\hfill
How many ways are there to select 4 mathematicians and 10 statisticians
from a group of 50 mathematicians and 60 statisticians?

\hfill
How many ways are there to select 4 mathematicians or 10 statisticians
from a group of 50 mathematicians and 60 statisticians?

\hfill
I need to downsize. I select 3 scarves and 2 jackets to donate to the
local thrift store. If I have 10 scarves and 6 jackets, how many ways
can I do this?

\hfill
Selecting 3 scarves from 10 gives $\binom{10}{3}$. Selecting 2 jackets
from 6 gives $\binom{6}{2}$. So, there are $\binom{10}{3}\binom{6}{2}$
ways to do this.

## What is a Combinatorial Model?

Consider this final warmup problem. Notice, I could have reversed this
process as well, selecting jackets then scarves. So,
$\binom{10}{3}\binom{6}{2}=\binom{6}{2}\binom{10}{3}$. But, what if I
instead asked the following question? (To motivate this section's topic)

\hfill
Show $\binom{10}{3}\binom{6}{2}=\binom{6}{2}\binom{10}{3}$.

Extremely easy to show algebraically, but we can double count!

  
First, we must identify a problem that these formulae count. Perhaps, we
can hypothetically select scarves and jackets!

- **Problem**: How many ways are there to select $3$ scarves and 2
   jackets from 10 scarves and 6 jackets?
- **LHS**: I don't care about my scarves as much. So, we can select
   the 3 scarves first in $\binom{10}{3}$ ways. We can select the 2
   jackets second in $\binom{6}{2}$ ways. So, in total we can select
   $3$ scarves and 2 jackets from 10 scarves and 6 jackets in
   $\binom{10}{3}\binom{6}{2}$ ways.
- **RHS**: I need time to admire my scarf collection. So, we can
   select the 2 jackets first in $\binom{6}{2}$ ways then the 3 scarves
   in $\binom{10}{3}$ ways. So, in total we can select $3$ scarves and
   2 jackets from 10 scarves and 6 jackets in
   $\binom{6}{2}\binom{10}{3}$ ways.
- **Conclusion**: Therefore,
   $\binom{10}{3}\binom{6}{2}=\binom{6}{2}\binom{10}{3}$.

The trick is that I created a scenario to help me prove the
combinatorial identity
$\binom{10}{3}\binom{6}{2}=\binom{6}{2}\binom{10}{3}$. This is the idea
behind a *combinatorial model*. For clarity, recall the process of
double counting:

Double counting is the proof technique commonly used in combinatorics to
prove identities. Consider a question of the form "Show =". Double
counting would proceed as follows:

- **Identify Problem**: Find a problem that the LHS and RHS count
   solutions to.
- **LHS**: Count once to obtain a formula, LHS.
- **RHS**: Count the same problem a different way to obtain a formula,
   RHS.
- **Conclusion**: Therefore, LHS=RHS.

Often, the hard part is identifying a problem to count. This is where
*combinatorial models* come in. Much like the jacket and scarf scenario,
we can use a hypothetical scenario that is counted by the identity we
are given (LHS=RHS).

## Tiling Model

We have already discussed an important combinatorial model: the
***tiling model***. Recall, we proved the following:

The number of tilings of a $1\times n$ board with squares and dominoes,
$t_n$, is given by $F_{n}$, the $(n)$-th Fibonacci number.

Where the Fibonacci number $F_i$ is defined by $F_i=F_{i-1}+F_{i-2}$ for
$i\geq 2$ with $F_0=1$ and $F_1=1$.  
We then used the tiling model to prove the following result:

Using just 1 and 2, there are $F_{n}$ ways to form a sequence that sums
to $n$. E.g. 1+1+2=1+2+1=4 are two examples of sequences that sum to 4.

What we did was find a correspondence between a $1\times n$ tiling using
squares and dominoes with sums of 1's and 2's.  
This is the key: ***we took an identity we wish to solve and used an
interpretable scenario to prove it***. Combinatorial models are
scenarios that allow us to prove results. Just like with bijections,
combinatorial models allows us to take a problem we do not know how to
solve and equate it with one we do.

\hfill
Using a tiling model, show that $F_0+F_1+F_2+\dots +F_n=F_{n+2}-1$

\hfill
__Problem__: How many ways are there to tile a $1\times (n+2)$ board
using at least one domino?  
__RHS__: Taking all the tilings of the board, we have $F_{n+2}$.
Removing the tiling of all squares, we have the number of tilings with
at least one domino, $F_{n+2}-1$.  
__LHS__: Consider the rightmost domino in a tiling of the
$1\times (n+2)$ board. To the right of this domino, there will be all
squares. Assuming there are $k$ squares to the right of this rightmost
domino, we have a board of length $n-k$ to the left of the domino. This
board can be tiled in $F_{n-k}$ ways. Since we can have $k=0$ squares to
the right all the way to $k=n$ squares to the right, we consider tilings
of each $1\times (n-k)$ board for all $k=0,1,2,\dots,n$. We can't have a
shared tiling of differently sized boards, so we add $F_{n-k}$ for each
size of board. Thus, we have $F_0+F_1+\dots+F_n$ total ways to tile the
$1\times (n+2)$ board.  
__Conclusion__: Since these expressions count the number of ways to tile
a $1\times (n+2)$ board using at least one domino, we conclude
$F_0+F_1+F_2+\dots +F_n=F_{n+2}-1$.

## Lattice Path Model

We also discussed another important model: the ***lattice path model***.
Recall, we found the following:

There are $\binom{m+n}{m}$ lattice paths on a $m\times n$ grid.

There are $\binom{2n}{n}-\binom{2n}{n+1}$ lattice paths on the
$n\times n$ grid that do not cross the $y=x$ line.

Again, we can use this model to prove other results:

\hfill
Use a lattice path model to show
$\binom{2n}{n}=\binom{n}{0}^2+\binom{n}{1}^2+\dots+\binom{n}{n}^2$ (or
equivalently $\binom{2n}{n}=\sum\limits_{k=0}^n\binom{n}{k}^2$).

\hfill
**Problem**: How many lattice paths are there on the $n\times n$ grid?  
**LHS**: We know from before, that there $\binom{2n}{n}$ lattice paths.  
**RHS**: Consider some column $k$ on our grid:

![image](math 325/book/content/photos/columnlattice.png){width=".3\textwidth"}

At some point, every lattice path must meet each column
$k=0,1,2,\dots, n$ by definition of a lattice path. Using the same
intuition when proving the general formula for lattice paths, consider
the path we took to meet the column $k$. We must have gone right $k$
times. There are $\binom{n}{k}$ ways to select when to go right. After
meeting this column, there are $n-k$ more right moves to make. We can do
this in $\binom{n}{n-k}$ ways. So, there are
$\binom{n}{k}\binom{n}{n-k}=\binom{n}{k}\binom{n}{k}=\binom{n}{k}^2$
ways for each $k$. Since selecting when to move right determines when we
move up, we have covered every lattice path. Therefore, there are
$\sum_{k=0}^n\binom{n}{k}^2$ total lattice paths.  
__Conclusion__: Since both formulas count how many lattices paths there
are, $\binom{2n}{n}=\sum_{k=0}^n\binom{n}{k}^2$.

## Committee Selection Model

The last model we'll discuss is the model of **committee selection**. We
consider the following simple scenario:

- There are some number of people in a club.
- They select committee members.
- Perhaps they select a chair or some number of chairs for the
   committee.

We then count the number of ways they could make this selection.
Apparently simple, but very useful!

\hfill
Use a committee selection model to show $$\begin{aligned}
n\binom{2n}{n}=(n+1)\binom{2n}{n+1}
\end{aligned}$$

\hfill
**Problem**: How many ways are there to select a committee of size $n$
with a chair from a club of $2n$ people?  
**LHS**: The chair could be considered a committee member. We could
select $n$ committee members in $\binom{2n}{n}$ ways. Then, select a
chair from the committee members in $\binom{n}{1}=n$ ways. So, there are
$n\binom{2n}{n}$ ways to create a committee of size $n$ with a chair.  
**RHS**: The chair could not be considered a committee member. We could
select $n+1$ people who could be a committee member or the chair in
$\binom{2n}{n+1}$ ways. We could then select the chair from the $n+1$
people in $\binom{n+1}{1}=n+1$ ways. So, there are $(n+1)\binom{2n}{n}$
ways to create a committee of size $n$ with a chair.  
**Conclusion**: Since the LHS and RHS count the number of ways to form a
committee in this case, $n\binom{2n}{n}=(n+1)\binom{2n}{n}$.

## Committee Selection Model

\hfill
Use a committee selection model to show that $$\begin{aligned}
k\binom{n}{k}=(n-k+1)\binom{n}{k-1}
\end{aligned}$$

\hfill
**Problem**: How many ways are there to select a committee of size $k$
with a chair from a club of $n$ people?  
**LHS**: Selecting the committee can be done in $\binom{n}{k}$ ways.
From that committee, we can select a chair in $\binom{k}{1}=k$ ways. So,
there are $k\binom{n}{k}$ total ways we can select a committee with
chair in this case.  
**RHS**: Selecting the $k-1$ committee members who are *not* the chair
can be done in $\binom{n}{k-1}$ ways. We can then select the chair from
the leftover $n-(k-1)$ people in $\binom{n-k+1}{1}=n-k+1$ ways. So,
there are $(n-k+1)\binom{n}{k-1}$ total ways we can select a committee
in this case.  
**Conclusion**: Since the LHS and RHS count the number of ways to form a
committee in this case, $k\binom{n}{k}=(n-k+1)\binom{n}{k-1}$.

## Combinatorial Model Practice

For each of the following, use the given model to describe what the LHS
and RHS of the given identities is counting in terms of the model.

- Committee Selection:
   $\binom{m+n}{3}=\binom{m}{3}+\binom{n}{3}+\binom{m}{2}n+\binom{n}{2}m$
- Tiling: $\sum\limits_{k=0}^n\binom{n-k}{k}=F_n$
- Lattice Path:
   $\frac{1}{n+1}\binom{2n}{n}=\binom{2n}{n}-\binom{2n}{n+1}$

Show $F_{m+n}=F_mF_n+F_{m-1}F_{n-1}$ using a tiling model.
