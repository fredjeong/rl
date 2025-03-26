# Tracking a Nonstationary Problem

Suppose that the probability distributions for our rewards change over time. In such nonstationary cases, it makes sense to give more weight to recent rewards than to long-past rewards. 

One of the ways of doing this is to use a constant step-size parameter, rather than using $1/n$ as from the previous section. We can modify the incremental update rule as

$$
Q_{n+1} = Q_n + \alpha (R_n - Q_n)
$$

where $a\in(0, 1]$ is a constant step-size hyperparameter. This results in $Q_{n+1}$ being a _weighted average_ of past rewards and the initial estimate $Q_1$:

$$
\begin{align*}
Q_{n+1}
&= Q_n + \alpha(R_n - Q_n)
\\
&= \alpha R_n + (1 - \alpha)Q_n
\\
&= \alpha R_n + (1 - \alpha)\left(\alpha R_{n-1} + (1-\alpha)Q_{n-1}\right)
\\
&= \alpha R_n + (1 - \alpha) \alpha R_{n-1} + (1-\alpha)^2 Q_{n-1}
\\
&= \alpha R_n + (1-\alpha)\alpha R_{n-1} + (1-\alpha)^2\alpha R_{n-2}
\\
&~~~~~+ (1-\alpha)^{n-1}\alpha R_1 + (1-\alpha)^n Q_1
\\
&= (1-\alpha)^n Q_1 + \sum_{i=1}^n \alpha (1-\alpha)^{n-i}R_i.
\end{align*}
$$

The weight, $\alpha(1-\alpha)^{n-i}$ given to the reward $R_i$ depends on how many rewards ago it was observed. It decays exponentially according to the exponent on $1-\alpha$.

Stochastic approximation theory requires the following conditions to assure convergence with probability 1:

$$
\begin{gather*}
\sum_{n=1}^\infty \alpha_n(a) = \infty
\\
\sum_{n=1}^\infty \alpha_n^2(a) < \infty.
\end{gather*}
$$

However, for a constant step size $\alpha_n(a)=\alpha$,the second condition is not met, indicating that the estimates never completely converge but continue to vary in response to the most recently received rewards. This is rather a desirable outcome in a nonstationary environment where the reward distribution consistently changes over time. Step-size parameters that meet the conditions above often converge very slowly and are rarely used in empirical work.

