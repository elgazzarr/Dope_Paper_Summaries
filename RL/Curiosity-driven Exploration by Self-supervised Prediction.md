# [Curiosity-driven Exploration by Self-supervised Prediction (ICML 2017)](https://proceedings.mlr.press/v70/pathak17a/pathak17a.pdf)
 
## What is the problem?
Reinforcement learning relies on extrinsic rewards provided by the environment to optimize its behavior.  In many real world settings, this reward signal can be extremely sparse, making learning very inefficient.

## What is the solution?
Learning by intrinsic motivation. Instead of relying solely on rewards provided by the environment, the agent has to have an intrinsic incentive to explore its environment.   

## How?
By rewarding novel states. Usually if an agent is seeing new states, it means that is making progress compared to getting stuck if there is no reward to guide where to go and what to do. 
We can measure if the state is novel by the ability of the model to predict the next state. In its comfort zone, the agent cant easily predict what happens next resulting, in contrary if the agent is in a novel territory. We can encourage this behavior of getting out the comfort zone by using the next state prediction error as a reward. 


## Technical details
There are two main challenges:

1. Predicting the next state in a high dimensional continuous space such as the pixel space of images is very challenging.
2. There are a lot of things happening in the environment that we do not care about, are very stochastic, and even impossible to predict. An agent rewarded when it cannot predict its input can get stuck in these stochastic states. e.g. watching a noisy tv (or browsing social media aimlessly)

**To solve these challenges, the paper propose to learn to predict next states in a _feature space_ that is _only affected by or has an effect on its actions._** Specifically, they design an intrinsic curiosity module trained by self-supervised learning to obtain the intrinsic reward. 

![ICM](utils/images/ICM.png)

1. The inverse model takes the state and next state, extract feature representations, use these that features representations to predict the action that the agent took to make this transition. This makes the feature representations \Phi only contain releveant information for the action.
2. The forward model takes the representations of the current state and the action to predict the representation of the next state, The difference between the predicted next state representation and the ground truth next state representations is used as the intrinsic reward.
The overall objective loss used to train the agent can be divided into three parts.
a) The usual reward maximization (intrinsic and extrinsic if available) via policy gradient methods (here they used A3C)
b) Minimizing action prediction error in the inverse model. 
c) Minimize the next state prediction error in the forward model. 


## Results
- They evaluate on two games Supermario and VizDoom
- They show improved performance (measured as the extrinsic reward per episode) when using ICM in sparse and very sparse reward settings. 
- They also show in absence of any extrinsic rewards, the agent can learn interesting desirable behavior. (navigating the corridors, jumping over enemies )
- They also experiment with agents trained using ICM in unseen environments in three settings (as is, fine-tuned on the new environment with curiosity only, fine-tuned with extrinsic rewards. The results of this highly depend on the correlation between the pretrained environment and the new environment. 


## Opinions & takeaways 
- This is a cool a paper that attempts to implement the idea of curiosity observed in  biological entities into RL agents to incentivize learning in the absence of direct feedback from the environment.
- Again self-supervised learning comes to the rescue to help us embed concepts into artificial neural networks.
- The setup here largely relies on actions (to learn the feature space, and to predict next state). This assumes that there is continuous interaction with environment to learn. What if that is not the case. How can we use intrinsic rewards if 
- On a more general note, this shows you that curiosity is a double edged sword. While it can drive you to explore alternatives to reach your goal if you are stuck,  you can also get stuck into states that seem to you novel, but do not serve any useful purpose other than fulfilling this reward. This is why in general a common theme in addiction is the stochastically of the input. (Internet surfing, watching tv , drugs, etc.).

