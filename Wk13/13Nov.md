---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | 13 November, Saturday (Lecture 18)
authors: Taught by Prof. Kannan Srinathan
header-includes: |
  \usepackage{physics}
---

# Quantum Algorithms (contd.)
## Shor's Algorithm
Shor's Algorithm is a method to find nontrivial divisors in polynomial time. It consists of four parts:

* reducing the divisors problem to finding a nontrivial square root of 1 modulo $N$ (classically)
* reducing the square root problem to finding order of a number modulo $N$ (classically)
* the order of an integer is simply the period of a particular periodic superposition
* the order-finding problem can be solved efficiently by the quantum Fourier transform or QFT

### Part 1
We wish to find a nontrivial factor of $N$. Let us suppose that $x$ is a nontrivial square root of 1 modulo $N$.  

Then let $x^2 = 1 \mod N$ for some $x \notin \{\pm 1\}$, which means that $(x+1)(x-1) = kN$. This means that $x+1$ and $x-1$ have some factor in common with $N$, and so $\gcd(x+1,N)$ is a nontrivial factor.

### Part 2
Now we choose a random $x$ and assume that $\gcd(x,N) = 1$. If this is not true, we are done.  

If $r$, the order of $x$, is even, then a nontrivial square root of 1 is $x^\frac{r}2$. Half the numbers in $\mathcal{Z}_N$ have even order.

### Part 3
Let us define $f(a) = x^a \mod N$, where $x$ is the number we chose in Part 2. Clearly, $f$ is periodic with period $r$.  
We can also find $U_f$ as the transformation which takes $\ket{x,0}$ to $\ket{x,f(x)}$. Then, we know that
$$\begin{split}
U_f \left(\frac{1}{\sqrt{2^n}}\sum_{x=0}^{2^n-1}\ket{x,0}\right) &= \frac{1}{\sqrt{2^n}}\sum_{x=0}^{2^n-1}U_f \left(\ket{x,0}\right) \\
&= \frac{1}{\sqrt{2^n}}\sum_{x=0}^{2^n-1}\ket{x,f(x)}. \end{split}$$

Then we can compute the superposition
$$\sum_{a=0}^{M-1} \frac1{\sqrt{M}} \ket{a,f(a)},$$
and measure the second register. The system will then collapse to the vectors of only those values of $a$ with the same $f(a)$, *i.e.* the value we measured.  

Now, the values of $a$ will be periodic – if say $s$ is the smallest value, then we will have $s, s+r, s+2r, \dots$. Thus we can find the period.

### Step 4
The Fourier transform of a vector
$$\ket{\alpha} = \sum_{j=0}^{\frac{M}{k}-1} \sqrt{\frac{k}{M}}\ket{jk}$$
is
$$\ket{\beta} = \frac1{\sqrt{k}}\sum_{j=0}^{k-1}\ket{\frac{jM}{k}}.$$
