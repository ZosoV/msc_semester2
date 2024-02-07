# Week 3_2:

## Evaluation Metrics Precision, Recall,  F-measure

- Classifiers are evaluated based on accuracy, **precision**, **recall**, and **F-measure**
    - These metrics are calculated from a confusion matrix
- Notice that you can understand
    - **precision**: as a notion of accuracy from the perspective of the model.
        - key to remember: horizontal, denominator include false positive
        $$\text{Precision} = \frac{TP}{TP + FP}
$$
    - **recall**: as a notion of accuracy from the perspective of the data.
        - key to remember: vertical, denominator include false negative
            $$\text{Recall} = \frac{TP}{TP + FN}$$
- The **F-measure** is a harmonic mean, which is the reciprocal of the arithmetic mean of reciprocals.
$$\text{F1-score} = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$
- It's also possible to calculate a macro and micro variants of these metrics, when there are **more than 2 classes** involved in the confusion matrix.
    - **macro** = simple average
    - **micro** = create a pooled confusion matrix (summing all together the small versions of each class). Then, calculate the metrics on the poopled confusion matrix.
- Classifiers are trained using distinct training, dev, and test sets, including the use of **cross-validation** in the training set, such as **K-fold cross-validation**.

## Hypothesis Testing

Statistical significance tests can be used to compare the performance of a metric $M$ on two different models $A$ and $B$.
- The idea is to provide **statistically significant** evidence that some model A is better than model B wrt to a performance metric. In other words, that the results weren't only obtained by accident.
- NOTE: If I get lost in this explanation review the [Hypothesis Testing Preliminary](003_2_0_preliminary_hypothesis_testing.md)

To perform this hypothesis testing, we can define a performance difference, also called effect size, 
$$\delta(x) = M(A,x) - M(B,x)$$

Based on that, we can define a null and alternative hypothesis as follows

- Null hypothesis $H_0: \delta(x) \leq 0 \quad$(Model A is **not** better than B)
- Alternative $H_1: \delta(x) > 0 \quad$. (Model A is better than B)

And consequently, a p-value

$$\text{p-value} = P(\delta(X) \leq \delta(x) | H_0 \text{ is true})$$

If $\text{p-value} < \alpha$, we can reject the null hypothesis $H_0$ and accept $H_1$.

Things to consider:

- $\delta(X)$ represents the calculation of performance difference over different test data sets. Then, in order to perform this hypothesis test we need several test sets.
- In practice, we don't apply parametric tests like t-test or ANOVA. Instead non-parametric tests **based on sampling** are used to **artificially** create many versions of the experimental setup. the most comer are:
    - approximate randomization
    - bootrap test

## Paired Boostrap Test
The boostrap method is a method to create artificial test data sets from an observed test set in order to perform an non-parametric hypothesis testing.

- It consists in creating artificial test data sets by sampling randomly with replacement from a base (or reference) test data set. Under the assumption that the base sample is a representative of the population.

- It's appropriate for comparing two classifiers because bootstrap normaly work with paired tests, which compare two sets of observations that somehow are aligned. When we analyze two classifier models A and B, the performance of A and B is paired by comparing them.

The process is as follows:

1. Measure the performance of metric $M$ in a base test set (size N) for the model A and B, and display the results.
2. Create artificial test results by randomly sampling with replacement from the results (of size N).
    - It is practically picked randomly with replacement one of those N results.
3. Repeat the process until complete a set of results of size N.
4. Repeat the process b times until generate b artificial test results.
5. Once we have b artificial test sets, we can calculate our p-value as follows

$$\text{p-value}(x) = \frac{1}{b}\sum_{i=1}^{b}\left(\delta(x^{(i)}) - \delta(x) \geq \delta(x) \right)$$

$$\text{p-value}(x) = \frac{1}{b}\sum_{i=1}^{b}\left(\delta(x^{(i)}) \geq 2\delta(x) \right)$$

where $x$ is the base test set and $x^{(i)}$ are the artificial test sample from $x$, and

$$\delta(x) = M(A,x) - M(B,x)$$

is the performance difference from A and B of metric $M$

6. If $\text{p-value} < \alpha$, we can reject the null hypothesis $H_0: \delta(x) \leq 0$ and accept $H_1: \delta(x) > 0$. In other words, accept that A is better than B wrt the performance on $M$.


- Designers of classifiers should carefully consider harms that may be caused by the model, including its training data and other components, and report model characteristics in a **model card**