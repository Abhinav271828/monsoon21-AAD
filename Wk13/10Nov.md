---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | 10 November, Wednesday (Lecture 17)
authors: Taught by Prof. Kannan Srinathan
header-includes: |
  \usepackage{physics}
---

# Quantum Algorithms
## The Photon Experiment
Consider the following experiment: place two polarisers in the path of a beam of photons such that no light passes beyond the second. Now, it is possible to place a third polariser in between these two such that some light ends up passing beyond all three – this is not explainable by classical physics.  

## Qubits
Thus, we describe photons in terms of a new concept – quantum bits or qubits. Qubits are unit vectors in a 2D complex vector space, with the basis conventionally taken as $\{\ket0, \ket1 \}$. Thus a qubit has the form $a\ket0 + b\ket1$, with the additional constraint that $|a|^2 + |b|^2 = 1$.  

The values $a$ and $b$ are interpreted as follows: the probability that, when measured, the qubit $a\ket0 + b\ket1$ returns $\ket0$ is $|a|^2$, and similarly for $\ket1$ and $|b|^2$.  

Now, we can explain our observation. The first two filters must be placed orthogonal to each other; thus all photons passing through the first one would collapse to $\ket0$ (say), and none could then pass through the next one.  

However, suppose the filter in the middle is placed halfway between each of these two (at a 45º angle). Then half the photons passing through the first filter could still pass through the second, and similarly for the third.

## Quantum Postulates
The following are some fundamental quantum postulates:

* the superposition postulate – quantum systems exist as a superposition of possible configurations, which are represented as state vectors in Hilbert space.
* the measurement and collapse postulate
* the evolution postulate – transformations are unitary matrices and systems evolve according to the Schrödinger equation.

As an example of using transformations, we can see the no-cloning theorem, which states that there is no quantum transformation $U$ such that $U \ket{a0} = \ket{aa}$ for all quantum states $\ket{a}$.  

This can be proved by considering a state $\ket{c} = \frac{1}{\sqrt2}(\ket{a} + \ket{b})$. Then,
$$\begin{split}
U\ket{c0} &= \frac{1}{\sqrt2}(U\ket{a0} + U\ket{b0}) \\
&= \frac1{\sqrt2}(\ket{aa} + \ket{bb}) \end{split}$$

But,
$$\begin{split}
U(\ket{c0}) &= \ket{cc} \\
&= \frac12(\ket{aa} + \ket{ab} + \ket{ba} + \ket{bb}), \end{split}$$
which is a contradiction.

## Multiple Qubits
Individual state spaces of $n$ classical particles combine with the cartesian product, but quantum states combine through the tensor product.  

For example, the basis for a three-qubit system is $\{\ket{000}, \ket{001}, \ket{010}, \ket{011}, \ket{100}, \ket{101}, \ket{110}, \ket{111}\}$, and in general an $n$-qubit system will have $2^n$ basis vectors.  

Thus, nature carries out an extremely complex computation in real time, which we can exploit.

## Quantum Entanglement
The state $\ket{00} + \ket{11}$ cannot be described in terms of its components separately, *i.e.*, we cannot find $a_1, a_2, b_1, b_2$ such that
$$(a_1 \ket0 + b_1 \ket1) \otimes (a_2 \ket0 + b_2 \ket1) = \ket{00} + \ket{11}.$$

This means that quantum states can show instantaneous effect at a distance – if the state $\ket{00} + \ket{11}$ is divided and the two bits taken to remote locations, the measurement of either one will lead the immediate collapse of the other.

## Quantum Gates and Circuits
Quantum gates are simply unitary transformations (matrices) applied on state vectors.  

Quantum circuits are built on such gates.

## Quantum Teleportation
The objective of quantum teleportation is to transmit the quantum state of a particle using classical bits and reconstruct the exact quantum state at the receiver. Note that it does not contradict the no-cloning theorem as the original state is destroyed in the process.  

Suppose Alice as a qubit $\phi = a\ket0 + b\ket1$ whose state she doesn't know. It must be teleported to Bob classically.  
We will assume that Alice and Bob each possess one qubit of an entagled pair
$$\psi_0 = \frac1{\sqrt2}(\ket{00} + \ket{11}).$$

Thus, the initial state is
$$\begin{split}
\phi \otimes \psi_0 &= \frac1{\sqrt2}(a\ket0 \otimes (\ket{00} + \ket{11}) + b\ket1 \otimes (\ket{00} + \ket{11})) \\
&= \frac1{\sqrt2}(a\ket{000} + a\ket{011} + b\ket{100} + b\ket{111}). \end{split}$$

Now, Alice applies $C_\neg \otimes I$ and $H \otimes I \otimes I$. Therefore, the state is now
$$\begin{split}
(H \otimes I \otimes I)(C_\neg \otimes I)(\phi \otimes \psi_0)
&= (H \otimes I \otimes I)(C_\neg \otimes I)\frac1{\sqrt2}(a\ket{000} + a\ket{011} + b\ket{100} + b\ket{111}) \\
&= (H \otimes I \otimes I)\frac1{\sqrt2}(a\ket{000} + a\ket{011} + b\ket{110} + b\ket{101}) \\
&= \frac12(a(\ket{000} + \ket{011} + \ket{100} + \ket{111}) + b(\ket{010} + \ket{001} - \ket{110} - \ket{101})) \\
&= \frac12(\ket{00}(a\ket0 + b\ket1) + \ket{01}(a\ket1 + b\ket0) + \ket{10}(a\ket0 - b\ket1) + \ket{11}(a\ket1 - b\ket0)). \end{split}$$

Alice measures the first two qubits of her state and sends the result to Bob. According to Alice's results, Bob can find the transformation to apply to his qubit as

| bits received | state | decoding |
| :---: | :---: | :---: |
| 00 | $a\ket0 + b\ket1$ | I |
| 01 | $a\ket1 + b\ket0$ | X |
| 10 | $a\ket0 - b\ket1$ | Z |
| 11 | $a\ket1 + b\ket0$ | Y |
