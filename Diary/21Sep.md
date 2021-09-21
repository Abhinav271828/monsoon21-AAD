---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | Daily Diary
          | 21 September, Tuesday
---

# CLRS Chapter 9: Medians and Order Statistics
## Selection in Worst-Case Linear Time
Instead of picking the pivot element randomly, we use a deterministic algorithm to select it.  

First, divide the $n$ elements into $\bigg\lceil \frac{n}{5} \bigg\rceil$ groups of 5 elements each. Find the median of each of these groups (in $O(1)$ time) and the median of these medians recursively. Let this pivot be $x$.  

Note that at least half of the groups contribute at least 3 elements greater than $x$ (except the one containing $x$ and the one with less than five elements, if any). Thus the number of elements greater than $x$ is at least
$$3 \left(\Bigg \frac{1}{2} \bigg\lceil \frac{n}{5} \bigg\rceil \Bigg\rceil - 2 \right)$$
which is
$$ \geq \frac{3n}{10} - 6.$$
Similarly, at least $\frac{3n}{10} - 6$ elements are less than $x$. Thus select is called recursively on at most $\frac{7n}{10} + 6$ elements.  

Therefore, for the running time $T$, we have
$$T(n) \leq \begin{cases}
O(1) & n < 140, \\
T\left(\bigg\lceil\frac{n}{5} \bigg\rceil \right) + T \left(\frac{7n}{10} + 6 \right) + O(n) & n \geq 140. \end{cases}$$

To prove that this is satisfied by $T(n) \leq cn$ for some $c$ and for all $n > 0$, we will substitute it in the expression to get
$$\begin{split}
T(n) &\leq c \bigg\lceil \frac{n}{5} \bigg\rceil + c \left(\frac{7n}{10} + 6 \right) + an \\
&\leq \frac{cn}{5} + c + \frac{7cn}{10} + 6c + an \\
&= \frac{9cn}{10} + 7c + an,
&= cn + (-\frac{cn}{10} + 7c + an).$$

This is $ \leq cn$ if
$$- \frac{cn}{10} + 7c + an \leq 0,$$
which is solved by any $c \geq 10a \frac{n}{n-70}$. This is bounded by 2 if $n \geq 140$, which is why we take the base case there.

# Information Theory: A Mathematical Theory of Communication
## Introduction
The semantic aspects of the meaning are irrelevant to the engineering problem.  
What we need to focus on is that the message is selected from a set of possible messages, so the system must be designed to operate for each possible selection.  

If the set is finite, then any function (most naturally, the logarithm) of the cardinality can be regarded as a measure of the information produced when one message is chosen from the set.  
If we use bits, the base of the logarithm will be 2.  

A communication system consists of 5 parts:

* an information source, which produces a message (a sequence of letters, or one or more functions of time and/or other variables).
* a transmitter, which converts the message to a transmittable signal
* a channel, which is the medium
* a receiver, which performs the inverse operation to the transmitter
* a destination.

We classify communication systems into discrete, continuous and mixed.

## Discrete Noiseless Systems
### The Discrete Noiseless Channel
A discrete channel is a system whereby a sequence of choices from a finite set of elementary symbols $S_1, \dots, S_n$ can be transmitted. Each symbol $S_i$ has a duration $t_i$ seconds.  

In the teletype case, all symbols are of the same duration and any of the 32 symbols are allowed. Each symbol then represents 5 bits; if the system transmits $n$ symbols per second, then the channel has a capacity of $5n$ bits per second.  

In the general case, we define the capacity as
$$C = \lim_{t \to \infty} \frac{\log N(t)}{t},$$
where $N(t)$ is the number of allowed signals of duration $t$.  

We note then that $N(t) = N(t-t_1) + \cdots + N(t - t_n)$, which means that $N(t)$ is asymptotically equal to $x_0^t$, where $x_0$ is the largest real solution to
$$x^{-t_1} + x^{-t_2} + \cdots + x^{-t_n} = 1.$$
This gives us $C = \log x_0$.  

The allowed sequences can be restricted by constructing a FSA of the machines, where the arcs have symbols. In all such cases $C$ will exist and can be calculated using Theorem 1 (Appendix 1).  

#### Theorem 1
Let $b_{ij}^(s) be the duration of the $s^\text{th}$ symbol which is allowable in state $i$ and leads to state $j$. Then the capacity $C$ is $\log W$ where $W$ is the largest solution of
$$| \sum_s W^{-b_{ij}^(s)} - \delta_{ij} | = 0,$$
where $\delta_{ij} = 1$ if $i = j$ and 0 otherwise.
