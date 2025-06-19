
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

### Algorithms Implemented
Greedy: Exploits only, with initial Q=0.

Epsilon-Greedy: Explores with probability ϵ. Tuned via pilot run; best ε = 0.1.

Optimistic Greedy: Greedy with high initial Q-values (99.5th percentile).

Gradient Bandit: Uses preferences and softmax action selection. Best α = 0.2 (chosen via pilot).

### Tuning and Evaluation
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
### Conclusion - Part 1
The epsilon-greedy and gradient bandit methods outperform others due to their balance between exploration and exploitation. The greedy method suffers due to lack of exploration. Optimistic greedy performs moderately well early on but is outperformed in the long run.
## Part 2: Non-Stationary Bandit
We modify the environment so that the true means 
𝜇
𝑖
μ 
i
​
  are no longer stationary.

### 2.1 Gradual Changes
#### 1. Drift Setting
Each arm’s mean changes slowly over time:
#### 2. Mean-Reverting Setting
Each arm’s mean is pulled toward zero:
#### Pilot Runs
Conducted pilot runs with different parameters (ε and α) to find best values for:

Epsilon-Greedy: ε = 0.1

Gradient Bandit: α = 0.2

Findings
Gradient Bandit showed better adaptability to non-stationarity. Epsilon-greedy also performed well due to continued exploration.

### 2.2 Abrupt Changes
#### Setup
At time step t = 501, the true action values (means) are randomly permuted. Two scenarios are tested:

1. No Reset: Algorithms continue without any knowledge of the changepoint.

2. Hard Reset: Algorithms reset internal state (Q-values, preferences) at 
𝑡
=
501
t=501.
## Observations
Resetting significantly helps action-value-based methods.

Gradient Bandit adapts well even without reset due to continual preference update.

## Final Comments
Epsilon-Greedy and Gradient Bandit are most robust in both stationary and non-stationary settings.

Optimistic Greedy is useful early but lacks adaptability.

Reset awareness improves performance drastically after abrupt changes.

Proper parameter tuning via pilot experiments is essential for maximizing performance.

## Reproducibility
All code is available at the GitHub repository linked above.
