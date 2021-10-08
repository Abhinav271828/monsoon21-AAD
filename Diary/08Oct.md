---
title: Algorithm Analysis and Design (CS1.301)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | Daily Diary
          | 08 October, Friday
header-includes: \usepackage{physics}
---

# Nielsen & Chuang
# Introduction and Overview
## Global Perspectives
### History of Quantum Computation and Quantum Information
Quantum mechanics was created when the theories of classical physics failed to make correct predictions of many phenomena. It is a mathematical framework for the construction of physical theories.

## Quantum Bits
Qubits are mathematical objects with certain properties.  

A qubit has a state, for example $\ket{0}$ or $\ket{1}$, or a linear combination
$$\ket{\psi} = \alpha \ket{0} + \beta \ket{1},$$
where $\alpha, \beta$ are complex numbers. Thus the state space is a subset of $\mathbb{C}^2$. $\ket{0}$ and $\ket{1}$ are called the *computational basis states*.  

When we measure a qubit, we get either the result 0 (with probability $|\alpha|^2$) or 1 (with probability $|\beta|^2$). Therefore $|\alpha|^2 + |\beta|^2 = 1$. After the measurement, the qubit collapses into the state that the measurement observed.  

We can also express a qubit as
$$\ket{\psi} = e^{i \gamma} \left(\cos \frac{\theta}{2} \ket{0} + e^{i \phi} \sin \frac{\theta}{2} \ket{1} \right),$$
where $\theta, \phi, \gamma$ are real numbers. The initial $e^{i \gamma}$ factor can be ignored, which then allows us to write
$$\ket{\psi} = \cos \frac{\theta}{2} \ket{0} + e^{i \phi} \sin \frac{\theta}{2} \ket{1}.$$

$\theta$ and $\phi$ determine a point one the unit sphere (the Bloch sphere).

### Multiple Qubits
If we have two qubits, the system has 4 computational basis states $\ket{00}, \ket{01}, \ket{10}, \ket{11}$. Each state can be associated with an *amplitude* to get the general state
$$\ket{\psi} = \alpha_{00} \ket{00} + \alpha_{01} \ket{01} + \alpha_{10} \ket{10} + \alpha_{11} \ket{11},$$
where $\alpha_{00}^2 + \alpha_{01}^2 + \alpha_{10}^2 + \alpha_{11}^2 = 1$.  

If we measure only one qubit (say the first one) and it yields 0, the post-measurement state becomes
$$\ket{\psi'} = \frac{\alpha_{00} \ket{00} + \alpha_{01} \ket{01}}{\sqrt{|\alpha_{00}|^2 + |\alpha_{01}|^2}}.$$

An important state is the *Bell state* or *EPR pair*:
$$\frac{\ket{00} + \ket{11}}{\sqrt{2}}.$$
For this state, the measurements of the two qubits are always correlated.

## Quantum Computation
A quantum computer is built from a quantum circuit, containing wires and quantum gates.

### Single Qubit Gates
The NOT gate converts $\ket{0}$ to $\ket{1}$ and vice versa. Since it acts linearly, we can also conclude that it takes $\alpha \ket{0} + \beta \ket{1}$ to $\alpha \ket{1} + \beta \ket{0}$. It is represented by
$$X = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}.$$

In general, for a matrix to be a valid quantum operator (for the normalisation condition to continue to hold on its output), a matrix $U$ must be unitary, *i.e.*, $U^\dagger U = I$. This is the only constraint on quantum gates.  

Other important unary gates are the $Z$ gate
$$Z = \begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix},$$
which leaves $\ket{0}$ unchanged and flips the sign of $\ket{1}$, and the Hadamard gate
$$H = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix},$$
which has the following behaviour:
$$\begin{split}
H \ket{0} &\to \frac{1}{\sqrt{2}}\left(\ket{0} + \ket{1}\right), \\
H \ket{1} &\to \frac{1}{\sqrt{2}}\left(\ket{0} - \ket{1}\right). \end{split}$$

Single qubit gates correspond to rotations and reflections of the Bloch sphere. The Hadamard gate is a rotation of the sphere around the $y$-axis by $90 ^\circ$, followed by a rotation about the $x$-axis by $180 ^\circ$.  

It is possible to build up an arbitrary single qubit gate using a finite set of quantum gates (called a *universal set*).

### Multiple Qubit Gates
An important 2-qubit gate is the controlled-NOT or CNOT gate, which is represented by
$$U_{CN} = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 \end{bmatrix}.$$
