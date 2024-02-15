# Finding Self-dual Stabilizer code distance using QUBO approach
This program constructs a QUBO cost function whose minimization corresponds to finding the Hamming distance of a self-dual Stabilizer code. Solving the minimization problem can  be done using classical algorithms like Simulated Annealing (SA) or quantum ones like Quantum Annealing (QA) or using hybrid approaches, ex QBsolv. More details can be found in this paper (link will soon be posted on arxiv) along with an investigation into the efficiency of the three approaches. This code was written in collaboration between ([@Refat Ismail](https://github.com/RefatIsmail96)) and ([@Ashish Kakkar](https://www.linkedin.com/in/ashishkakkar21/)), while the paper with in collaboration with ([@Anatoly Dymarsky](https://scholar.google.com/citations?user=n9NSqaIAAAAJ&hl=en)) too.

## Installation
Running the correct environment.

## Working with code
The code constructs the QUBO and solves it using Neal's Simulated Annealing Sampler. It can be easily adjusted to run using other classical, quantum, and hybrid algorithms depending on the user's purpose.

Attached is a minimalist implementation of the code to show the core ideas. We construct the QUBO matrix using the generator matrix of a circulant self-dual code:
$$G^T = \left( I_{n}|B \right)$$ with B a circulant matrix and I_n the nxn identity matrix.
We introduce auxiliary variables to write the QUBO -see details in the paper-. Our cost function can then be written as:
$$\textbf{cost function} = \min_z z^T Q z$$
Where z is a list of binary variables consisting of: our original variables $x_i$ and the auxiliary variables $y_{i,j}$, arranged as $[x_1,x_2,...,x_n, \ y_{1,1},y_{2,1},...,y_{n,1}, \ y_{1,2},...,y_{n,r}]$. And the Q matrix will be made of multiple blocks as shown:
```math
Q = \begin{bmatrix} I_{n}+B^2 -B  & 2^0 (I_{n}-2B) & 2^1 (I_{n}-2B) & \dots & 2^{r-1} (I_{n}-2B)\\ 2^0 (I_{n}-2B) & 2^2 I_{n} & 2^3 I_{n}& \dots & 2^{r+1} I_{n} \\ 2^1 (I_{n}-2B) &  2^3 I_{n} & \ddots & \ddots & 2^{r+2} I_{n} \\ \vdots & \vdots & \ddots & \ddots & \vdots & \\ 2^{r-1} (I_{n}-2B) & 2^{r+1} I_{n}& 2^{r+2} I_{n} & \dots & 2^{2r} I_{n} \end{bmatrix}
```

This can be straightforwardly extended to non-circulant and non-self dual codes as well (see the paper for info).


