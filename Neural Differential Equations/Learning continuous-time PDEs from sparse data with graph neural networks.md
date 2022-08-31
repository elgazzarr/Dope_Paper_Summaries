# [LEARNING CONTINUOUS-TIME PDES FROM SPARSE DATA WITH GRAPH NEURAL NETWORKS(ICLR 2021)](https://arxiv.org/pdf/2006.08956.pdf)


## What is the problem?

Several dynamical systems follow complex unkown pdes. While multiple methods propose to learn the pdes directly from data, they assume that observations arrive at regular grids (temporally and spatially) and they use dicrete time approximations to find the pde.

## What is the solution?

They propose a general *continous-time* framework for modelling dynamical systems whose governing equations are parametrized by message passing graph neural networks.

## How?

- for a system u(x,t), assume that there is an unkown PDE F(x,u, du/dx, d^2u/dx,.. ) which govern the temporal evolution of the systems du/dt. First The use the MOL to nummerically solve this pde. This works by discretizing the pde as a system of ODEs, each descibing the temporal evolution of each node (x). These ODE F^ are now functions of each node poistion and state, and the neighbours positions and states.

- F^ is defined as a parametrized function (here a message passing graph neural network), and its parameters can be learned by minimzing the prediction error between the output of the last GNN layer at node i (which is here du_i/dt, it still needs to be integrated to get the prediction *u_i*) and the ground truth representation u_i.


## Technical details

- They make the GNN position invariant by defining the edge feature as the position difference between the nodes. This makes the GNN invariant to translation and rotations and assume absence of postion-dependent quantities.
- The MPNN only outputs the time derivative, it still needs to be integrated using (e.g Euler or Rugne-Kutta solvers) get the observation prediction.
- The input to the system is the observation at each time point. Yet when we train the model, we minimze the MSE between the predictions and the ground truth for the entire temporal duration of the observation.
- Here they use the adjoint method (similar to the Neural ODE method) to train the system in continous time, not discrete-time as mentioned in the last point.



## Results

- They evaluate the system perfomance at learning the dynamics of the convection-diffusion equation, heat equation and Burger's equations and show robust results.
- They conducted ablation studies on the number of gridpoints, timepoints, noise, irregularity of timepoints and show that the methods still works well under extreme sparsity although of course it still benifits from more fine-grained training data.


## Opinions and takeaways

- This work mainly discitize the PDE of the system into several ODEs, and utilize GNNs to solve each ODE independently.
- We are solving as many ODEs as we have nodes in the system. For each node a different MPNN is trained to solve each ODE.
- There is now an assumption that the entire system can be descibed independely. But I guess this method hinge on the accuracy of the graph defining the neigbourhoods.
