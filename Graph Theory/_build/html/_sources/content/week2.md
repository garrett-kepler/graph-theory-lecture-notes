---
author:
  - Garrett J. Kepler
date: Updated 2.4.26
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 2: "Counting"

## Week's Warmups

\hfill
How many total subsets of $S=\{1,2,3,\dots, 50\}$ are there?

\hfill
Calculate $1+2+3+\cdots+49+50$. Could you form a general formula for
$1+2+3+4+\cdots+n$?

\hfill
Determine the number of subsets of $S=\{1,2,3,\dots,50\}$ whose sum of
elements is larger than or equal to 638.

\hfill

1. Consider a subset $\mathcal{S}$ of $S$.

   - For each $i=1,2,3,\dots, 50$, either $i$ is in $\mathcal{S}$ or
      not.
   - For each $i$, define $\mathcal{S}_{i}=\{0,1\}$ where $0$ is the
      case where $i$ is in $\mathcal{S}$ and 0 where $i$ is not.
   - Then, the total number of ways we can create subsets is given by
      $|\mathcal{S}_1\times \mathcal{S}_2\times \mathcal{S}_3\times \cdots\times \mathcal{S}_{50}|$.
   - By the multiplication principle, this tell us that there are
      $$\begin{aligned}
      |\mathcal{S}_1\times \mathcal{S}_2\times \mathcal{S}_3\times \cdots\times \mathcal{S}_{50}|&=|\mathcal{S}_1|\cdot |\mathcal{S}_2|\cdot |\mathcal{S}_3|\cdots |\mathcal{S}_{50}|\\
      &= 2\cdot 2\cdot 2\cdots 2=2^{50}
      \end{aligned}$$ possible subsets of $S$.

   This is a totally valid solution.  
   As you may know, there are multiple ways to solve a problem. So,
   let's try and solve this problem by finding a bijection. Consider
   taking a subset $A\subseteq S$.

   - For each element $s$ in $S$, $s$ is either in $A$ or not.
   - We could think of assigning each element $s$ a 1 or 0 depending
      on if it is in $A$ (say, 1 if $s\in A$, 0 if $s\notin A$).
   - Then, $f(A)$ could be a vector of length $n$ with entries 1
      or 0. For example,
      $f(\{1,3,4, 6\})=[1,0,1,1,0,1,0,\dots, 0]^T=X_A$.
   - What $f^{-1}$ be then? If the $i$-th entry of $X_A$ is 1, put
      $i$ in a set $A$. If the $i$-th entry of $X_A$ is 0, exclude $i$
      from $A$.
   - Thus, $f^{-1}$ exists and $f$ is a bijection. So, the number of
      subsets $A$ of $S$ equals the number of possible 0,1-vectors
      $X_A$ of size $|S|$.
   - How many vectors are there? There's 2 options for each $|S|$
      entries of a vector $X_A$. So, again, by the multiplication
      principle, there are $2^{|S|}$ possible such vectors. And so,
      the total number of subsets is equal to $2^{|S|}$.
   - In our case, this means there are $2^{50}$ subsets.

   There are multiple ways to solve a problem. The benefit of this is
   that we may learn different things about the objects in question.
   For example, in the bijection proof we learn about the relationship
   between 0,1-vectors of size $n$ and total subsets of a set of size
   $n$. They are equivalent!

2. You might try the following: $$\begin{aligned}
   L &= 1+2+3+\cdots+49+50\\
   \implies 2L &= 1+2+3+\cdots+49+50\\
   &+50+49+48+\cdots+2+1\\
   \implies2L&= (1+50)+(2+49)+(3+48)\\
   &+\cdots
   +(49+2)+(50+1)\\
   &= 51+51+51+\cdots+51+51\\
   &=50(51)\\
   \implies 2L&=50(51)\implies L=\frac{50(51)}{2}=1275
   \end{aligned}$$ This generalizes to $\frac{n(n+1)}{2}$ when we
   sum 1 through $n$.
3. Again, let us try and find a bijection. Let $T$ be the collection of
   all possible subsets of $S$. From warmup problem 1, we know
   $|T|=2^{50}$. From warmup problem 2, the sum of elements of $S$
   is 1275.

   - Let $A$ be the set of all subsets of $S$ whose sum is $\geq 638$
      and $B$ be the set of all subsets of $S$ whose sum is $<638$.
      Since either a subset sums to $\geq 638$ or $<638$ and not both,
      $A\cup B=T$ and $A\cap B=\emptyset$. Thus,
      $|T|=|A\cup B|=|A|+|B|$.
   - Moreover, if $A_i\in A$, then the sum of elements in $A_i$ is
      $\geq 638$. Since the sum of elements in $S$ is 1275, the sum of
      elements in $A_i^C$ must be less than or equal $1275-638=637$.
   - From Friday's class, we know $f(A_i)=A_i^C$ is a bijection. So,
      $|A|=|B|$.

   <!-- -->

   - So, $|T|=|A|+|B|=|A|+|A|=2|A|$.
   - Since $|T|=2^{50}=2|A|$, we know $|A|=2^{49}$.

   You might try and generalize this to $S=\{1,2,3,\cdots, n\}$ with a
   specific choice of sum for the subsets, say 325.

## Permutations, Combinations, & Double Counting

Combinatorics differs itself from many fields by its proof techniques.
We have been talking about bijections the last few classes. What
bijections allow us to do is say the following:

- We want to find a formula to count something
- We can transform the problem into an equivalent problem with a
   bijection
- Finding a formula in this equivalent problem tells us the count of
   the original problem

But, what if we found formulas for both problems? These are equivalent
problems, so they should have equivalent formulas!  
This is what is referred to as "double counting" or "counting with
equivalence" or "counting in two ways". The backbone of double counting
can be summarized as follows:

\hfill
If $f(n)$ and $g(n)$ are functions that count the solutions to a problem
involving $n$ objects, then $f(n)=g(n)$ for every $n$.

\vspace{.5em}
That is, if there are two equivalent ways to count something, they must
be equivalent all the time!

\hfill
A *combinatorial proof* works as follows:

- **Problem**: There is a problem of counting the number of solutions
   to a problem on $n$ objects.
- **LHS**: Count one way and find a function $f(n)$ counts these
   solutions.
- **RHS**: Count another way and find a function $g(n)$ counts these
   solutions.
- **Conclusion**: Then, $f(n)=g(n)$ for every $n$.

The result, $f(n)=g(n)$, is what we call a *combinatorial identity*.

\hfill
This first step is crucial. Sometimes we are given the problem we are
going to solve (e.g. "How many ways are there to permute $n$ objects?").
Then, we find two equivalent formulas. Other times, we are given an
identity to prove and we must identify a problem to count (e.g. "Prove
$\binom{n}{k}=\binom{n}{n-k}$"). Then, we must show that both the left
hand side and right hand side count the solutions to the problem we have
identified.

\hfill
A *selection* is the creation of a subset of a set. The resulting subset
is called a *combination*. We do not care about the ordering of the
elements. Simply what elements are chosen.

\hfill
The number of ways to select a subset of $k$ objects from a set $n$
distinct objects, $C(n,k)$, is denoted: $$\begin{aligned}
C(n,k)&=_nC_k=\binom{n}{k}
\end{aligned}$$ The right hand side is what we call a _binomial
coefficient_. We read this as "$n$ choose $k$".

\hfill
How many ways are there to make a sundae with 3 toppings from an ice
cream shop with 10 toppings?

\hfill
An *arrangement* is a selection . Each resulting ordered arrangement is
called a *permutation*.

\hfill
The number of ways to arrange $k$ objects from a set of $n$ distinct
objects, $P(n,k)$, is denoted: $$\begin{aligned}
P(n,k)&=_nP_k=(n)_k
\end{aligned}$$

\hfill
Out of the 20 karaoke competitors, how many ways are there to schedule
the performances of the 4 finalists?

\hfill
To recall a previous example "How many ways can we draw 4 labelled orbs
(A,B,C,D) from an urn without replacement?" Using the multiplication
principle, we found there was 4 options for the first draw, 3 for the
second, and so on giving a count of $4\cdot 3\cdot 2\cdot 1=4!=12$.
Equivalently, there are $P(4,4)$ ways.

\hfill
How many ways are there to arrange $k$ objects from a set of $n$
distinct objects?

\hfill

- **Identify Problem**: How many ways are there to arrange $k$ objects
   from a set of $n$ distinct objects?
- **LHS**: We know by definition $P(n,k)$ counts this.
- **RHS**: We can think of assigning $n$ objects to $k$ boxes. For box
   1, there are $n$ possible objects that can be assigned to it. For
   box 2, there are $n-1$ possible objects. Continuing on to the $k$th
   box, all $k-1$ boxes before it have an object, so there are
   $n-(k-1)$ possible objects that can be assigned box $k$. Using the
   multiplication principle, there are
   $n\cdot(n-1)\cdot (n-2)\cdot (n-(k-1))$ ways to do this.
- **Conclusion**: Thus, there are
   $P(n,k)=n\cdot (n-1)\cdot (n-2)\cdot (n-(k-1))$ ways to arrange $k$
   objects from a set of $n$.

The proof above allows us to immediately say the following as well:

\hfill
$$\begin{aligned}
P(n,k)=n\cdot (n-1)\cdot (n-2)\cdot (n-(k-1))=\frac{n!}{(n-k)!}
\end{aligned}$$ where
$n!=n\cdot(n-1)\cdot(n-2)\cdots 3\cdot 2\cdot 1$ and referred to as "$n$
factorial". By convention, $0!=1$.

Coming back to a version of our orbs and urn problem: "You draw from an
urn with 4 labeled orbs (A,B,C,D) one by one without replacement. How
many ways are there to do this?"

\hfill
We are arranging 4 objects from a set of 4. There are $P(4,4)$ ways to
do this. So, there are $P(4,4)=\frac{4!}{(4-4)!}=4!$ ways to do this.

We also asked the following: "You draw the orbs from the urn with
replacement, you write down 4 labels. How many ways are there to do this
so their is only a pair of repeats?" (e.g. (A,B,C,A) is okay but not
(D,D,C,D)).

\hfill
Consider a set of four slots $S$ in which you will write the labels. We
select one of the labels to repeat, there are 4 ways to do this. We
select 2 slots from the 4 slots for this label, there are
$C(4,2)=\binom{4}{2}$ ways to do this. After this label has been placed,
there are 3 labels to be arranged in 2 slots, there are
$P(3,2)=\frac{3!}{(3-2)!}=3!$ to do this. This means there are
$4\cdot C(4,2)\cdot P(3,2)=4\cdot\binom{4}{2}\cdot 3!$ ways in total to
get exactly one pair in this case. This is a totally valid response to a
combinatorics question. For an concise answer, we can simplify to obtain
144 ways.

\hfill
How many ways are there to draw $n$ labeled orbs from an urn with
replacement?

\hfill
How many ways are there to draw $n$ labeled orbs from an urn with
replacement only $m$ times when $m<n$? What about $m>n$?

Now that we have some practice with combinations and permutations, let's
get some practice with combinatorial proofs and show how they are
different from non-combinatorial proofs.

\hfill
Use a combinatorial proof to show that $P(n,k)=P(k,k)C(n,k)$.

\hfill

- **Identify Problem**: How many ways are there to arrange $k$ objects
   from a set of $n$ objects?
- **LHS**: By definition, $P(n,k)$ counts this.
- **RHS**: $C(n,k)$ counts the number of ways to select a subset of
   $k$ objects from a set of $n$. This ignores the order of the
   objects. For each $k$-element selection, there are $P(k,k)$ ways to
   arrange the elements. Thus, by the multiplication principle, there
   are $C(n,k)P(k,k)$ ways to arrange $k$ elements from a set of $n$
   objects.
- **Conclusion**: Therefore, $P(n,k)=P(k,k)C(n,k)$.

From the proof above, we can immediately algebraically deduce:

\hfill
$$\begin{aligned}
C(n,k)=\binom{n}{k}=\frac{n!}{k!(n-k)!}
\end{aligned}$$

\hfill
$$\begin{aligned}
P(n,k)=P(k,k)C(n,k)&\implies \frac{n!}{(n-k)!}=\frac{k!}{(k-k)!}C(n,k)\\
&\implies C(n,k)=\frac{n!}{k!(n-k)!}=\binom{n}{k}
\end{aligned}$$

\vspace{.5em}
What we've done here is simply use algebra and pre-established
relationships to reach our result. We have counted nothing. This is an
example of a *non-combinatorial proof*.

Using the above theorem, here is another good example of a
non-combinatorial proof:

\hfill
$$\begin{aligned}
\binom{n}{k}=\binom{n}{n-k}\end{aligned}$$  
(That is, the number of ways to select $k$ objects from $n$ is equal to
the number of ways to select $n-k$ objects from $n$.)

\hfill
$$\begin{aligned}
\binom{n}{k}=\frac{n!}{k!(n-k)!}=\frac{n!}{(n-(n-k))!(n-k)!}=\binom{n}{n-k}
\end{aligned}$$

How could we change this into a combinatorial proof?

\hfill
$$\begin{aligned}
\binom{n}{k}=\binom{n}{n-k}\end{aligned}$$

\hfill

- **Identify Problem**: How many ways are there to select $k$ objects
   from a set of $n$?
- **LHS**: By definition, $\binom{n}{k}$ counts the number of ways to
   select $k$ objects from a set of $n$ objects.
- **RHS**: By definition, $\binom{n}{n-k}$ counts the number of ways
   to select $n-k$ objects from a set of $n$. By including $n-k$
   objects in a set, we are creating a set of $k$ excluded objects. If
   instead, we select the $n-k$ objects from a set of $n$ to exclude,
   we are including the other $k$ objects. Thus, $\binom{n}{n-k}$
   counts the number of ways to select $k$ from a set of $n$.
- **Conclusion**: Therefore, $\binom{n}{k}=\binom{n}{n-k}$.

Double counting gives us many ways to count the same thing! A few great
examples:

\hfill
$$\begin{aligned}
\binom{n}{k}&=\binom{n}{n-k}=\frac{n}{n-k}\binom{n-1}{k}\\
&=\frac{n}{k}\binom{n-1}{k-1}=\binom{n-1}{k}+\binom{n-1}{k-1}
\end{aligned}$$

# Pigeonhole Principle

## Warmup Problem

\hfill
There are $n$ married couples waiting at tables around a dance floor.

1. Pairing the $2n$ people up to dance, how many ways are there to
   select a pair of dance partners?
2. How many people must be on the dance floor to guarantee a married
   couple is somewhere on the dance floor?

\hfill

1. This is a case where we would like to use our new notion of
   combination:

   - We are selecting 2 people from $2n$ people.
   - There are $C(2n,2)=\binom{2n}{2}$ ways to do this.

2. We want to *guarantee* that a married couple is on the dance floor.
   If we invite $n$ people to the floor, there is a chance we could
   have a couple. But, what if invite only one spouse from each couple?
   Then there is no couple on the floor. Consider this case.

   - Select one spouse from each married couple to the dance floor.
      There are now $n$ people ready to dance.
   - If we invite any one else to the dance floor, we are guaranteed
      their spouse is on the dance floor.
   - So, to *guarantee* we have a couple on the dance floor, we need
      to invite $n+1$ people to the floor.

This is what we call the *pigeonhole principle*. It is an incredible
powerful tool:

\hfill
If $n+1$ objects are distributed into $n$ boxes, then at least one box
contains two or more objects.

\hfill
If each of the $n$ boxes has at most one object, then the total number
of objects is at most $1+1+1+\cdots+1=n$. Since there is one object not
accounted for, we can say there exists some box that contains at least
two objects.

Out of Garrett, the Dean of the University, and the Chair of the Math &
Stats Department, there are at least two people either inside Garrett's
office or outside of Garrett's office.

We can also exploit a more generally case of the pigeonhole principle
when we have potentially more than $n+1$ objects:

\hfill
Let $q_1,q_2,\dots,q_n$ be positive integers. If $$\begin{aligned}
q_1+q_2+q_3+\cdots+q_n-n+1
\end{aligned}$$ objects are distributed into $n$ boxes, then
either the 1st box contains at least $q_1$ objects or the 2nd box
contains at least $q_2$ objects,$\dots$, or the $n$th box contains at
least $q_n$ objects.

\hfill
We distribute the $q_1+q_2+q_3+\cdots+q_n-n+1$ objects into $n$ boxes.
If each $i$th box contains less than $q_i$ objects, then the number of
objects in boxes is less than $$\begin{aligned}
(q_1-1)+(q_2-1)+\cdots+(q_n-1)&=q_1+q_2+\cdots+q_n-n
\end{aligned}$$ Since there is an object not accounted for, we
can say there exists a box $i$ with at least $q_i$ objects.

\hfill
Out of the 21 students in Math 325, there are 3 whose birthday lie on
the same day of the week.

What both the simple form and strong form of the pigeonhole principle
say in plain english is: ***distributing too many objects into too few
boxes forces overlaps***.  
Recall the 4 E's of combinatorics:

- Enumeration: How many ways...?
- Existence: Does there exist...?
- Extremal: What is the largest/smallest possible...?
- Expectation: What is the expected number of objects such that...?

We have been covering how to answer questions of enumeration. The
pigeonhole principle is our first technique to answer questions of
existence!  
For example, we can answer the following existence question using the
pigeonhole principle:

\hfill
Consider choosing 101 integers from $S=\{1,2,3,4,\dots, 200\}$. Show
that there are two chosen integers such that one divides the other.
Hint: try factoring out as many 2's as possible from each term in $S$.

\hfill
Each number in $S=\{1,2,3,4,\dots, 200\}$ is either even or odd.
Consider writing each integer $s\in S$ as $s=2^k\cdot t$ where $t$ is
odd and $k\geq 0$. Each $t$ comes from the set $T=\{1,3,5,\dots, 199\}$
of size 100. By picking 101 integers from $S$, we are also picking 101
odd factors from $T$. Since 101=100+1 factors are chosen from 100
factors, by the pigeonhole principle, there are two integers chosen from
$S$ that share a factor from $T$. That is, from the chosen integers of
$S$, there are two, say $s_1$ and $s_2$, such that $s_1=2^m\cdot t$ and
$s_2=2^n\cdot t$. Either $m>n$ and $s_2$ divides $s_1$ or $n>m$ and
$s_1$ divides $s_2$. As such, there are two integers such that one
divides the other.

This problem exemplifies why the pigeonhole principle is so useful:

- How many ways are there to select 101 integers from
   $S=\{1,2,3,\dots, 200\}$? $C(200,101)=\binom{200}{101}>10^{57}$.
- This is an insanely large number. More than the number of atoms in 1
   million Earths (Earth is about $\approx 10^{51}$ atoms).
- But, without going through every single possible subset choice, we
   know something about *every single one of these choices*. Namely,
   that there must be two numbers in each such that one divides the
   other.

\centering
=\[font=\] (5,11.75) to\[short, -o\] (5,11.75) ; (4.75,11.5) to\[short,
-o\] (4.75,11.5) ; (8.75,11.5) rectangle (8.75,11.5); (8.5,11.5)
rectangle (9.5,10.5); (9,10.5) rectangle (8.75,10.5); (9.25,8.75)
rectangle (9.25,8.75); (8.5,9.75) rectangle (9.5,8.75); (9,8.75)
rectangle (9,8.75); (9.5,11) rectangle (9.5,10.75); (9.5,11) rectangle
(9.5,10.5); (8.5,8) rectangle (9.5,7); (8.5,13) rectangle (9.5,12);
(tikzmaker) \[shift=(0, -0.125)\] at (3,8.75) ![Simple example of the
pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="0cm"}; (tikzmaker) \[shift=(.75, -0.75)\] at (3.5,7.75) ![Simple
example of the pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="1.5cm"}; (tikzmaker) \[shift=(-0.75, --0.75)\] at (5,12.75)
![Simple example of the pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="1.5cm"}; (tikzmaker) \[shift=(0.75, -0.75)\] at (3.5,9.25)
![Simple example of the pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="1.5cm"}; (tikzmaker) \[shift=(-0.65, --0.75)\] at (5,11.25)
![Simple example of the pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="1.5cm"}; (tikzmaker) \[shift=(0.75, -0.75)\] at (3.5,11) ![Simple
example of the pigeonhole principle (using
pigeons!)[]{label="fig:placeholder"}](math 325/lecture notes/week 3/pigeon.jpg "fig:"){#fig:placeholder
width="1.5cm"}; (4.75,13.5) -- (8.25,12.5); (5,12) -- (8.25,11);
(5,10.25) -- (8.25,9.25); (4.75,8.75) -- (8.25,7.5); (5.25,6.75) --
(8.25,7.25); at (9,12.5) 1; at (9,11) 2; at (9,7.5) 4; at (9,9.25) 3;

  
To end this section, let's work through a few problems:

\hfill
Pretend we are going to group the 21 Math 325 students into 4 study
groups. Each group will have a leader.

- How many ways can we select the leaders?
- Pretend we number the groups 1,2,3, and 4. How many ways can we
   assign leaders to groups?
- Use the pigeonhole principle to show that there is a group with at
   least 2 people.
- Use the pigeonhole principle to show that there is a group with at
   least 6 people.

\hfill

1. We are selecting 4 people from 20. There are $C(20,4)=\binom{20}{4}$
   ways to do this.
2. We are arranging 4 people into 4 groups. There are $P(4,4)=(4)_4=4!$
   ways to do this.
3. We are distributing 21 students into 4 groups. Considering the first
   5, we are placing 4+1 students into 4 groups. So, by the pigeonhole
   principle, there must be a group with at least two people.
4. Again, we are distributing 21 students into 4 groups. In other
   words, we are placing 21 = 6+6+6+6-4+1 people into 4 groups. By the
   pigeonhole principle, either group 1 has at least 6, group 2 has at
   least 6, and so on. So, there exists at least one group with at
   least 6 people in it.

\vspace{1em}
