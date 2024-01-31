Date: 2023-04-28 | 15:24
Status: #note
Tags: [[Support Vector Machine (SVM)]] | #math-ml-book #coursera-ml 
Links: [[Decision Boundary SVM]]

# Basic Large Margin Classifier
The basic idea is to represent the data in a high-dimensional space and partition this space with an hyperplane that **maximizes the margin** between the positive and negative examples. To do that, we seek to solve the following constrained optimization problem.
$$\begin{aligned}
\max _{\boldsymbol{w}, b, r} & \underbrace{r}_{\text {margin }} \\
\text { subject to } & \underbrace{y_n\left(\left\langle\boldsymbol{w}, \boldsymbol{x}_n\right\rangle+b\right) \geqslant r}_{\text {data fitting }}, \underbrace{\|\boldsymbol{w}\|=1}_{\text {normalization }}, \quad r>0
\end{aligned}$$
which clearly state that we want to maximize the margin $r$ while ensuring that the data lies on the correct side of the hyperplane (using $y_i(\textlangle w, x_i \textrangle + b) \ge r$).

> [!caution] 
> We could have problems in practice because the scale of the dataset could affect the margin $r$. Check [[Hard SVM]] for a solution.

The following ilustration shows us a general representation:
![[Pasted image 20230429185606.png | 500]]

>[!note]
> 
The **margin** is the distance from the hyperplane to the closest samples ($x_i$) in the dataset. Note there could be two or more closest samples to a hyperplane

>[!note]
The **hyperplane** is a subspace of dimension $\mathbb{R}^{D-1}$ and is defined as the set of points satisfying $f(x) = \textlangle w,x\textrangle + b = 0$, where $w$ represents a vector that is orthogonal to the hyperplane.