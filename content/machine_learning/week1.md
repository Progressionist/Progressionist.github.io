---
title: "week 1"
draft: true
---
### I. Supervised and Unsupervised Learning
#### 1. Supervised Learning: 
data set is given, and right answer is given. In other words, using given data to predict requested result.
And there is **regression problem** and **classification problem**. For example, we can using data set of house size
compare to price to predict a specific house's price based on its size, this is a regression problem. Or, use data
set of breast tumor size compare to if it's malignant or benign to predict a specific size of tumor's condition, and
this is a classification problem. Notice, size of the house, and size of the tumor are **features**, for machine learning
problem, we can have infinite number of features to predict a result.

#### 2. Unsupervised Learning: 
data set is given, but no right answer is provided. Machine is not told what to do. 
**clustering problem** is the most common algorithm. Algorithm will try to find the structure of the data set, for example, divide it into 
different group based on their features.

* Cocktail Party Problem: In a cocktail party, people are talking in different volume, language, all sounds are in a mess.
Using clustering algorithm, we can then try to separate each person's voice independently. 

Note: **Regression**, in math, regression is methods or processes to estimate the relationships among variables. The word itself means
to return to a former or less developed state. When data set consist of many variables, we can use regression to find
how these variables are related to each other, kind of like its less developed structure or state.

### II. Model Representation and Cost Function
#### 1. Model Representation:
**m** = Number of training examples <br>
**x** = Input variable (features) <br>
**y** = Output variable (target variable) <br>
$\textbf{x}^i$: $i$th input variable; $\textbf{y}^i$: $i$th output variable; $(\textbf{x}^i, \textbf{y}^i)$: $i$th training example. <br>
$\textbf{h}$: hypothesis (model), h remaps x to y: $\textbf{x} \rightarrow \textbf{h} \rightarrow \textbf{y}$ 

linear regression with one variable (Univariate Linear Regression) representation: 
$$h_{\theta}(x) = \theta\_{0} + \theta\_{1}x$$
Univariate means one variable, in this case is $x$.

#### 2. Cost Function:
For a linear regression problem, we want to choose the best $\theta \_0$ and $\theta \_1$ value so that the hypothesis (or model)
fits our training set the best. How do we do that? We will first formulate a cost function, then try to minimize it. <br>
For each training example, there is an error between the example real value and our output value from the hypothesis, or:
$$e^i = h_{\theta}(x^{(i)}) - y^{(i)}$$

for each error, we square it (because there're negative errors), and then sums it up to get the net erros' squared of m training examples:
$$\sum_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)})^2$$

Since we sum all of the training set, we need to divide it by $m$ to get an average. In addition, we divide that result by 2 to make the math 
a little bit easier to be calculated. Hence our cost fucntion $J$ (J is a conventional notation) is:
$$J(\theta_0, \theta_1) = \frac{1}{2m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)})^2$$

and our goal is to choose $\theta_0$ and $\theta_1$ in order to minimize the result of this cost function:
$${minimize} \ \  J(\theta_0, \theta_1)$$

Note, this cost function is also called **Squared Error Function** or **Squared Error Cost Function**, there are other types of cost function, but it turns out that 
squared error cost function works reasonably well for regression problem, and that's why wo choose it for linear regression problem.

Now, if we choose a lot of different pair of $(\theta_0, \theta_1)$, and plot it, we will get a 3D graph representation of the cost function like this:
![cost_function](https://user-images.githubusercontent.com/25803108/31395222-d6279a2c-ae12-11e7-946f-9dbe11ad27ce.png)
Notice that there is a lowest point (local minimum) that represents the minimized result of the cost function. And the corresponding pair of $(\theta_0, \theta_1)$
is exactly what we want.

### III. Gradient Descent
#### 1. Algorithm
Gradient Descent is a basic algorithm that minimize a general function $J(\theta_0, \theta_1, \theta_2, ...)$. In this case, we will
use our cost function $J(\theta_0, \theta_1)$ for demonstration. The basic idea of gradient descent is first picking an initial location of the cost function, and then move continously in small steps in the descending direction until we find a 
local minimum (optimum). Notice that if we start off at a slightly different location, we might end up at a different local minimum.

Lets put gradient descent into formular:
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1) \ \  (for \  j = 0, \ j = 1)$$
Let's break it down to several parts for better interpretation:

* "**:=**" is the assignment sign, if $a := b$, that means we assigns b's value to a. Single equal sign **=** calls **truth assertion** sign, if $a = b$, that's claiming a and b have same value. Never write $a = b$, it's wrong
* "$\alpha$" is the learning rate, it determines how large/small each step we will move
* $\frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1)$: the partial derivative inidicates in which direction will move. In this case it will move 
in $\theta_0$ and $\theta_1$ direction.

Notice, when implementation, $\theta_j$ needs to be **simultaneously update** in $\theta_0$ and $\theta_1$ direction.
##### Correct: Simultaneous Update
$temp0 := \theta_0 - \alpha \frac{\partial}{\partial \theta_0}J(\theta_0, \theta_1)$ <br>
$temp1 := \theta_1 - \alpha \frac{\partial}{\partial \theta_1}J(\theta_0, \theta_1)$ <br>
$\theta_0 := temp0 $ <br>
$\theta_1 := temp1 $
##### Incorrect:
$temp0 := \theta_0 - \alpha \frac{\partial}{\partial \theta_0}J(\theta_0, \theta_1)$ <br>
$\theta_0 := temp0 $ <br>
$temp1 := \theta_1 - \alpha \frac{\partial}{\partial \theta_1}J(\theta_0, \theta_1)$ <br>
$\theta_1 := temp1 $ <br>
The latter is incorrect because notice that the partial derivative depends on both $\theta_0$ and $\theta_1$, and $\theta_0$ has already
been updated in second step.

#### 2. Intuition
1. Why it descends? <br>
We starts at $\theta_j$, and minus $\alpha \frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1)$, where $\frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1)$
is the gradient (slope) of the function. Since we want to descend, we need to move into the negative slope direction, that's why we minus it.
2. What does $\alpha$ do? <br>
$\alpha$ is called the learning rate. It decides the magnitude of each step we move. If the $\alpha$ is too small, gradient descent can be very slow.
If the $\alpha$ is too large, then it gradient descent might miss the minumum and then diverge.
3. Why does gradient descend converge? <br>
If we start at the local minimum, then the derivative is zero, we won't go anywhere. Hence, the closer we move towards to local minimum, the curve becomes less steep, and $\frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1)$
becomes closer to zero. Gradient descent takes smaller step, and eventually converges.

#### 3. Linear Regression Application
For squared error cost function:
$$J(\theta_0, \theta_1) = \frac{1}{2m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)})^2$$

We implement gradient descent algorithm:
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j}J(\theta_0, \theta_1) \ \  (for \  j = 0, \ j = 1)$$

We get (repeat until convergence):
$$ \begin{cases} \theta_0 := \theta_0 - \alpha \frac{1}{m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)}) \newline
\theta_1 := \theta_1 - \alpha \frac{1}{m} \sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)}) \ \cdot \ x^{(i)} \end{cases}$$


Good thing about linear regression is that its cost function is always a "bowl shaped" function meaning it doesn't have any local optima except for the global one.
This type of function is also called **convex funtion**. Hence if we apply gradient descent in a linear regression problem, whenever it converges to a minimum, it's always the global one.

* **Batch Gradient Descent**:
The gradient descent algorithm we performed is also called "Batch Gradient Descent" meaning each step of gradient descent we use all of the training examples.
More specifically, every deivative we take over the sum $\sum\_{i=1}^{m} (h\_{\theta}(x^{(i)}) - y^{(i)})$