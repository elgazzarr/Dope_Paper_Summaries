# [Hamiltonian Neural Netowkrs (Neurips 2019)](https://proceedings.neurips.cc/paper/2019/file/26cd8ecadce0d4efd6cc8a8725cbd1f8-Paper.pdf)


## What is the problem?

Deep neural networks are not incroportated by priors about the phsyical laws of the system it is trying to model/ learn from. If needed, they only implicilty learn to approximate some laws to be able to solve the task. This can lead to errors accumlation in forward simulations (drifting) and training can be highly sample-ineffecient.

## What is the solution?

Well, equip the neural network with physical priors. Here they lean onto Hamiltonian mechanics, which relates systems coordianties into a scalar function (The hamiltonian, usualy indicate energy or energy-like value). The evolution of the system coordiantes in time can be described as the derivative of the hamiltonian with respect to these coordiantes.


## How?
Parametrize a neural network that takes coordiantes and output the hamiltonian scalar and then compute the L2 loss using the gradient of this socre with respect to the inputs.


## Technical details


- They used simple Fully connected networks for all the experiments.
- The ground truth (time derivatives of the coordiantes) are computed either analytically or using finite difference approximations.
- The Hamiltonian neural network is trained to minimze this hamiltonian loss while baseline model is trained directly to minimze the prediction error between gradient predictions.


## Results

- They show superior results on systems with known dynamics and coordiantes using simulations (e.g. frictionless mass-spring and inverse non-linear pedulum)
- They also show that the method can work on higher dimensional settings (N-body problem) and can learn directly from pixel observations.
- For learning from observations, they train an autoencoder to find the coordinates and then use the latent dimensions to opimtimize the hamiltonian loss. 

## Opinions and takeaways

- This is a great paper that motivates incoporating conservation law into the neural network.
- The model is very sample effecient
- A drawback is that the model blindly learns that energy is conserved so it does not account for any loss that happens (e.g. due to friction) and this has to be modelled seperately
- Learning directly from observations such as the pixels experiment is the most promising direction since in most unsolved problems, we dont really know the useful coordinate system that best describe the system. More work can be made to find even better coordinates in dynamically evolving systems.  e.g. LSTMs, state space models, beta-VAEs
