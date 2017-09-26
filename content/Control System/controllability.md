---
title: "Controllability"
draft: true
---
### 1. What is Controllability?
#### 1.1 Main Concept
Let's say in a linear system:
$$ \begin{cases} \dot{x} & =  & \textbf{A}x + \textbf{B}u \newline
y & = & \textbf{C}x\end{cases}$$

If this system is controllable, then one can choose a control law $u$, 
and put **eigenvalues** of the new system in any places one wants, or 
(same meaning) steer the **states** of the system in any direction one likes. 
For example, if we choose control law $u = -Kx $, then the system becomes:  

$$ \begin{cases} \dot{x} & = & (\textbf{A} - \textbf{B} K )x \newline
y & = & \textbf{C}x\end{cases}$$

and now the old system $\textbf{A}$ matrix becomes $(\textbf{A} - \textbf{B} K )$ in the new system,
if the system is controllable, by tuning control gains $\textbf{K}$, 
we can put eigenvalues of $(\textbf{A} - \textbf{B} K )$ in any places we want (put in left side of the imaginary plane to make it stable); 
or we can steer sates $\textbf{x}$ in any direction that we want.

#### 1.2 Real World Case:
First, a recap of what $\textbf {A, B, C}$ matrix represents in a system:<br>
$\textbf{A}:$ represents the system itself, relationships between all states;<br>
$\textbf{B}:$ represents how the control input affect the system; <br>
$\textbf{C}:$ represents sensors that can give information of the states 
(if this is identity matrix, that means full states feedback which means we can detect every 
state of the system).

In real life, **A** matrix is already built and cannot be changed; most of the cases, 
**B** matrix is also built and cannot be changed. (Think about a car, **A** is how the 
car moves, and **B** is how steering wheel, throttle and brake affect **A**). 
Therefore, we can only choose a control law $u$ to control the system. However, if matrix 
**A** and **B** are not built correctly in the first place, then the system is not 
controllable no matter what $u$ we choose.

#### 1.3 Quick Example:
For a simple system, we can determine if it's controllable just by inspection:
$$\begin{bmatrix} \dot{x_1} \newline \dot{x_2} \end{bmatrix} = \begin{bmatrix} 1&0 \newline 0&2 \end{bmatrix} \begin{bmatrix} x_1 \newline x_2 \end{bmatrix} + \begin{bmatrix}0 \newline 1\end{bmatrix} u$$
By quick inspection, it's not hard to see that this system is not controllable because there's no way that $u$ can affect $x_1$. 
However, if we rebuild $\textbf{B}$ matrix and $u$ to be $\begin{bmatrix}1&0 \newline 0&1\end{bmatrix} \begin{bmatrix}u_1 \newline u_2 \end{bmatrix}$. Then is will be controllable. 
In another example:
$$\begin{bmatrix} \dot{x_1} \newline \dot{x_2} \end{bmatrix} = \begin{bmatrix} 1&1 \newline 0&2 \end{bmatrix} \begin{bmatrix} x_1 \newline x_2 \end{bmatrix} + \begin{bmatrix}0 \newline 1\end{bmatrix} u$$
The system is controllable because $u$ can affect $x_2$, and since $x_1$ is $x_2$ dependent, $u$ can also affect $x_1$.

### 2. Controllability Matrix
#### 2.1 The Controllability Matrix
For more complicated system, inspection is not possible to determine its controllability, yet we can use a controllability matrix to do that. The matrix consists of only $\textbf{A}$ and $\textbf{B}$ matrix:
$$\mathcal{C} = \begin{bmatrix} B & AB & A^2B & \cdots & A^{n-1}B \end{bmatrix} $$ 
for $ x \in \mathbb{R}^n$. <br>
If and only if this controllability matrix $\mathcal{C}$ is full rank: 
$$rank(\mathcal{C}) = n$$
then the system is controllable, otherwise it's uncontrollable.

#### 2.2 Discrete-Time Intuition
One way to intuitively understand the controllability matrix is to use its discrete-time analogy, with an impulse response. 
The impulse response will give the system a "kick" in the $u$ direction. We let that input rings through the system, and then measure what happens in the system. Say the system has a discrete-time representation:
$$x_{k+1} = \tilde{\textbf{A}} x_k + \tilde{\textbf{B}} u_k $$
(notice that $\tilde{\textbf{A}}  \neq \textbf{A}$  and $\tilde{\textbf{B}}  \neq \textbf{B}$).\\
We then "kick" the system with an impulse response. In discrete-time, this is:
$$u_0 = 1,  \ u_1 =0,  \ u_2 = 0, \ u_3 = 0, \ \cdots, \ u_m = 0 $$
correspondingly, the system (states) will look like:
$$x_0 = 0, \ x_1 = \tilde{\textbf{B}}, \ x_2 = \tilde{\textbf{A}} \tilde{\textbf{B}}, \ x_3 = \tilde{\textbf{A}}^2 \tilde{\textbf{B}}, \ \cdots, \ x_m = \tilde{\textbf{A}}^{m-1} \tilde{\textbf{B}}$$
Generally speaking, if input $u$ rings through the system, and touches every state of the system ($\mathcal{C}$ is full rank), then we say the system is controllable. 
Otherwise, there will be some directions in state-space that my input cannot reach.

### 3. Degrees of Controllability
#### 3.1 <font color=red>Gramians</font>

#### 3.2 <font color=red>PBH Test</font>
PBH test is an extremely simple test for controllability with tremendous amount of insight into why and how controllable the system is. 
It states like this: a system a pair of $(\textbf{A}, \textbf{B})$ is controllable if and only if:
$$rank[(\textbf{A} - \lambda \textbf{I}) \ \ \textbf{B}] = n,  \ \forall \ \lambda \in \mathbb{C}$$
If the matrix $(\textbf{A} - \lambda \textbf{I})$ is full rank already, then the system already passed the PBH test and it s controllable. 
So, the right question to ask it that when it is not full rank (rank deficient)? We say a matrix is rank deficient only when its 
determinant is zero: $det(\textbf{A} - \lambda \textbf{I}) = 0$, and this is only true when $\lambda$ are **eigenvalues** of matrix $\textbf{A}$.$\color{red}{*}$ 

Based on the statements above, the PBH test can give us below insights: 

1. When use PBH test, instead to test in all complex plane $\mathbb{C}$, we only need to plug \textbf{eigenvalues} of matrix $\textbf{A}$ into $\lambda$, 
if still $rank[(\textbf{A} - \lambda \textbf{I}) \ \ \textbf{B}] = n$, then the system is controllable. 

2. Since $(\textbf{A} - \lambda \textbf{I})v = 0$, when $\lambda$ is eigenvalues, then the matrix $(\textbf{A} - \lambda \textbf{I})$ is rank deficient 
in the directions of $\textbf{eigenvectors} \ "v"$. Therefore, in order for the system to past the PBH test, matrix $\textbf{B}$ has to compliment, or say 
have some components in the directions of $\textbf{eigenvectors} \ "v"$. 

3. If matrix $\textbf{A}$ has a eigenvalue with multiplicity greater than $1$ (it has repeated eigenvalues). Let's say that the matrix has 2 same eigenvalues, 
then the matrix is rank deficient in 2 eigenvector directions. Therefore, we need to have a $\textbf{B}$ matrix that has 2 independent columns to fill in the null space. 
In other words, we will need to have 2 control knobs to make this system pass the PBH test. $\color{red}{*}$ 

#### 3.3 <font color=red>Cayley-Hamilton Theory</font>
Cayley-Hamilton Theory is extremely important, and it states like this: 

"Every square matrix A satisfies its only characteristic (eigenvalue) equation."