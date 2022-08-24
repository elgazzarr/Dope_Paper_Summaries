# [Diffusion Improves Graph Learning (Neurips 2019)](https://arxiv.org/pdf/1911.05485.pdf)


## What is the problem?

Spatial Graph Convolution Neural Networks use messeage passing between direct (one-hop) neighbours to learn node features. While higher order neigbourhood information can be incroporated by adding more layers, learning at each layer is still limited by only direct neighbours of the node. Further, often in real world graphs, the graph structure is noisy and sometimes arbitarly defined which 
can further hinder learning. 

## What is the solution?

Replace message passing with a sparsified disctritized form of a diffusion process.

## How?

They use either one of known speical examples of diffusion (personalized PageRank and the heat kernel) to define the diffusion process. In short, both variants only differ in the way the diffusion coeffecients are defined, but can use any general form of transition matricies. (Here they used Random Walk (AD^-1) but one cane use anything such as the popular symmetric transition matrix(D^(-1/2)AD^(-1/2))

## Technical Details

- Technically, all GNNs can be defined using a a generalized diffusion process. For example Kipf&Welling GCN use only first order approximation of the diffusion series (setting theta1 equal to 1 and the rest to zero and use the symmetric tansition matrix)
- We have to ensure that the diffusion series converge.
- Essentialy what happens with diffusion processes is that know replace your adjacency matrix with a new graph structure defined using this desnity (heat for example) which is very dense. You can have to then sparsify it and then used this sparse version to define the neighbouhood.
- Note that this is done K times at each layer. 
- To sparsify the graph we can use top-k truncation or a threshold.


## Results

- They evlaute using graph diffusion in 5 popular graph neural network architecures using both diffusion kernels on six node classifcation datasets and show that almost conistently either or both of the variants imporve upon not using them.
- They state that results for graph classification are 'promising' but not as consitent.


## Opinions and takeaways

- The paper is an example of a straightforward incremental improvment that can be easily added to exisitng solutions with no much hassle and computational overhead.
- The general intuition behind the idead is that diffusion smooths out the nighebhood over the graph and thus it acts as kind of denoising filter. This can be helpful in noisy settings and I think it makes sense that it improves the perfomance of GNNs.
- If the graph struture is not noisy, you can be losing some fine grained details that are essential. 
- What other kernels can be used to defined diffusion?
- Is there a way to make this diffusion process continous in the actual time domain of the data and not in the spectal domain? . i.e. diffusion on a graph with temporal features at the nodes and the graph structure is dynamically evolving?


