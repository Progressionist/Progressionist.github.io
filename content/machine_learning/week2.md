---
title: "week 2"
draft: true
---
### I. Multivariate Linear Regression
#### 1. Multiple Features
In this section, we will have data set with multiple features. <br>
New notation: <br>
$n$ = number of features. <br>
$x^{(i)}$ = features of $i^{th}$ training sample. (it's a vector)<br>
$x\_j^{(i)}$ =  $j^{th}$ feature in $i^{th}$ training sample. <br>
Now our new hypothesis for multiple features becomes:
$$h\_\theta(x) = \theta\_0 + \theta\_1 x\_1 + \theta\_2 x\_2 + ... + \theta\_n x\_n$$
Notice that for convenience of notation, we define $x\_0 = 1$. 

Put them into vectors we now have:
$$x = \begin{bmatrix} x\_0 \newline x\_1 \newline x\_2 \newline \vdots \newline x\_n \end{bmatrix} \in \mathbb{R}^{n+1}, \ \ \
\theta = \begin{bmatrix} \theta\_0 \newline \theta\_1 \newline \theta\_2 \newline \vdots \newline \theta\_n \end{bmatrix} \in \mathbb{R}^{n+1}$$
and
$$h\_\theta (x) = \theta^{\ T} x$$