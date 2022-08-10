[# Exploration by random network distillation (ICLR 2019)](https://arxiv.org/pdf/1810.12894.pdf)



## What is the problem?

Extrinsic rewards provided by the environment can be sparse/non existent to drive learning, and it is difficult to scale hand-engineered rewards.


## What is the solution?

Better exploration policies that are intrinsic to the agent as bonuses to the extrinsic reward provided by the environment.    


## How?

Here the authors propose to use the prediction error between the output of a fixed randomly initialized network and a trained network as a proxy for state count and thus reward the agent when it has high prediction error.



## Technical details

- The fixed random network is distilled into the trained network. This avoids the noisy tv problem because the fixed network is deterministic, thus ideally the trained network will learn the weights of the random network and hence be able to predict the output even if the input is stochastic.

- They propose non-episodic intrinsic rewards and episodic extrinsic rewards. This makes sense, because novel states should be really novel to get a reward. If the extrinsic reward is non-episodic, the agent can learn to exploit this by getting a reward, dying and coming back to this reward.

- To combine non-episodic and episodic rewards they use two value head functions. This can be generally a good practice to combine for example differently discounted rewards. 


## Results

- The most impressive results are on monetzouma revenge game when combining both rewards.
- They train on 2B frames with an RNN to get the best results on montezouma
- The baselines are slightly weak 



## Opinion and takeaways

- This is a neat approach that can be easily integrated to existing RL algorithms, and only requires a single forward pass of neural network on a batch experience. 
- Not sure how it really scale to other games. The paper is really focused on montezouma and it might be the case that RND is only optimal for this setting, where novelty is purely driven from moving enemies or room transition, but not from external factors that do not affect the game.
- While finding policies that scale well with the sample size is necessary, 2B frames to train is really inefficient given the return.


