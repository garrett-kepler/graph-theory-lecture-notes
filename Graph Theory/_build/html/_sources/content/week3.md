---
author:
  - Garrett J. Kepler
date: Updated
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 3: Combinatorial Thinking Practicum

In this section, we'll go through a few key problems to develop our
intuition for combinatorial problems.\

## Trailing Zeroes in a Product

\hfill
Consider the set $S=\{1,2,3,\dots, 325\}$. How many zeroes are at the
end of the product $1\cdot 2\cdot 3\cdot \cdots \cdot 324\cdot 325$?
E.g. in $1\cdot 2\cdot 3\cdot 4\cdot 5=120$ there is one zero at the
end, but in $1\cdot 2\cdot 3\cdot 4=24$ there are none.

\hfill
: Note that there are more powers of two than 5 in our set (i.e. the
powers of 5 are $\{5, 25, 125\}$ while powers of 2 are
$\{2,4,8,16,32,\dots, 256\}$). We want to pair up 2's and 5's until we
run out of 5's. Try for yourself to verify there are 65 multiples of 5,
13 multiples of 25, and 2 multiples of 125 in $S$. Then, there are at
least 80 zeroes. Try and find why this implies there are *exactly* 80
zeroes.

## Points in a Square

\hfill
Given five points inside a 2 by 2 square, show that there are two points
whose distance is at most $\sqrt{2}$.

\hfill
: Consider partitioning the square into 4 equally sized squares.

The maximum distance between any two points is between the corners
themselves. This distance is $\sqrt{2}$. Since we have 5 points in 4
squares, by the pigeonhole principle, we have at least 2 points in one
square. These two points could be on the corners, which means the
distance between them is at most $\sqrt{2}$.

## Lattice Paths

\hfill
Consider an $m\times n$ grid with corners $(0,0), (0,n),(m,0)~\&~(m,n)$.
A *lattice path* is a path starting at (0,0) and ending at $(m,n)$ only
moving right and up.

\hfill
Below is an example of a lattice path on the $5\times 4$ grid.\

![image](math 325/book/content/photos/lattice path.png){width=".3\textwidth"}

\hfill
How many lattices paths are there an $m\times n$ grid?

\hfill
: Consider the steps we must make as a list
$L=\{\underline{\hspace{.7em}},\underline{\hspace{.7em}},\underline{\hspace{.7em}}, \dots,\underline{\hspace{.7em}}\}$.
To get from $(0,0)$ to $(m,n)$, we must move right $m$ steps and we must
move up $n$ steps. In total, we must make $m+n$ steps (i.e. $|L|=m+n$).
Note that if we choose when to go up/right, this determines when we must
go right/up. There are $\binom{m+n}{n}$ ways to select which steps
should be up's. We then fill the rest of the steps with right's.
Likewise, we could have also counted the ways to place right's,
$\binom{m+n}{m}$, and then place the up's. As such, there are
$\binom{m+n}{n}=\binom{m+n}{m}$ lattice paths in this case.

\hfill
How many lattice paths on an $m\times n$ grid do not cross the line
$y=x$? i.e. They can meet the points $(i,i)$ but not $(i+1,i)$.

\hfill
Below is an example of paths we want to consider. On the left, we have a
path that does not cross $y=x$ while on the right we do.

![image](math 325/lecture notes/week 3/goodpath.png){width=".3\textwidth"}
![image](math 325/lecture notes/week 3/badpath.png){width=".3\textwidth"}\

\hfill
: Consider the point after a path crosses the diagonal. Using the
example above, we have something like

![image](math 325/book/content/photos/latticepathproof.png){width=".3\textwidth"}

Assume we cross for some path. This point, $(x-1,x)$, we have gone up
one more time than we'd like. This means we will have $n-x$ more ups and
$n-x+1$ more rights to get to $(n,n)$.  
Keeping the path up to $(x-1,x)$ the same, let's reverse the direction
of everything afterward. Before, we had one more right than up ($n-x+1$
rights and $n-x$ ups). Now, we will now have one more up than right
($n-x$ rights and $n-x+1$ ups). Since every step before $(x-1,x)$ is
this same, we end up making $n-x$ more rights to end up at $n-1$ to the
right and making $n-x+1$ ups to end up at $n+1$ up. So, we have a
lattice path of the $(n-1)\times (n+1)$ grid.

![image](math 325/book/content/photos/latticepathproof2.png){width=".3\textwidth"}

This operation defines our function $f$ taking paths that cross the
diagonal in the $n\times n$ grid to lattice paths of the
$(n-1)\times (n+1)$ grid. $f^{-1}$ is simply taking a lattice path on
the $(n-1)\times (n+1)$ grid and reversing steps after crossing the
diagonal (try formalizing yourself!).  
Since we have a bijection, there are the same number of paths that cross
on the $n\times n$ grid as lattice paths on the $(n-1)\times (n+1)$
grid. There are $\binom{n-1+n+1}{n-1}=\binom{2n}{n-1}$ such lattice
paths on the $(n-1)\times (n+1)$ grid. Removing this from the total
$\binom{2n}{n}$ lattices path on the $n\times n$ grid, we get the number
that do not cross the diagonal: $$\begin{aligned}
\binom{2n}{n}-\binom{2n}{n-1}\end{aligned}$$

This expression forms an exceptionally useful sequence of numbers, the
*Catalan Numbers*. They count many, many things including rooted binary
trees, polygon triangulations, and more. For a reference list, see
<https://oeis.org/A000108>.

## Tilings

We are going to place objects on a $1\times n$ board. "Tiling" the board
means we cover the $n$ spots exactly.

\centering
=\[font=\] (2,9.75) -- (5.25,9.75); (2,9.75) -- (2,8.25); (2,8.25) --
(5.25,8.25); (4.5,7.25) -- (4.5,7.25); (5.25,9.75) -- (7.5,9.75);
(5.25,8.25) -- (7.5,8.25); (7.5,9.75) -- (9.25,9.75); (7.5,8.25) --
(9.25,8.25); (9.25,9.75) -- (9.25,8.25); (3.5,9.75) -- (3.5,8.25);
(5,9.75) -- (5,8.25); (7.75,9.75) -- (7.75,8.25);

\hfill
Let $t_n$ be the number of ways there are to tile the $1\times n$ board.
Find an expression for $t_n$ using $t_{n-1}$ and $t_{n-2}$ (i.e. some
function $t_n=f(t_{n-1},t_{n-2})$).

\hfill
: Consider a tiling of a $1\times n-1$ board. How can we extend this
tiling to a tiling of $1\times n$? By adding a $1\times 1$ square.
Likewise, we can extend a tiling of a $1\times n-2$ board to a tiling of
$1\times n$ by adding a domino. The extension of these tilings never
produce the same tiling of the $1\times n$ board. Moreover, any tiling
must end in either a domino or a square. So, a tiling of the $1\times n$
board is counted by these two cases. As such, $t_n=t_{n-1}+t_{n-2}$.

Consider then, $t_1$. There is only 1 way to tile a $1\times 1$ board,
with a square. $t_2$ gives 2: two squares or one domino. You might try
finding higher and higher values: $$\begin{aligned}
t_1&=1\\
t_2&=2\\
t_3&=3\\
t_4&=5\\
t_5&=8\\
\vdots\end{aligned}$$ You might immediately recognize the sequence,
the _Fibonacci Numbers_! This is arguably the most ubiquitous sequence
in combinatorics. The list of problems with Fibonacci numbers as the
solution is immense. For a brief list, refer here
<https://oeis.org/A000045>.

\hfill
Recall we defined $t_n$ to be the number of ways to tile the $1\times n$
board with $1\times 1$ squares and $1\times 2$ dominoes. How many ways
are there to tile a $2\times n$ board with $1\times 2$ dominoes?

\hfill
: Bijection! ($t_n=$ the number of tilings of the $2\times n$ board with
dominoes)

- $f$: Take a $2\times n$ tiling with $1\times 2$ dominoes. Split the
   board down the middle (horizontally) perhaps with some
   domino-cutting-strength scissors. We now have two copies of a tiling
   of the $1\times n$ board with $1\times 1$ squares and $1\times 2$
   dominoes.
- $f^{-1}$: Take two copies of the same $1\times n$ tiling with
   $1\times 1$ square and $1\times 2$ dominoes. Stack them on top of
   one other. Take the squares that lay on top of one another and
   replace them with a vertical domino. We now have the tiling of the
   $2\times n$ board with dominoes.

## {1,2}-sums

\hfill
Using just 1 and 2, how many ways are there to form a sequence that sum
to $n$? E.g. 1+1+2=1+2+1=4 are two examples of sequences that sum to 4.

\hfill
: We have already solved this!

- $f$: Take a sum $q_1+q_2+q_3+\dots+q_k=n$ where each $q_i$ is either
   1 or 2. We can create a tiling of the $1\times n$ board using $k$
   tiles as follows:

   - If $q_i=1$, the $i$-th tile will be a square.
   - If $q_i=2$, the $i$-th tile will be a domino.

   Since the sum of the $q_i$ terms must be $n$, we have a tiling of
   the $1\times n$ board.

- $f^{-1}$: Take a tiling of the $1\times n$ board using $k$ tiles. If
   tile $i$ is a square, let $q_i=1$. If tile $i$ is a domino, let
   $q_i=2$. Since the sums of the lengths of the tiles must be $n$, the
   sum of $q_i$ terms must be $n$.

We have a bijection, so there are the same number of ways to do each.
Since there are $t_n$ ways to tile the $1\times n$ board, we have $t_n$
ways to form the $\{1,2\}$-sums.
