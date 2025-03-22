# FPGA-ADMM-analysis

In ADMM (Alternating Direction Method of Multipliers), we update variables u, v, and λ iteratively. A key computational challenge arises during the u-update

![Screenshot](./images/Screenshot%202025-03-22%20183506.png)

which involves matrix inversion and multiplication. This process can be computationally expensive, especially when dealing with the cached inverse matrix (the inverse term) of large dimensions.

Matrix multiplication has a computational cost proportional to the size of the matrices. For two matrices of dimensions m×n and n×p, the number of operations required is:
Operations =m*n*p

The goal is to reduce the number of computations during the u-update step by using low-rank approximations via Singular Value Decomposition (SVD). The Singular Value Decomposition (SVD) allows you to approximate a matrix by breaking it into three components:

![Screenshot](./images/Screenshot%202025-03-22%20183604.png)

By retaining only the top r singular values (with r<50), we can approximate the inverse matrix and reduce the number of operations required for matrix multiplication. This reduces the computational cost while maintaining acceptable accuracy.

The cached inverse matrix is of dimensions 50x50 and the remainder of the update equation results in a matrix of dimension 50x1. Following the earlier formula for calculating number of operations , the no. of operations without any low-rank approximation (r=50) is:
50*50*1=2500.
We aim to use SVD based low rank approximation (using r=8, r=16 and r=32) of the cached inverse matrix to reduce the number of operations for the u-update.

### Graphs Analysis

The `SVD graphs` folder contains the iteration vs error (primal and residual) graphs for three types of ADMM:

1. **Basic ADMM**
2. **Accelerated ADMM**
3. **Accelerated ADMM with Restart**

For each type of ADMM, the convergence behavior is compared under four scenarios:

1. Cached inverse matrix with no low-rank approximation (\(r = 50\)).
2. Cached inverse matrix with low-rank approximation (\(r = 8\)).
3. Cached inverse matrix with low-rank approximation (\(r = 16\)).
4. Cached inverse matrix with low-rank approximation (\(r = 32\)).

These graphs allow us to analyze the trade-off between computational complexity and convergence accuracy.
