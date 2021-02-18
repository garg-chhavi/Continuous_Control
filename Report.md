# Project: Continuous Control

The project demonstrates how policy-based methods - in particular actor and critic, can be used to learn the optimal policy in a model-free Reinforcement Learning setting using a Unity environment.
The objective is to train a double-jointed arm that can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of the agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector is a number between -1 and 1. 
  
## Learning Algorithm

The algorithm uses actor-critic method to train the agent. Policy-based methods like REINFORCE, which use a Monte-Carlo estimate, have the problem of high variance. TD estimates used in value-based methods have low bias and low variance. Actor-critic methods balance the two methods where the actor is a neural network which updates the policy and the critic is another neural network which evaluates the policy being learned which is, in turn, used to train the actor.

In particular the the alogorithm follows the [Deep Deterministic Policy Gradient (DDPG)](https://arxiv.org/abs/1509.02971).

In addition, soft updates are used to update the target network.

The concept of Experience Replay has also been used to uncorrelate the samples while training the network.

### Hyperparameters

Hyperparameters used are

| Hyperparameter                      | Value |
| ----------------------------------- | ----- |
| Replay buffer size                  | 1e6   |
| Batch size                          | 1024  |
| $\gamma$ (discount factor)          | 0.99  |
| $\tau$                              | 1e-3  |
| Actor Learning rate                 | 1e-4  |
| Critic Learning rate                | 3e-4  |
| Leak for LeakyReLU                  | 0.01  |

## Rewards

The best performance was achieved by **DDPG** where the reward of +30 was achieved in 108 episodes (Environment solved in  episodes). This was done using enviroenemt with 20 agents in parallel.
  ![ddpg](Scoret.png)
  
## Ideas for improvement

- Using Prioritized Replay ([paper](https://arxiv.org/abs/1511.05952)) has generally shown to be effective.

- Other algorithms like TRPO, PPO, A3C, A2C that have been discussed in the course could potentially lead to better results as well.