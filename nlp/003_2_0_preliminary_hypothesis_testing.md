# Preliminary: Hypothesis Testing

- **Intuition**: In hypothesis testing, we have two contexts what is happening in reality and what is happening in our testing.
    - **What is happening in reality**? Suppose somehow we know that the probability of applying a vaccine is 99% accurate
        1. P(accurate) = 99%
        2. These clearly leads us to understand that if we apply the test 100 times we will get the following probabilities
            - P(accurate 100/100) = 36.6%
            - P(accurate 99/100) = 37.0%
            - P(accurate 98/100) = 18.5%
            - P(accurate 97/100) = 6.0%
            - P(accurate 96/100) = 1.5%
            - P(accurate 95/100) = 0.3%
        3. Based on this info check your test
    - **What is happening in testing**? In the testing, we want to create a vaccine with 99%, we don't know the probability, but we will want to reach that probability. How do we proceed?
        1. Developed an hypothesis: P(new test accurate) = 99% (we assume this)
        2. Apply the test 100 times
        3. If after applying 100 times, we get 95/100. We can clearly notice that if everything was true (our vaccine 99%) the probability of observing the outcome 95/100 after 100 times applications would be really low.
            - It's still possible, but less likely (that result surprised us). At that point, we can reject our hypothesis with a certain threshold (if the probability observed is less than certain threshold).
            - In other words, we will say we reject the hypothesis if the probability is less than 5% (for example). And we should have to redo the vaccine.
- When you try to set a null hypothesis and alternative hypothesis take in mind this intuition.
    - **Null Hypothesis**: It's almost always when everything works as EXPECTED, "NO DIFFERENCE".
    - **Alternative Hypothesis**: It's a difference, a behavior out of the normal.
- The **significance level** ($\alpha$) is the threshold used to make a decision: reject the null hypothesis or not.
    - It can take values of 0.01, 0.05, or 0.1
    - Changing $\alpha$ impacts the probabilities of Type I and Type II errors.
        - A Type I error is when we reject a true null hypothesis.
        - A Type II error is when we fail to reject a false null hypothesis.
        - Lower values of $\alpha$ reduce Type I, but increase Type II
        - Higher values of $\alpha$ increase Type I, but reduce Type II 

- A p-value is defined as p-value = $P( \text{observed} | H_0 \text{ true})$
    - We use p-values to make conclusions in significance testing. More specifically, we compare the p-value to a significance level to make conclusions about our hypotheses.


- Process:
    1. Set the null and alternative hypothesis 
    2. Set (ahead of time) the significance level $\alpha = 0.05$ (with 95% of confidence)
    3. Take a sample $n=100$ and calculate a desired statistic (or metric). This is our observed behavior.
    4. Calculate the p-value = $P( \text{observed} | H_0 \text{ true})$
    5. Check:
        - If p-value < $\alpha \rightarrow$ Reject $H_0$
        - If p-value < $\alpha \rightarrow$ don't reject $H_0$ (but don't accept $H_0$ we don't have enough evidence).

    - **NOTE:** The conclusion if we reject the hypothesis is that with 95% level of confidence (given by the significance level), we conclude the alternative hypothesis. We have enough evidence to do that.
    - **NOTE:** If after reading this you don't remember. Check this [video](https://www.khanacademy.org/math/statistics-probability/significance-tests-one-sample/idea-of-significance-tests/v/p-values-and-significance-tests)