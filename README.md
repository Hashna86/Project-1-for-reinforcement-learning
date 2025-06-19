# Introduction
## Part 1: Stationary k-Armed Bandit
### Problem Description
We consider a 10-armed bandit problem where the true action values (means) for each arm are drawn from a normal distribution 
𝑁
(
0
,
1
)
N(0,1), and the rewards are drawn from 
𝑁
(
𝜇
𝑖
,
1
)
N(μ 
i
​
 ,1). The objective is to evaluate different bandit algorithms in terms of:

Average reward over time.

Percentage of optimal action selection.

We run each algorithm over 2000 time steps for 1000 simulations, each with independent random seeds.

Algorithms Implemented
Greedy: Exploits only, with initial 
𝑄
=
0
Q=0.

Epsilon-Greedy: Explores with probability 
𝜖
ϵ. Tuned via pilot run; best ε = 0.1.

Optimistic Greedy: Greedy with high initial Q-values (99.5th percentile).

Gradient Bandit: Uses preferences and softmax action selection. Best α = 0.2 (chosen via pilot).

Tuning and Evaluation
Epsilon-greedy: Tested several ε values from 0.01 to 0.4; ε = 0.1 yielded consistent high rewards and optimality.

Optimistic Greedy: Initial Q-values set using 99.5th percentile of 
𝑁
(
𝜇
𝑚
𝑎
𝑥
,
1
)
N(μ 
max
​
 ,1).

Gradient Bandit: Pilot tested α values [0.1, 0.2, 0.4, 0.6, 0.8, 1.0]; α = 0.2 found best balance.
