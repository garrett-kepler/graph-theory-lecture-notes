---
author:
  - Garrett J. Kepler
date: Updated
title: 'Lecture Notes on Combinatorics: Draft'
---


# Chapter 5

Week's Warmup

\hfill
Given 5 points on the surface of a sphere, show that there is a closed
hemisphere that contains 4 points. (A closed hemisphere is a sphere cut
in half including the boundary that was cut)

\hfill

1. How many ways are there to select $k$ objects from $n$?
2. After selecting, how many ways are there to permute those $k$
   objects?
3. How many ways are there permute $k$ objects from $n$?

Courtesy of Zvezdelina Stankova, a combinatorial thinking builder:

\hfill
Given $n$ points on the boundary of a circle, connect each pair of
points such that only two lines intersect at any point. How many regions
does this create?

\hfill
For 1 point, this is an easy answer: 1 region, the circle itself. For 2,
also fairly straightforward: 2. For 3, we get 4. Powers of 2! Pictures
from:
[ThreeSixty360](https://threesixty360.wordpress.com/2008/04/30/1-2-4-8-what-comes-next/).

![image](math 325/book/content/photos/Screenshot 2026-02-15 192106.png){width=".5\textwidth"}

We can continue this process and find the answer for higher numbers of
points:

![image](math 325/book/content/photos/pizza.png){width=".5\textwidth"}

With a fair bit of zooming in, you may count 1,2,4,8,16, and then\...
31. This strange sequence exemplifies the need for combinatorial
reasoning. Although we may conjecture a relationship between a sequence
and a process like this, without proof, we know close to nothing! So, be
careful when conjecturing.

\hfill
Given an $n\times n$ board, how many ways can we place $n$ points so
that no point shares a column or row with any other point?

This question formulated differently, is what we call the "non-attacking
rook position" problem. Given an $n\times n$ chess board, we want to
places $n$ rooks so that no rook can attack any others. As an example,
consider the following placement.

Each rook has been placed in a spot such that it is the only rook in its
respective row and column.

\hfill
Going column by column, consider placing a rook in the first column. No
other have been placed, so we can place this rook in $n$ ways. Now that
this rook has been placed, the rook we will place in second column can
be placed anywhere so long as it doesn't share the row from the first
rook. There are $n-1$ ways we can do this. Likewise, we can place the
rook to be in column 3 in any row except the rows of the 2 previous.
There are $n-2$ ways. Continuing on, we have
$n(n-1)(n-2)\cdots 3\cdot 2\cdot 1=n!$ total ways. (One could equally
think of this as a permutation problem!)

# Graphs

One fundamental combinatorial object we study in combinatorics is the
*graph*. You may have already seen these. For example, see Figure
[\[fig:network\]](#fig:network){reference-type="ref"
reference="fig:network"}. We will formalize the idea in this section.

\centering
![Examples of graphs. On the left, a network of the internet. On the
right, a graph corresponding to a molecule. Courtesy of
[https://en.wikipedia.org/wiki/Computernetwork](https://en.wikipedia.org/wiki/Computer_network)
and <https://en.wikipedia.org/wiki/Molecule>
respectively.[]{label="fig:network"}](math 325/book/content/photos/Internet_map_1024.png "fig:"){#fig:network
height="0.2\textheight"} ![Examples of graphs. On the left, a network of
the internet. On the right, a graph corresponding to a molecule.
Courtesy of
[https://en.wikipedia.org/wiki/Computernetwork](https://en.wikipedia.org/wiki/Computer_network)
and <https://en.wikipedia.org/wiki/Molecule>
respectively.[]{label="fig:network"}](math 325/book/content/photos/TOAT_AFM.png "fig:"){#fig:network
height=".2\textheight"}

\hfill
A *graph* $G=(V,E)$ is a collection of vertices $V$ and edges $E$ where
$E$ is a set of pairs of vertices.

We can synonymously call vertices and edges nodes and arcs, but I will
try to remain consistent with the former. We typically assume $E$ is a
set of edges defined over $V$. Otherwise, this object would indeed be
hard to interpret. Consider the following graphs.

\hfill
Let $G=(\{1,2,3\},\{(1,2),(2,3)\}$. Then, we can visualize $G$ as

Notice, if we remove $(2,3)$, we end up with a different, yet similar
graph $H=(\{1,2,3\},\{(1,2)\}$

Note that in drawing these graphs, we have an ordered pair $(x,y)$
telling us our edge begins at $x$ and ends at $y$. As such, we have an
arrow indicating the starting node and ending node for each edge. A
graph where this *direction* is important we call a *directed graph*. If
instead, order does not matter, we have an *undirected graph*.

\hfill
A graph $G=(V,E)$ is *directed* when $E$ consists of *ordered pairs* of
vertices (e.g. $(2,3)$). Conversely, a graph is *undirected* when $E$
consists of *unordered pairs* of vertices (e.g. $\{2,3\}$).

Consider the graph from before, $G=(\{1,2,3\},\{(1,2),(2,3)\}$.

We can form an undirected analogue, $H=(\{1,2,3\},\{\{1,2\},\{2,3\}\}$.

Note, we do not require that the vertices in an edge be distinct. That
is, we could have a *self-loop* $(x,x)$ for some $x\in V$.

We also do not require that there is only one edge between a pair of
nodes.

We can even weight edges!

These objects can be very complicated indeed. As such, we can further
restrict our graphs to what we call *simple*.

\hfill
A *simple* graph is an undirected, unweighted graph without self-loops
and multiple edges.

A simple graph is arguably the easiest graph to think of. But, simple
and not simple graphs have the pros and cons when dealing with them in
practice. Consider the following question:

\hfill
How many simple graphs in general are there on $n$ nodes?

\hfill
For an edge to exist, we have to pair up two nodes. How many ways can we
do this? $\binom{n}{2}$ ways. For each of those potential edges, there
is 2 possibilities: the edge exists or it doesn't. So, by multiplication
principle, there are $2^{\binom{n}{2}}$ possible graphs in general.

Okay, $2^{\binom{n}{2}}$ in general. But, consider the two following
graphs.

Intuitively, these are representatives of the same structure. One could
say these are the same graph with different labels. This idea is what we
call *isomorphic graphs*. The question of "How many simple
*non-isomorphic* graphs are there on $n$ nodes?" is a much more
difficult question to answer. We will come back to this.  
There are many features of graphs we care about. One particular example
is the number of edges each node is represented in.

\hfill
The number of edges incident with a node $v$ is the *degree* of $v$
denoted $d(v)$.

\hfill
For the following graph, the degree of each node is: $d(1)=1$, $d(2)=2$,
and $d(3)=1$.

\hfill
Let $G=(V,E)$. Then, $$\begin{aligned}
\sum_{v\in V} d(v)&=2|E|
\end{aligned}$$

\hfill
For each node $v$, $d(v)$ counts the number of edges $v$ appears in
(i.e. the number of edges $(v,u)$ or $\{v,u\}$). The sum over all $v$
will count $(v,u)$ and $(u,v)$ for every edge in the graph. As such, we
count twice the number of edges in the graph.

\hfill
In a graph $G$, there are an even number of odd degree nodes.

\hfill
Let $x,y\in \mathbb{R}$. Then, $$\begin{aligned}
(x+y)^n&=\sum_{k=0}^n\binom{n}{k}x^ky^{n-k}
\end{aligned}$$

On the left, we have $n$ factors of $(x+y)$,
$(x+y)^n=(x+y)(x+y)\cdots (x+y)$. The coefficient of $x^k$ will be the
number of ways to choose $x$ from the total factors. Since we have $n$,
we also choose $y^{n-k}$ as a consequence. This corresponds to selecting
$k$ terms to contribute to the coefficient of $x^ky^{n-k}$ from $n$
factors. Since we can do this in $\binom{n}{k}$ ways, the coefficient of
$x^ky^{n-k}$ is $\binom{n}{k}$. Adding from $k=0$ to $k=n$ gives *all*
the ways we can do this.

\hfill
Using the binomial theorem, how many *directed* graphs are there on $n$
nodes in general?
