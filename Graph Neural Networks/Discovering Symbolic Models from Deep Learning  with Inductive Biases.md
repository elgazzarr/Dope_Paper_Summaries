# [Discovering Symbolic Models from Deep Learning with Inductive Biases](https://proceedings.neurips.cc/paper/2020/file/c9f2f917078bd2db12f23c3b413d9cba-Paper.pdf)


## What is the problem?

Graph Neural Networks are ideal to model physical systems with interacting particles, however, they are black boxes, we do not know what is happening under the hood (e.g what messages are the nodes passing to each other, what transformations are applied to the node etc.). Can we find a way to recover the underlying equations of the physical system from the GNN?


## What is the solution?

The authors propose to do symbolic regression on the internal functions of the GNN (i.e. the MLPs in the GNN; edge MLP (transform edge and connecting node features into a message), node MLP (transform summed messeages from neighbours and the node features into the updated node feature), golbal MLP (aggregates all messeages and updated nodes and coumpute a global property))


## How?

First, They train the GNN in supervised setting while enforcing sparsity on the messages (L1 regulization on the output of the edge MLP)
Then, They use a genetic symbolic regression algorithm to find the algerbraic expressions of the three GNN functions independently.


## Technical Details

- An important insight here is that if we can recover the true dimension of the latent represnetation, we can view the GNN functions as a mathemateical rotation (Matrix multiplication) of the true vectors. 
- You can specify the dimension pre-hand if you already know the true dynamics of the system, or you can use a regulization method to enforce sparsity on the represnetation. Here they try L1 and KL divergence and they find that L1 regulization work better.
- They start with a big dimension and then regularize until the loss degrades, this is when you know you are now losing information in this sparsfication process.
- The messeages are sorted by the largest standard vairation, and they only use the top K messeages for fitting the algebric expressions.



## Results

- They show that the framework can recover Newtonian dynamics equation, Hamiliton equations and evaluate it on an astrophysics problem where the ground truth equations are not know.

- They show that the learned equations can generalize to unseen data

## Opinions and takeaways

- I love what the paper is trying to do here. Using ML not only for prediction but for understanding physics and dynamics (in terms of algebraic equations) that describe its prediction is the ultimate goal of adopting ML for science.

- The emphasis on sparsity seems to be the most important angle of this work.

- The biggest limiation of this work is that in many phsysical systems we do not know the underlying graph structure. The success of this method also hinges on the perfomance of the supervised model. If a model can not predict the label perfectly (or is not learning causal features) I assume that this approach will not work very well. Also the cost of the genetic algortihm even with the sparsity is very high and can be difficult to scale to systems with more nodes and features. 



