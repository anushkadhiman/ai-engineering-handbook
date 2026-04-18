# Reinforcement learning (RL)

Reinforcement learning (RL) is a machine learning approach where an autonomous agent learns to make decisions by interacting with an environment, receiving feedback through rewards or penalties, and optimizing a strategy (policy) to maximize cumulative rewards. It learns through trial-and-error without needing labeled data, making it suitable for complex, sequential tasks.

**Key Components**

- Agent: The learner or decision-maker.
- Environment: The context or world with which the agent interacts.
- Action : Steps taken by the agent.
- State : The current situation of the agent.
- Reward : Feedback signal indicating the success of an action.

**How It Works**

Reinforcement learning agents learn from experience, similar to human learning, by assigning rewards to different actions within a Markov Decision Process (MDP) framework. They develop a policy to select actions that maximize long-term rewards, navigating the trade-off between exploring new strategies and exploiting known high-reward actions.

**Major Types of RL Algorithms**

- Value-based: Learns the expected cumulative reward (value) of being in a state and acting, such as Q-learning.
- Policy-based: Directly learns the strategy (policy) that maps states to actions to maximize rewards.
- Actor-critic: Combines both methods, where the actor decides the action and the critic evaluates it.

**Here are some of the RL applications,**

- Robotics: Training robots for tasks like walking or manipulation.
- Autonomous Driving: Decision-making and control in complex traffic scenarios.
- Gaming: Mastering games like Chess, Go, and Atari, often surpassing human capabilities.
- Recommendation Systems: Personalizing content by learning user preferences.

**What are the challenges?**

- It requires massive amounts of data and interaction to learn.
- It is high sensitivity to hyperparameters, leading to training instability.
- Reward Design: Crafting appropriate reward functions is difficult, as poor design can lead to undesired behaviors.

---

## Proximal Policy Optimization (PPO)

Proximal Policy Optimization (PPO) is a state-of-the-art, policy-gradient reinforcement learning algorithm that balances ease of implementation, sample efficiency, and training stability. It limits policy updates using a clipping mechanism, preventing large, destabilizing changes. PPO is the default algorithm at OpenAI, commonly used for robotics and language model alignment (RLHF).

**What are the key componenets?**
- Itolicy Algorithm: PPO directly updates the policy and requires new data for every update cycle.
- Clipping Mechanism: Instead of complex Trust Region Policy Optimization (TRPO), PPO uses a clipped surrogate objective to keep the new policy close to the old one.
- Actor-Critic Architecture: Typically, an Actor (policy network) decides the action, and a Critic (value network) estimates the value of the current state.
- It works efficiently with both discrete and continuous action spaces.


**How PPO Works (The Clipped Objective):**
PPO tries to maximize the following objective, which consists of three parts:

- Policy Loss (Clipped): Limits how much the policy can change, preventing performance collapse.
- Value Loss: Optimizes the critic to better estimate future rewards.
- Entropy Bonus: Encourages exploration by preventing the policy from becoming too deterministic too quickly.

***

*References:*
1. https://huggingface.co/learn/deep-rl-course/unit0/introduction
2. https://web.stanford.edu/class/psych209/Readings/SuttonBartoIPRLBook2ndEd.pdf
3. https://spinningup.openai.com/en/latest/spinningup/rl_intro.html
4. https://icml.cc/2016/tutorials/deep_rl_tutorial.pdf
