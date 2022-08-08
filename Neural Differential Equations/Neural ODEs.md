[# Neural Ordinary Differential Equations (Neurips 2018)](https://arxiv.org/pdf/1806.07366.pdf)



## What is the problem?

Training a neural network can be viewed as finding the solution to an Ordinary Differential Equation (ODE) that describe the transformation of the input with respect to the weights to find the target output.
Standard neural networks such as ResNets can be viewed as Euler discretization solution of a continuous transformation. This discretization requires approximating the number of steps (find optimal number of layers), is memory inefficient (storing intermediate derivatives), and difficult to tradeoff computational complexity versus accuracy dynamically. 


## What is the solution?
Use a more sophisticated ODE solver method than Euler. Here they propose to treat ODE solvers as a black box and compute the gradients using the adjoint sensitivity method trick


## How?

- Back-propagating through the operations of the ODE solver is a bad idea (Very high memory cost, accumulate numerical error)
- So they use something called the adjoint sensitives method (developed in the 60s) to approximate the derivative. This is the main bottleneck that the paper try to solve. **How to back-propagate through the ODE solver to update the function to optimize your desired loss?**


## Technical details

*While reading the paper, think of time as the model weights.*


- To optimize Loss L, we require gradients with respect to weights theta.
- But first to get there, we need to determine how the change in the gradient of the loss depend on the hidden state.
- We define something called the adjoint a, which is the gradient of the loss with respect to the hidden state. It can be computed using automatic differentiation.
- We can integrate the adjoint dynamic (da/dt) back in time using a call to another ODE solver that runs back in time to obtain the dependence of the loss on the initial state. 

I know it is a bit messy to think about without equations!

## Results

- They show that a neural ODE performs competitively on MNIST classification.
- They show that you can tradeoff error tolerance vs complexity (number of function evaluation)
- Number of function evaluation grows as you proceed with training (a more complex function)
- The most impressive utilities is in continuous time series modeling and continuous normalizing flows.


## Opinion and takeaways

- The idea is very powerful, and this paper kickstarted a whole direction into modeling neural networks via continuous functions.
- It seems that most of the results are on simple tasks and learning simple processes. This is also confirmed by a quick research on the applications of Neural ODEs as describe in this paper. It is obvious that we need to develop a model that can learn much richer families of functions. 
- One thing also that is not clear to me is these models seem very prone to overfitting. Are there better regularization methods to build generalizable functions on a wide variety of observations of the same processes?


