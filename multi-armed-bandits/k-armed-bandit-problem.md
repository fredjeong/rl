# A $k$-armed Bandit Problem

Suppose you are faced with a choice among $k$ different _actions_. That is, in the slot machine analogy from the previous chapter, you get to choose which oen of the $k$ slot machines to play. 

After each action you receive a numerical _reward_, which follows a stationary proability distribution that depends on the action you selected. Your goal is to choose the set of actions that maximises the expected total reward over some time period, $T$ timesteps.

### Value

Here, each of the $k$ actions has an expected or mean reward given that that action is selected, so called _value_. Denoting the action selected on time step $t$ as $A_t$, the corresponding reward is denoted as $R_t$. The value of an arbitary action $a$, $q_*(a)$ is defined as:

$$
q_*(a) = \mathbb E\left[ R_t\mid A_t=a \right].
$$

We assume that we do not accurately know this value, as it is trivial to solve a $k$-armed bandit problem if we do. Instead, we estimate the value $q_*(a)$ by $Q_t(a)$, and aim to make it as close as possible to $q_*(a)$.

### Exploitation vs Exploration

At any time step $t$, there is at least one action whose estimated value is the greatest. A strategy that always chooses this action is called a _greedy_ algorithm. If you select actions that have the highest estimated expected rerturn, we say that you are _exploiting_ your current knowledge of the values of the actions. 

On the other hand, you can make some other decisions, choosing one of the non-greedy actions. In this case we say that you are _exploring_. Exploration enables you to improve your estimate of the non-greedy action's value. 

In the short run, exploitation is the right thing to do to maximise the expected reward of the current time step, but in the long run, exploration may lead you to the greater total reward. Therefore, if you have many time steps ahead on which to make action selections, it is reasonable that you explore the non-greedy actions and discover which one of them are better than the greedy action.

This way, in the long run, the reward is higher, because you can exploit the better actions many times after you have discovered them. You cannot exploit and explore at the same time; there is a trade-off. So it is import to balance betweeen exploitation and exploration.