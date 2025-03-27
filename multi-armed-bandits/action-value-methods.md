# Action-value Methods

Recall that the true value of an action, $q_*(a)$, is the expected reward when the action is selected:

$$
q_*(a) = \mathbb E\left[ R_t\mid A_t=a \right].
$$

One way to estimate this is the _sample-average_ method. We average the rewards actually received from the past experience:

$$
\begin{align*}
Q_t(a) 
&= \frac{\text{sum of rewards when } a \text{ taken prior to }t}{\text{number of times } a \text{ taken prior to }t}
\\
&= \frac{\sum_{i=1}^{t-1} R_i\cdot \mathbb{1}_{A_i=a}}{\sum_{i=1}^{t-1}\mathbb{1}_{A_i=a}}
\end{align*}
$$

where $\mathbb{1}_{\rm{predicate}}$ is an indicator function. If the denominator is zero, that is, if the action has not been chosen before, then we instead define $Q_t(a)$ as some default value, such as 0. By the law of large numbers, we have $Q_t(a)\to q_*(a)$ as the denominator goes to infinity.

The simplest action selection rule is, as mentioned in the previous section, the greedy algorithm. We select the action with the highest estimated value. That is,

$$
A_t= \arg\max_a Q_t(a).
$$

If there is more than one greedy action, then we randomly select one among them.  Note that it always exploits current knowledge to maximise immediate reward. 

An alternative is to behave greedily most of the time, but select randomly from among all the actions with some probability $\epsilon$. This is called $\epsilon$-greedy method. In the limit as the number of steps increases, every action will be sampled an infinite number of times, thus ensuring that all the $Q_t(a)$ converge to $q_*(a)$.