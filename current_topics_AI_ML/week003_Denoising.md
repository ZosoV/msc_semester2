# What is fluorescence microscopy? 

# What kind of noise affects it? How to quantify it?

- In general, more signal (photons per average in capture in a pixel) generate more noise.
- In specific, the approach overcompensates the lack of light by multiplying the result for some scalar (scaling). Then, we should analyze the noise relative to the original signal. In this case, more signal reduce the noise, and fewer signal increase the noise.


## Probability Theory

- The expected value represents different things
    - It is the value you should expect on average if you run your experiment several times.
    - It not necessarily must be a value allowed by your random variable.
    - It is the center of mass of the distribution of X (random variable).
    - IMPORTANT: It is the expected value that minimizes quadratic error. In other words, if in any problem, someone asks you to estimate what is gonna be the output of a random event, you would not be able to do so precisely. But the best you can do is to say your expected value even though this is not allowed by X because the expected value is the value that minimizes the quadratic error.

- **The expected value is that value that minimizes the quadratic error**: This also has an effect in neural networks or when you look to minimize mean square error. In these scenarios, normally with an NN you look to estimate $p(y|x)$, by a mapping x to y, but notice that $p(y|x)$ is actually impossible task because is a probability (not a certaintity). You cannot for certain map some x to y. Then, the best (THE BEST COMPROMISED ESTIMATION THAT YOU CAN COME UP TO SOLVE THIS IMPOSIBLE TASK) you can do is estimate $\hat{y}$ that is an expected value of y. This is the best we can do because it minimizes the square error (MSE) that we use in our lost. For that reason, it makes sense in some context to use MSE, but we actually are estimating the expected value with the NN.

- Notice that the random variable independence explains why it's reasonable to estimate $p(y|x)$ in some models.
    - Independance would mean that $p(y|x) = p(y)$, but it's not true in some classifiers (or regression) models, where the data x actually has something to say about y.

    