# FPGA-ADMM-analysis

In ADMM, we update variables u, v, and λ iteratively. A key computational challenge arises during the u-update, u^{k+1}={(Q+\tau A^TA)}^{-1}(A^T(\lambda^k+\tau v^k)-q), which involves matrix inversion and multiplication. This process can be computationally expensive, especially when dealing with the cached inverse matrix (the inverse term) of large dimensions.
Matrix multiplication has a computational cost proportional to the size of the matrices. For two matrices of dimensions m×n and n×p, the number of operations required is:
Operations\ =m\times n\times p
The goal is to reduce the number of computations during the u-update step by using low-rank approximations via Singular Value Decomposition (SVD). The Singular Value Decomposition (SVD) allows you to approximate a matrix by breaking it into three components:
M=U\Sigma V^T

The cached inverse matrix is of dimensions 50x50 and the remainder of the update equation results in a matrix of dimension 50x1. Following the earlier formula for calculating number of operations , the no. of operations here result to 50*50*1=2500.
We aim to use SVD based low rank approximation of the cached inverse matrix to reduce the number of operations for the u-update.

The graphs folder contains the iterations vs error (primal and residual) graph for three types of ADMM viz. Basic, Accelerated and Accelerated with restart. There are 4 graphs for each type of ADMM, compraing the convergence behaviour when:
1. The cached inverse matrix is considered with no low rank approximation i.e. r=50
2. The cached inverse matrix is considered with low rank approximation of r=8.
3. The cached inverse matrix is considered with low rank approximation of r=16.
4. The cached inverse matrix is considered with low rank approximation of r=32.
