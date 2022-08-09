# [GRAND: Graph Neural Diffusion (ICML 2021)](http://proceedings.mlr.press/v139/chamberlain21a/chamberlain21a.pdf)



## What is the problem?

There is not really a problem here. This is a new angle to view Graph neural networks as continuous diffusion processes enabling the development of a new family of GNNs.


## What is the solution?

Message passing is a diffusion process on some manifold. We can derive a partial differential equation using the general form of Fourier's law of heat equation and continuity equation which states the change of heat (flux) is equal the divergence of diffusivity times the change in position (or diffusivity times Laplacian of X).    


## How?

The driven pde can be solved using different methods. Standard GCN solve this as an explicit Euler method with iterations analogous to the number of layers. The formulation of the GNN as a PDE can enable the to use a wide array of more advanced PDE solvers where you have control over stability and uses and adaptive step size.  



## Technical details

- GRAND can be linear if the attention weights of A is fixed (does not depend on X) and the PDE can be solved analytically.
- GRAND non-linear uses adaptive multi-step solvers 
- The graph is already given spatially discretized (We have the graph structure) but you can use the graph rewiring (using different thresholds) find the pde solution over all possible graph structures. This the version GRAND-nl-rw and I imagine it is much more robust. 
- They use the same set of weights across all iterations/layers.



## Results

- They show robust results on three node classification results.
- Surprisingly, the linear version of GRAND performs the best, which makes you wonder about the difficulty of the task.
- They empathize that the model uses less parameters because the weights are shared.


## Opinion and takeaways

- I like this flexible formulation of the problem. 
- This is still a discretization, but a more adaptive discretization.
- There are lots of assumption here that makes me wonder about their application to solve science problems. e.g. initial condition given, static graph structure, known graph structure (although they claim it can be extended to learning it from scratch) 

