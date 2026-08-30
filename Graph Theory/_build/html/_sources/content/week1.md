---
author:
  - Garrett J. Kepler
date: Updated 2.4.26
title: 'Lecture Notes on Combinatorics: Draft'
---

# Chapter 1: What is Combinatorics?

One great property of the field of combinatorics is most people have
already encountered combinatorial questions in their own life.

*Considering the optimal path we should take to get groceries and visit
the coffee shop then return home. Now that we have the groceries,
figuring out which set of dishes we can cook for the party when we've
invited a vegetarian, a non-vegetarian, and someone allergic to peanuts.
Now that we know what to cook, determining the best drinks paired with
which dishes.*

As simple of an example party planning is, we have described three
combinatorial problems already: minimal path, dish enumeration, and
drink/dish combinations.  
Many of the questions we ask in combinatorics focus on counting of some
sort.

- Enumeration: How many ways$\dots$?
- Existence: Does there exist$\dots$?
- Extremal: What is the largest/smallest possible$\dots$?
- Expectation: What is the expected number of$\dots$?

### Week's Warmups

\hfill
How many ways are there to assign 3 students 3 distinct Math 325
projects? 4 students 4 distinct projects? $n$ students $n$ distinct
projects?

\hfill
How many people must attend the first day of lecture in Math 325 to
guarantee 2 people either both have met before or both have not met
before?

\hfill
How many people must attend the first day of lecture in Math 325 to
guarantee 3 people either have all met before or have all not met
before?

These preliminary warmup problems are classic combinatorial questions.
The first, a question of enumeration, we may have a straightforward way
to answer already:

\hfill
Well, we could assign student A project 1. Or, we could assign them
project 2. Or, we could assign them project 3. That's 3 ways. Okay, for
student B, we could assign project 1. Or, we could assign them project
2. Or,$\dots$ This is exhausting listing them out. I'm bored.

What we are going to learn in this class is methods to avoid this one by
one counting. Instead, we will "count". Rather than assigning a specific
student to a specific project one by one, we'll deal with the collection
of students and the collection of projects in their entirety:

\hfill
Given a student, we assign them 1 of the 3 projects. Since we want
distinct assignments, the next student must be assigned one of the other
2 projects. Likewise, the final student must be assigned the leftover
project. Using what we will later refer to as the *multiplication
principle*, we have $3\cdot 2\cdot 1=6$ ways to do this.

Questions 1.2 and 1.3 ask questions of guaranteed substructures that we
will discuss later in the Ramsey Theory section.

# Problem Solving Basics & Set Theory

We will start with questions of *enumeration* and dedicate a fair amount
of time to this concept.

\hfill
The problem of *enumeration* is to count the total number of objects
with a specified property.

\hfill
A few basic examples:

- How many ways are there to assign $n$ students to $m$ projects?
- How many distinct Sudoku puzzles are there?
- How many total (potentially isomorphic) graphs are there are on $n$
   nodes?

This questions can often be difficult to answer given a certain object
with a desired property. However, the philosophical approach we often
take is: **simplify**!  
Our approach to these problems can be summarized in a joke told to me by
a faculty member at WSU:

*A mathematician walks into a room. In one corner, he sees an empty
bucket. In another corner, he sees a sink with a water faucet. In yet
another corner, he sees a fire. Leaping into action, he picks up the
bucket, fills it up at the faucet, and douses the fire.*  
*The next day, the same mathematician returns to the room. Once again,
he sees a fire in the same corner. But, this time the bucket rests next
to the fire full of water. Once more he leaps into action: he picks up
the bucket, dumps the water in the sink, places the bucket empty where
it was from the day before and leaves. As he exits, he exclaims
victoriously \"I've reduced it to a previously solved problem!\"*

Our first goal will be to mimic this proverbial mathematician's
mentality: *simplify*! Once we've simplified, we'll ask ourselves: "can
we generalize this?"\

### Simplification

[\[question1\]]{#question1 label="question1"}

Consider the following problems:

1. How many whole numbers are between 1 and 325 inclusive?
2. How many whole numbers are between 28 and 352 inclusive?
3. How many even numbers are there between 28 and 352 inclusive?
4. How many numbers between 28 and 352 are divisible by 3?

On the one hand, these are four distinct problems. On the other, you may
be able to see there is a process we can use to answer all of them. One
main approach we often utilize in combinatorics is the following: to
count what we need to count, reframe the problem as something we already
know how to count. To quote a great mathematician:

"*I have reduced it to a previously solved problem!*"

Consider our first problem: "How many whole numbers are between 1 and
325 inclusive?"

- 1 is our $1^{st}$, 2 is our $2^{nd}$, and so on, 325 is our
   $325^{th}$. So, there must be 325 such numbers.

This was so easy to solve! What we want to do now is use this solved
problem to answer another. Consider our second problem: "How many whole
numbers are between 28 and 352 inclusive?"

- We begin counting: 28 is our $1^{st}$ number, 29 is our $2^{nd}$,
   and so on, so 352 must be our $?^{th}$.

What do we put here? No idea. We only know how to count numbers between
1 and 325. Let's instead transform this counting problem to the one we
know how to count:

- We may notice 28 is 27 away from 1. Likewise, 29 is 27 away from 2
   and so on.
- So, take each number $28,29,30,\dots, 352$ and subtract 27:
   $1,2,3,\dots, 325$.
- Amazing! We already know this answer: there are 325 such numbers.

One issue you may already have thought of: "how do I know there are the
same amount of numbers between 1 and 325 as 28 and 352 by simply
subtracting 27?" That is a great point. We don't yet know. However, this
is the beauty of a *bijection*. Something we'll talk about: if we have a
bijection between two sets, we know they are the same size. More on the
formalities later!\

\"*I have generalized the method to solve a previously unsolved
problem!*\"

For now, consider the third problem: "How many even numbers are there
between 28 and 352 inclusive?". Again, we don't know how to count this.
But, on the second problem, we transformed to the numbers
$1,2,3,\dots, 325$ and made our problem easier. Let's try something
similar:

- Take each number, $28,30,32,\dots,350, 352$, and divide by $2$:
   $14,15,16,\dots, 175, 176$.
- They may look different, but we can transform similarly to problem
   two. Subtract 13 and we get $1,2,3,\dots, 162, 163$.
- There are 163 such numbers, so there must be 163 such even numbers
   between 28 and 352.

Now that we have a specific method of solution, we might reformat this
method to a more general problem. We may want to count the numbers
between $m$ and $n$ ($m<n$).  
In our second and third problem, we took each number and found a way to
obtain $\{1,2,3,\dots, n\}$ so that we could enumerate the solutions. If
we want to take our $1^{st}$ number $m$ and send it the first natural
number $1$, we might subtract $m-1$ (since $m-(m-1)=m-m+1=1$). For each
of these numbers, we get
$m-(m-1),m+1-(m-1), m+2-(m-1),\dots, n-1-(m-1), n-(m-1)$ which really is
$1,2,3,\dots, n-m, n-m+1$. As such, we obtain a count of $n-m+1$
integers between $m$ and $n$ ($m<n$). What's left to prove is that the
process of subtracting $m-1$ here guarantees the two sets of numbers are
the same size. The next section will discuss how to use a *bijection* to
do so.

## Set Theory Basics

This concept of bijection we subtly utilized previously is actually a
fundamental result combinatorialists love to exploit. Before we get
there, some basics are necessary.

\hfill
A *set* is a collection of distinct objects. E.g. The set of integers
between 28 and 56 = $\{28,29,30,\dots, 56\}$, a set of graphs =
$\{ {\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq1.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq2.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq3.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq4.png}},\dots \}$,
etc.

Note in our definition of a set we require *distinctness*. As such, the
collection $\{1,1,2,3,\dots,29\}$ is not a set. Likewise with any
collection with repeating elements, but this permits another important
definition:

\hfill
A *multiset* is a collection of not necessarily distinct objects. E.g.
The multiset of integers = $\{28,28,28,29,30,\dots, 56\}$, the multiset
of graphs =
$\{ {\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq1.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq1.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq2.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq3.png}},{\includegraphics[height=2ex,valign=m]{math 593/photos/8.23.25/gseq4.png}},\dots \}$,
etc.

However, we won't touch multisets until later on. For now, let us
discuss relations between sets.

\hfill
A function $f:A\to B$ is a relation between sets $A$ and $B$ such that
for each $a\in A$ ($a$ in $A$), there is a unique $b\in B$ such that
$f(a)=b$.

\hfill
As an example, on the left, we have $g:A\to B$ that assigns the second
element in $A$ to two elements in $B$. This means $g$ a function.
However, on the right, we have $f:A\to B$ that assigns each element in
$A$ only one element in $B$. This means $f$ a function.

    

\hfill
Firstly, a function $f$ is *injective* if distinct elements in $A$ are
mapped to distinct elements in $B$. Secondly, $f$ is *surjective* if
every element in $B$ has at least one element in $A$ that gets mapped to
it. Lastly, if $f$ is both injective and surjective, then $f$ is
*bijective*.

For combinatorial purposes, one nice way to think of a function
$f:A\to B$ as the placement of a set of objects $A$ into a set of boxes
$B$:

- If no two objects are placed in the same box, $f$ is injective.
- If no box is left empty, $f$ is surjective.
- If both occur, $f$ is bijective.

We can use this thinking to phrase the following statements:  
Let $f:A\to B$ be a function that assigns a set of objects $A$ to be
placed into a set of boxes $B$.

- $f$ is injective means $f$ ensures no two objects are placed in the
   same box.
- $f$ is surjective means $f$ leaves no box empty.
- $f$ is bijective means $f$ leaves no box empty and ensures no two
   objects are placed in the same box.

But, why do we care about this as combinatorialists?

\hfill
Again, let $f:A\to B$ as defined above.

1. If $f$ is injective, $|A|\leq |B|$.
2. If $f$ is surjective, $|A|\geq |B|$.
3. If $f$ is bijective, $|A|=|B|$

where $|\cdot|$ denotes the number of elements in a set.

First, an outline of a proof.

\hfill
Let $f$ be a function such that $f:A\to B$ for sets $A$ and $B$.\

1. If $f$ is injective, it ensures no two objects are in the same box.
   So, there must be at least enough boxes to house these distinctly
   assigned objects ($|A|\leq |B|$).
2. If $f$ is surjective, it leaves no box empty. So, there must be at
   least enough objects to fill each box ($|A|\geq |B|$).
3. If $f$ is bijective, it ensures no two objects are in the same box
   *and* no box is left empty. As such, we know $|A|\leq |B|$ *and*
   $|A|\geq |B|$ (i.e. that $|A|=|B|$).

This simple statement is incredibly powerful. What this theorem firstly
tells us is that there is a way to infer information about the *sizes*
of the sets when we have a specific property about the *relationship*
between those sets. Most importantly, the theorem also states that if
there exists a bijection between two sets, they must be the exact same
size. We can exploit this fact to enumerate easily! In fact, we already
have.  
Think back to our second problem: "how many integers are there between
28 and 352 inclusive?". Perhaps we write out "28 is $1^{st}$, 29 is
$2^{nd}$,$\dots$" and so on until we reach 352 or count on our 325
fingers one by one. Either way we know this would be annoying and
tedious to count explicitly. By defining a bijective function between
sets, we eased the trouble, $f(a)=a-27$ for
$a\in \{28,29,30,\dots, 325\}$.  
From this final "proof" in
[\[injsurjbij\]](#injsurjbij){reference-type="ref"
reference="injsurjbij"}, we can infer a lot of information. For clarity,
if $f$ is bijective, each object has a distinct box *and* each box has a
distinct object. If we wish to reverse the process of assignment $f$ has
committed, we could easily do so: simply reverse each assignment!  
This thinking leads to the following theorem:

\hfill
The function $f:A\to B$ is a bijection if and only if $f^{-1}$ exists.

This allows us to formalize our results:

- Let $A=\{28,29,\dots, 352\}$, $B=\{1,2,\dots, 325\}$, and $f:A\to B$
   be defined as $f(a)=a-27=b$ for $a\in A$ and $b\in B$.
- Since $f$ subtracts 27, $f^{-1}$ might add 27
   ($f(a)=a-27=b\implies a=f(a)+27\implies f^{-1}(b)=b+27$).
- Thus, $f$ must be a bijection since there exists an $f^{-1}$. So, we
   know $|A|=|B|$.
- Therefore, $|\{1,2,\dots, 325\}|=|\{28,29,\dots, 352\}|=325$.

We can use the same process with problems 3 and 4 of
[\[question1\]](#question1){reference-type="ref" reference="question1"}
:

- Let $A=\{28,30, 32,\dots, 352\}$ and define $f(a)=\frac{1}{2}a-13=b$
   for $a\in A$. What is $f^{-1}$? What is $B$? Conclude $|A|=|B|$.
- Let $A=\{30,33,36,\dots,348,351\}$ and define $f(a)=\frac{1}{3}a=b$
   for $a\in A$. What is $f^{-1}$? What is $B$? Conclude $|A|=|B|$.
- (Extra!) Let $A=\{m,m+1,m+2,\dots, n-1, n\}$ and define
   $f(a)=\frac{1}{k}a-\ell$ for $m<k<n$ and $\ell\geq 0$. What is
   $f^{-1}$? What is $B$? Conclude $|A|=|B|$.

## Summary

What we've done so far is introduce important techniques we often use in
combinatorics:

- Let's simplify our current problem to a problem we already know how
   to solve
- Now that we have found a method to solve a problem, let us
   generalize

These often guide thought in mathematical problem solving and we will
utilize both in combinatorics!

# Introduction to counting techniques

### Warmup

Consider the following problem:

[\[question2\]]{#question2 label="question2"}

Physics 533 and Math 325 occur at the same time (12:10-1PM MWF). Phys
533 has 5 people enrolled while Math 325 has 21.

1. How many people are in Math 325 or Physics 533 from 12:10-1 MWF?
2. How many people are in Math 325 and Physics 533 from 12:10-1 MWF?

This may seem immediately obvious to some, but this highlights key
counting principles used in combinatorics.

\hfill

1. There are 21 people in Math 325. There are 5 in Phys 533. So, there
   are 21+5 in either during the class period.
2. Nobody can be in two places at once, so there must be zero people in
   both classrooms during the class period.

This is a nice set up. We know the set of students in 325 is completely
separate from the set of students in 533. If we use set theoretic
language, the set of students in 325 is *disjoint* from the set of
students in 533. More on this later.  
For now, consider yet another problem:

\hfill
How many ways are there to flip a coin then a six sided dice? More
generally, rolling an $m$ sided dice then an $n$ sided dice?

You might note that my first roll *does not affect* my second roll. They
are independent! Intuitively, if I roll heads, I have the opportunity to
roll 1-6 on the dice. Likewise if roll tails. As such:

\hfill
There are 2 options for my first roll. Since each roll is independent,
there are 6 options for my second roll. So, there must be $2\cdot 6=12$
ways to do this. More generally, since each roll is independent, there
are $m\cdot n$ ways to do this with an $m$ sided dice and an $n$ sided
dice.

## More Set Theory

\hfill
Let $B$ be some set. Another set $A$ is a *subset* of $B$ if every
element of $A$ is an element of $B$ (for every $a\in A$, $a\in B$). We
denote this relationship by $A\subseteq B$ if $A$ could equal $B$
itself. If $A$ cannot equal $B$, we write $A\subset B$.

\hfill
Let $A\subseteq S$. The *complement* of $A$ with respect to $S$,
$A^C=S\setminus A$, is the set of elements in $S$ that are not in $A$
($A^C=\{s\in S|s\notin A\}$). The complement of $S$ with respect to
itself, $S^C=S\setminus S$, is the set with zero elements,
$\emptyset=\{\}$.

We can think of the set complement $S\setminus A$ as considering all the
elements of $S$ that are not in $A$. If there are no such elements (i.e.
$A\nsubseteq S$), $S\setminus A$ is $\emptyset$.\

\hfill
Let $A=\{$integers between 28 and 352 divisible by 3$\}$ and
$S=\{$integers between 28 and 352 inclusive$\}$

- $A\subset S$
- $A^C=S\setminus A=\{$integers between 28 and 352 not divisible by 3}

\hfill
The choice of $S$ is important. If $S=\mathbb{Z}$ (the set of all
integers), then $A^C$ in the previous example would become the set of
*all* integers excluding only integers between 28 and 352 that are
divisible by 3.

\hfill
Let $A\subseteq S$. Is the function $f(A)=A^C$ a bijection? If so, what
is $f^{-1}$?

\hfill
$f$ assigns subset $A$ to its complement $A^C=S\setminus A$.

- Let us say $f(A)=A^C=B$.
- By the definition of a set's complement, $B$ contains every element
   of $S$ that is not in $A$. Likewise, $A$ contains every element of
   $S$ that is not in $B$.
- In other words, $A^C=B$ *and* $A=B^C$.
- So, $f^{-1}(B)=B^C$. Hence, $f^{-1}$ exists and $f$ is a bijection!

\vspace{.5em}
This is a nice property. Consider the problem of enumerating $k$-element
subsets of $S=\{1,2,3,4,\dots, n\}$ ($k<n$).

- Let $A$ be the set of all $k$-elements subsets $A_i\subset S$.
   Moreover, let $B$ be the set of all the complements of elements in
   $A$.
- Then for each $A_i$, there is some set $B_i$ such that
   $f(A_i)=A_i^C=B_i\subset S$ of size $n-k$.
- Since $f(A_i)=A_i^C$ is a bijection, the set of all $k$-element
   subsets, $A$, is the same size as the set of all ($n-k$)-element
   subsets, $B$. That is, $|A|=|B|$.

We will talk about what the actual sizes $|A|$ and $|B|$ later.

\hfill
The *union* of two sets $A$ and $B$, denoted $A\cup B$, is the set of
all elements in $A$ or $B$ ($A\cup B=\{x|x\in A$ or $x\in B$}).

\hfill
The *intersection* of two sets $A$ and $B$, denoted $A\cap B$, is the
set of all elements in $A$ and $B$ ($A\cap B=\{x|x\in A$ and $x\in B$}).

\hfill
If the intersection between sets $A$ and $B$ is empty, denoted
$A\cap B=\emptyset$, we say $A$ and $B$ are *disjoint*.

\hfill
Let $A=\{$the set of students in Math 325$\}$ and $B=\{$the set of
students in Physics 533$\}$.

- $A\cup B=\{$the set of students in either couse$\}$
- $A\cap B=\emptyset$ since now student is in both classes

## Addition & Multiplication Principle

Thinking back to the initial problem of this section
([\[question2\]](#question2){reference-type="ref"
reference="question2"}), we could simply add the number of people in 325
and 533 to get the total number *since no student is in both classes*.
This principle of complete separation allowing simple addition can be
formalized:

\hfill
If $A\cap B=\emptyset$, $|A\cup B|=|A|+|B|$.  
More generally, if $A_i\cap A_j=\emptyset$ for all $i\neq j$ and
$1\leq i,j\leq n$, then
$|A_1\cup A_2\cup \cdots \cup A_n|=|A_1|+|A_2|+\cdots +|A_n|$.

\hfill
Let $A\times B$ be the set of ordered pairs $(a,b)$ where $a\in A$ and
$b\in B$.

\hfill
Let $S=A\times B$. Then, $|S|=|A\times B|=|A|\cdot|B|$.  
More generally, let $S=A_1\times A_2\times \cdots \times A_n$. Then,
$|S|=|A_1\times A_2\times \cdots \times A_n|=|A_1||A_2|\cdots|A_n|$

\hfill
From warmup problem 2, let $A=\{H,T\}$ be the results from flipping a
coin and $B=\{1,2,3,4,5,6\}$ be the results from rolling the six-sided
dice. Then,

$A\times B=\{(H,1),(H,2),(H,3),\dots,(T,5),(T,6)\}$

and $|S|=|A\times B|=|A||B|=2\cdot 6=12$.

### (In)dependence

Note that the *independence* of warmup problem 2 is important. Flipping
a coin *has no impact* on the rolling of the dice. Consider a different
problem:

\hfill
There are four orbs labelled $A,B,C,D$ in an urn. You will draw from the
urn four times. For each draw, you take a single orb out, write down its
label, and replace it in the urn. How many possible label sequences
could you write down?

- Let $A_1, A_2, A_3,$ and $A_4$ be the sets of possible draws on draw
   1, 2, 3, and 4 respectively and $S$ be the set of possible label
   sequences you could write down.
- Since all four balls in the urn before you draw first,
   $A_1=\{A,B,C,D\}$.
- Moreover, since you placed the orb you drew back into the urn, you
   have a chance to draw any of the four orbs again: $A_2=\{A,B,C,D\}$.
- Likewise with $A_3$ and $A_4$.
- Thus, the total possible label sequences there are is:
   $|S|=|A_1\times A_2\times A_3\times A_4|=|A_1||A_2||A_3||A_4|=4^4=256$.

Consider a small change to your process:

\hfill
You really like writing down labels, so you continue with your setup
from the previous problem. However, this time instead of replacing the
orb after drawing it, you set it to the side. You then draw another orb
and set it next to the previously drawn orb. You repeat this process
until there are no orbs left. Then, you write down the sequence of
labels you see. How many possible label sequences could you see?

\hfill

- Let $B_1, B_2, B_3,$ and $B_4$ be the sets of possible draws on draw
   1, 2, 3, and 4 respectively and $T$ be the set of possible label
   sequences you could write down.
- Since all four balls in the urn before you draw first, $|B_1|=4$.
- Whatever you drew, it stays outside of the urn. Since there are 3
   orbs left, you have 3 options for your next draw: $|B_2|=3$.
- Continuing on, you have taken yet another option for your third draw
   away: $|B_3|=2$.
- Lastly, since you drew one of the two remaining orbs, that leaves
   one left for your final draw $|B_4|=1$.
- Thus,
   $|T|=|B_1\times B_2\times B_3\times B_4|=|B_1||B_2||B_3||B_4|=4\cdot 3\cdot 2\cdot 1=24$.

So, replacing the orbs every time gave us a count of 256 while leaving
them out every time gave us a count of 24. What happened? One way to
think of this is that by replacing the orbs, you have allowed for
*repetitions* to exist in your set $S$ (e.g. by drawing $A$ then $A$
then $C$ then $A$). Contrarily, by leaving the orbs out after drawing,
you remove the ability to have repeats. As such, you remove every
element in $S$ that has any repeat labels to obtain a new set $T$, the
set of label sequences with *distinct* labels.

\hfill
Let $S$ and $T$ be defined as in the above problem. What is
$T^C=S\setminus T$? How big is $T^C$ in this case?

\hfill
Let $S$ be defined as in the above problem. How many label sequences
have only 2 repeats? i.e. sequences like $(A,A,B,C)$ or $(D,A,C,D)$.

\hfill
Consider drawing $n$ labelled orbs from an urn with replacement. How
many ways can you do this? Without replacement?

## Summary

What we've covered here:

- A function $f:A\to B$ having an inverse function $f^{-1}:B\to A$
   means $|A|=|B|$.
- Set complements, unions, and intersections.
- Addition principle: the size of a union of disjoint sets is the sum
   of their sizes.
- Multiplication principle: the size of a product of two sets is the
   product of their sizes.
- The difference between counting with dependence versus without.
