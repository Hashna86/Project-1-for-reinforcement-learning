## ASSIGNMENT 1
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
Each arm’s mean changes slowly over time.
#### 2. Mean-Reverting Setting
Each arm’s mean is pulled toward zero.
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


## ASSIGNMENT-2
### Gridworld Assignment Report
### Part 1 – Value Function Estimation and Optimal Policy
In Part 1, we evaluated the state-value function and optimal policies for a 5×5 Gridworld with special squares (BLUE at (0,1), GREEN at (0,4), RED at (3,2), and YELLOW at (4,4)). BLUE teleports to RED (+5 reward), GREEN teleports to RED or YELLOW (50% chance each, +2.5 reward), off-grid moves yield −0.5 reward, and valid moves yield 0 reward. We solved the Bellman equation analytically using matrix inversion and verified results using iterative policy evaluation, ensuring identical results. Optimal policies were derived using the Bellman optimality equation, policy iteration, and value iteration, with all approaches converging to the same state values.
### Part 2 – Monte Carlo Control for Modified Gridworld
In Part 2, the RED state was relocated to (4,2) and terminal states were defined at (2,0), (2,4), and (4,0). Using γ = 0.95, we applied three Monte Carlo methods to estimate the optimal value function and policy:
1) Exploring Starts (On-Policy MC),
2) ε-soft On-Policy MC (ε = 0.1, no exploring starts),
3) Off-Policy MC with Per-Decision Importance Sampling (PDIS). Each method used 10,000 episodes and a maximum of 50 steps per episode for stability.


## ASSIGNMENT-3
### Objective:
The goal of this assignment is to analyze and compare the performance of the SARSA and Q-learning reinforcement learning algorithms in a 5x5 GridWorld environment. The task is to learn optimal navigation policies under risk of penalty and reach terminal states with minimum cumulative negative reward.
### Environment Setup:
- Grid Size: 5x5
- Start State: (4, 0) (bottom-left corner)
- Red Penalty States: [(2, 0), (2, 1), (2, 3), (2, 4)] with reward -20 and reset to start
- Terminal States: [(0, 0), (0, 4)]
- Other Moves: Reward -1
- Invalid Moves: Reward -1
### Algorithms Implemented:
1. SARSA (On-policy TD Control)
2. Q-learning (Off-policy TD Control)

Both algorithms use the ε-greedy policy for exploration, with the following hyperparameters:
- Learning rate (α): 0.1
- Discount factor (γ): 0.95
- Exploration rate (ε): 0.1
- Episodes: 10,000
- Max Steps per episode: 500
### Trajectory Analysis:
#### 1. SARSA Agent Trajectory
•	The agent starts at the green S cell (4, 0) and reaches the terminal state T at (0, 4)` after 8 steps.
•	The trajectory moves upward cautiously, avoiding all red penalty states.
•	After reaching the row with the red wall (row 2), the agent continues up, then moves right to reach the terminal.
•	This reflects a risk-averse behavior, typical of on-policy learning — SARSA learns to act conservatively because it updates based on the actions it actually follows under the ε-greedy policy.

#### 2. Q-learning Agent Trajectory
•	The agent also starts from (4, 0) and reaches a terminal state in 8 steps.
•	However, the agent moves more directly toward the terminal, following a path that cuts through the middle by navigating closer to the red wall and using the safe gap at (2, 2).
•	This demonstrates greedy, optimal behavior, which is expected from Q-learning, an off-policy method. It learns from the best possible future actions, not necessarily the ones taken during exploration.
### Conclusion
The SARSA and Q-learning agents learn different trajectories due to their underlying learning mechanisms. The SARSA agent demonstrates a more cautious path that avoids the red penalty states by moving around them, which is a result of its on-policy nature that learns from actions taken under the ε-greedy strategy. In contrast, the Q-learning agent finds a shorter and more direct path by exploiting the safe gap in the red wall. This behavior reflects its off-policy update mechanism, which prioritizes the highest possible future reward. As a result, Q-learning converges to a more optimal path faster, while SARSA tends to prioritize safer exploration even if the path is longer.

### Reproducibility
All code is available at the GitHub repository linked above.



