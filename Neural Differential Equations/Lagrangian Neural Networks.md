# [Lagrangian Neural Netowkrs (Neurips 2020)](https://arxiv.org/pdf/2003.04630.pdf)


## What is the problem?

Neural Networks are increasingly being used in physical scineces but donot have physics prioris. One popular method to incrorpate convervation laws as a priori is Hamiltonian neural networks. However, they require canonical coordiantes, which can be unknown or difficult to compute in many settings. 

## What is the solution?

Learn the Lagrangian of the system instead of the Hamiltonian.


## How?
A system that travels between two points can be descirbed as the action (i.e., the time integral across the difference between kinetic and potential energy). This difference can be defined as the lagrangian of the system.
There is only one path the system can take to become stationary (change in action is zero). We can use this to derive a constraint equation called the Euler Lagrange equation. We can model the dynamics of the system by solving this second order differential equation and integrating over time.



## Technical details


- We can define the loss as the error between the second order dervivative obtained by the NN and the second order ground turth derivative (obtained either analytically or by finite difference method)

- The forward  model of the lagrnaging (involving Hessian inverse of a neural network) is quite challenging, but I think it is much easier with JAX

- The neural network  here takes the input coordiantes and  output the Lagrnaigan and from it we calculate the second order derviative.

## Results

- They show results on double pendulum and a reletivistic particle in a unifrom potential. While the system shows the same loss as the baseline, the Lagrangian NN shows energy conservation. 
- They also show that Hamilitonian fail to learn the dynamics in a system with no canonical coordinates while the Lagrangian does.


## Opinions and takeaways

- Hmm, I am not sure I fully grasped this one. There are a lot of details missing in the paper or assuming deep prior knowledge in the topic.

- How does this system fair in high dimensional settings?

-  