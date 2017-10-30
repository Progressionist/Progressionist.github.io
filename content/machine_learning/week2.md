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

#### 2. Gradient Descent for Multiple Features
In last week, we talked about the formula of gradient descent for one feature. Now, let's make the formula a more generalized representation for
multiple features. <br>
**Hypothesis**:
$$h\_\theta (x) = \theta^T x = \theta\_0 x\_0 + \theta\_1 x\_1 + \theta\_2 x\_2 + ... + \theta\_n x\_n$$
where $x\_0 = 1$.

**Parameters**: for convenience, we make parameters $\theta\_0, \theta\_1, \theta\_2 ... \theta\_n$ into just $\theta$.

**Cost Function**:
$$J(\theta) = \frac{1}{2m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)})^2$$

**Gradient Descent**:
$$Repeat: \theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j}J(\theta) \ \  (for \  j = 0,1,2...n)$$

**New Formula**:<br>
Use partial derivative, we can have the new formula:
$$\theta_j := \theta_j - \alpha \frac{1}{m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)}) \ \cdot \ x\_j^{(i)} \ \  (for \  j = 0,1,2...n)$$

Don't forget that each $\theta\_j$ needs to be updated simultaneously.

#### 3. Feature Scaling
"Suppose you have only two parameters and one of the parameters can take a relatively large range of values. 
Then the contour of the cost function can look like very tall and skinny ovals (see blue ovals below). 
Your gradients (the path of gradient is drawn in red) could take a long time and go back and forth to find 
the optimal solution."
![feature_scaling_1](https://user-images.githubusercontent.com/25803108/32150269-e61549e2-bccd-11e7-98a1-e384a58ebba3.png)
"Instead if your scaled your feature, the contour of the cost function might look like circles; then the gradient 
can take a much more straight path and achieve the optimal point much faster."
![feature_scaling_2](https://user-images.githubusercontent.com/25803108/32150270-ea7cc834-bccd-11e7-998a-5f9d033e1374.png)

You may ask, why would a gradient descent run longer in a tall and skinny cost function in the first place? The key reason is that for gradient
descent algorithm, we only have one learning rate $\alpha$. This means if have 2 features, one in large scale and one in small scale,
because of the fixed learning rate, we will always run in small step in that small scale feature. If the path to the minimum is fixed,
this of course will take longer time to get there.







