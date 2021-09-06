---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | Daily Diary
          | 05 August, Sunday
---

# Kruskal's Algorithm
## Properties of Rank
1. $\text{rank}(x) < \text{rank}(\pi(x))$  

2. Any node of rank $k$ has at least $2^k$ nodes in its tree.  
    This can be proved by induction. Clearly, it is true for nodes of rank 0.  

    Consider a tree formed by the union of nodes $a$ and $b$ with ranks $m$ and $n$ (assuming that the theorem holds for $a$ and $b$).  
    Let $m \leq n$ WLOG. Then $b$ becomes the parent of $a$ and its rank increases by 1. Therefore,
    $$\text{the number of nodes dominated by }b \leq 2^n + 2^m$$
    $$ \leq 2^n + 2^n$$
    $$ \leq 2^{n+1}.$$
    Hence the theorem holds after the union, and by induction, for all sets.  

3. If there are $n$ elements overall, there are at most $\frac{n}{2^k} of rank $k$.  
    Suppose there are $p$ elements of rank $k$. They each dominate at least $2^k$ elements; therefore $p \cdot 2^k \leq n$. Hence $p \leq \frac{n}{2^k}$.

## Amortised Running Time with Path Compression
Consider the running time for running `find` on $m$ different vertices. Note that each vertex leads to multiple calls of `find`.  

We have split the integers into intervals according to the $\log * $ function as
$$\{1\}, \{2\}, \{3, 4\}, \{5, 6, \dots, \16\}, \{17, 18, \cdots, \2^{16} = 65536\}, \{65537, 65538, \dots, 2^{65536}\}, \dots$$

Now, there are two types of traversals: one where the parent is in the next interval, and one where it's in the same one.  
The first kind can happen at most $m \log * n$ times for $m$ different vertices, since there are $\log * n$ intervals.  
The second kind can happen at most $2^k$ times for a vertex in $\{k+1, \dots, 2^k\}$. There are at most $\frac{2n}{2^k}$ such vertices, and $\log * n$ intervals. Therefore this is limited to $2n \log * n$, which is independent of $m$ and taken to be constant.  

Thus the total time is $O(m \log * n)$ for $m$ vertices. This makes the running time for the whole algorithm $O(|E| \log * V)$.
