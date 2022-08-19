# [Physics Informed Deep Learning](https://www.sciencedirect.com/science/article/pii/S0021999118307125)


## What is the problem?

Often when we use deep learning to solve a problem, we train a model to optimize a defined loss function that minimze the error between its predictions and the ground truth. While a powerful concept, it does not enforce the model to respect any rules that we might know exist in the data/enviorment (e.g. laws of physics). Encoding these rules can improve data effecinecy and drive the model to learn the true causal dynamics of the process it is learning from.

## What is the solution?

Here they introduce Physics Informed Neural Networks (PINNs), a new class of NN that are trained to solve supervised learning tasks while repsecting any given law of physics described by general nonlinear partial differential equations. They introduce two classes of the model :
1- data-driven solution of pdes.
2- data driven discovery of pdes. (it is not entirely true, it just some 'coeffecients' of the already known pde)

## How?

- Using a neural network to obtain the latent dimensions (u).  
- Derive the pde (f) descirbing the data using the equation and derivatives of the latnet dimension
- Minimize two MSE errors, one for the latent dimension using the boundary and initial conditions (already known) to find u, and the other is on the observational data to find f.


## Technical Details

- By training the NNs with the two losses, and since the parameters are shared between f and u, the NN is forced to solve the pde to obtain the data-driven solution.

- They present discritized version using Runge-Kutta discritization of the equation and then use sum of square of errors to train the network

- The framwork can handle peridoic boundary conditions by using another loss for the boundary conition and complex-valued solutions by designing a two output NN for the latent dimension. 


## Results

- They show the flexibility of the model in solving a wide range of known PDEs

## Opinions and takeaways

- This is a very exciting direction moving forward with NNs, as it 
- My main concern is in these problems, you already know the underlying phsyics of the enviroment and the governing pde. In their *data-driven discovery* class, the model can only estimate some constant parameters of the equation, yet it doesnot know the terms.
- We can create a library of terms agains similar to SIDny and try to do sparse regression on the terms. 
- How does the selection of the NN affect the latent dimensions? Can I also use an inductive bias in the NN to improve the representations?
- What if I dont know the boundary conditions on my latent dimensions? Is it suffecient to train the network using observations?


