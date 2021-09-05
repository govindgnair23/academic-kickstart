---
title: Solving Tic-Tac-Toe with Reinforcement Learning
author: Govind G Nair
date: '2021-08-14'
slug: solving-tic-tac-toe-with-reinforcement-learning
categories:
  - Article
tags:
  - AI
  - Python
  - Reinforcement Learning
subtitle: ''
summary: ''
authors: []
lastmod: '2021-08-14T10:36:42-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---






## Introduction

In [this](https://www.govindgnair.com/post/solving-tic-tac-toe-with-minimax/) earlier blog post, I covered how to solve Tic-Tac-Toe using the classical Minimax algorithm. Here we will use Reinforcement Learning to solve the same problem.

This should give you an overview of this branch of AI in a familiar setting. As argued in this paper by pioneers in the field, RL could be the key to Artificial General Intelligence. Therefore, it would behoove us to better understand this fascinating field.

## Introduction to Reinforcement Learning

I will refer you to this [post](https://lilianweng.github.io/lil-log/2018/02/19/a-long-peek-into-reinforcement-learning.html) by someone way smarter than me if you want to really spend some time understanding Reinforcement Learning.

I will just skim the surface in this section. Feel free to skip this section entirely.

![](/post/2021-08-14-solving-tic-tac-toe-with-reinforcement-learning.en_files/RL.PNG)

As shown in the figure above, the reinforcement learning framework comprises the following elements

1) **Agent** : Entity learning about the environment and making decisions. We need to specify a learning algorithm for the agent that allows it to learn a policy <br>
2) **Environment**: Everything outside the agent, including other agents <br>
3) **Rewards**: Numerical quantities that represent feedback from the environment that an agent tries to maximize <br>
    - Goal reward representation: 1 for goal, 0 otherwise
    - Action penalty representation: -1 for not goal, 0 once goal is reached
4) **State**: A representation of the environment. At time step $ t $,the agent is in state $ S_t \in \mathcal{S} $ where $ \mathcal{S} $ is the set of all possible states <br>
5) **Action**: At time step $t$, an agent takes an action $ A_t \in \mathcal{A}(S_t) $ where $ \mathcal{A}(S_t) $ is the set of actions available in state $ S_t $ <br>
6) **Policy**: A policy tells the agent what action to take in a given state. $ \pi(a|S) $

A policy can be deterministic i.e. there is one action that is deterministically selected in a given state $ \pi(s)=a $,
or   stochastic i.e. the policy maps a state onto a set of probabilities for taking each action. $ \mathbb{P}[a^i|s] < 1 $  subject to $ \sum_i \mathbb{P}[a^i|s] =1 $

To solve a problem using RL, we should be able to formulate it as a markov decision process (MDP).

### Markov Decision Process

In an MDP, the environment is completely characterized by the **transition dynamics equation**

$$ p(s',r|s,a) $$
That is, the probability of each possible value for $ s' $ (the subsequent state) and $ r $ (reward) depends only on the immediately preceding state and action, $ s $ and $ a $, and, given them, not at all on earlier states and actions. In other words, given the present, the future is independent of the past.

**The state must include information about all aspects of the past agent–environment interaction that make a difference for the future. If it does, then the state is said to have the *Markov property***

If the transition dynamics equation is fully known by the agent, it means an optimal policy can be computed without interacting with the environment. This is **planning**. Some kind of search algorithm can be used here.<br>

When the environment is not fully known, the agent has to learn by interacting with the environment. i.e. **learning**. If an agent constructs a model of the environment , it is called **model based RL**, else it is called **model free RL**.

If you are building a self driving car, learning from real experience can be too expensive so you want to build a model of then environment which you can query for information to make decisions.

When an agent in state $ S_t $ takes an action $ A_t $ as prescribed by a policy $ \pi $, it transitions to a state $ S_{t+1} $ and receives a reward $ R_{t+1} $. The Agent interacting with the **MDP** environment thus gives rise to a sequence or trajectory

$$ S_0,A_0,R_1,S_1,A_1,R_2,S_2,... $$
The goal of an agent is to maximize the long term reward or return.

Long term reward or return is formally defined as the discounted sum of future rewards.

$$ G_t = R_{t+1} + \gamma R_{t+2} + \gamma R_{t+3} +... = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1} $$

$$ = R_{t+1} + \gamma G_{t+1} $$

## Value Functions

To navigate an environment optimally, we need the concept of a value function that comes in two flavors

1) State Value Function <br>
2) Action Value Function

The **State - Value function** of a state $ s $ under a policy $ \pi $,is the expected return from following policy $ \pi $ when starting in state $ s $
$$ v_{\pi}(s) \doteq \mathbb{E}_{\pi}[G_t | S_t =s]  $$

The **Action-Value function** is the value of taking action $a$ in state $s$ under policy $\pi$ and thereafter following the policy $\pi$

$$ q_{\pi}(s,a) \doteq \mathbb{E}_{\pi}[G_t| S_t =s ,A_t=a] $$


## Bellman Equations

The above defintions of the state and action value functions suggest equations to evaluate them known as Bellman Equations.

**The Bellman expectation equation for the state value function** follows naturally from the above definition of the state value function.

$$ v_{\pi}(s) \doteq \mathbb{E}[G_t | S_t =s]  $$ 

$$ = \mathbb{E}_{\pi}[R_{t+1} + \gamma G_{t+1} | S_t =s]  $$ 

$$ = \sum_{a} \pi(a|s) \sum_{s'}\sum_{r} p(s',r|s,a) \Big[ r + \gamma \mathbb{E}_{\pi}[G_{t+1}|S_{t+1} = s']\Big] $$
$$ \sum_{a} \pi(a|s) \sum_{s',r}  p(s',r|s,a) [r + \gamma v_{\pi}(s')] $$



This is easily understood from the backup diagram shown below.


![](/post/2021-08-14-solving-tic-tac-toe-with-reinforcement-learning.en_files/backup.PNG)

The value of a state $ s $ is obtained by considering all possible paths to all possible successor states , and weighting the rewards obtained and value of these successor states by the probabilities of taking each path.

**The Bellman expectation equation for the action value function** is similarly given by

$$ q_{\pi}(s,a) \doteq \mathbb{E}_{\pi}[G_t| S_t =s ,A_t=a] $$
$$ = \mathbb{E}_{\pi}[R_{t+1} + \gamma G_{t+1} | S_t =s',A_t=a']  $$ 

$$ =  \sum_{s',r} p(s',r|s,a)[r + \gamma \sum_{a'} \pi(a'|s')q_{\pi}(s',a')] $$


To make this idea concrete, we can calculate the state value functions for the simplified version of the example we covered in the previous blog post.We will assume that there is only a single player carrying out a series of actions  following a random policy with an equal probability of taking either action - **L** or **R**

We will assume the discount factor $ \gamma = 1 $


![](/post/2021-08-14-solving-tic-tac-toe-with-reinforcement-learning.en_files/RL_my_image2.png)

The value of any given state is derived from the value of the successor states.E.g.
$$V_{\pi}(B) = 0.5V_{\pi}(D) + 0.5 V_{\pi}(E)  = 0.5 \times 4 + 0.5 \times 3 = 3.5$$

Once the value of the successive states are known, the agent can pick the action that leads to the optimal state. 
In this example, the agent wants to move to state B, and takes action "L" to move to that state. A limitation of the state value function is that once you have determined the optimal state, you have to then identify the action that leads to that state.

The action value function does not have this limitation, it directly gives the value of each action at a given state making it easy to pick the optimal actions.

The action-value function at states B, C and A are given by

$$ Q(\mathcal{S}=B,\mathcal{A}=L) = 4 $$
$$ Q(\mathcal{S}=B,\mathcal{A}=R) = 3 $$
$$ Q(\mathcal{S}=C,\mathcal{A}=L) = 2 $$
$$ Q(\mathcal{S}=C,\mathcal{A}=R) = 1 $$
$$ Q(\mathcal{S}=A,\mathcal{A}=L) = 3.5 $$
$$ Q(\mathcal{S}=A,\mathcal{A}=R) = 1.5 $$

## Optimal Policy

**Theorem** <br>
For any MDP <br>
- There exists an optimal policy $\pi_*$, that is better than or equal to all other policies, $ \pi_* \ge \pi, \forall \pi $ 
- All optimal policies achieve the optimal value function $ v_{\pi_*} = v_*(s) $
- All optimal policies achieve optimal action-value function, $ q_{\pi_*}(s,a) = q_*(s,a) $

An optimal policy can be found by maximizing over the optimal value function
$$ \pi_*(s) = \underset{a} \arg\max q_*(s,a) $$

$ q_*(s,a) $ is given by the **Bellman optimality equations**

**The Bellman Optimality equation for state values** is given by

$$  v_*(s) =  \max_{a} \sum_{s',r}  p(s',r|s,a) [r + \gamma v_{\pi}(s')] $$

**The Bellman Optimality equation for action-values** is given by

$$ q_{*}(s,a) = \sum_{s',r} p(s',r|s,a)[r + \gamma\ \underset{a'}max \ \pi(a'|s')q_{\pi}(s',a')] $$

All RL algorithms solve for the Bellman Equations exactly or approximately.  To solve the Tic-Tac-Toe, I will use an algorithm called **Q-Learning**. I will not not go into details of Q-Learning as there are plenty of free online resources that cover this.

## Design

To solve this problem I will create a TicTacToe class that represents the board as a player sees it. Each of the two players retain their own copy of the board. This is possibly an inefficient design, but this is what I will run with.

Given tic-tac-toe is a 2 player game, I essentially simulate two different environments. In the first one, the agent is player X and in the second one the agent is player Y.

After the agent plays, the move by the opposing player is considered a change in the environment resulting from the agent's actions. The new state the agent lands in is a board where the opposing player has already made his/her move.























