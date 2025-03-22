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


# FPGA-ADMM-Analysis

In ADMM (Alternating Direction Method of Multipliers), we iteratively update the variables \(u\), \(v\), and \(\lambda\). A key computational challenge arises during the u-update step:

\[
u^{k+1} = (Q + \tau A^TA)^{-1}(A^T(\lambda^k + \tau v^k) - q)
\]

This step involves matrix inversion and multiplication, which can be computationally expensive, especially when dealing with large matrices. The matrix inversion term \((Q + \tau A^TA)^{-1}\) is cached to reduce the complexity, but even so, matrix multiplication can still be costly.

For matrix multiplication, the number of operations required is proportional to the size of the matrices. For two matrices of dimensions \(m \times n\) and \(n \times p\), the number of operations is:

\[
\text{Operations} = m \times n \times p
\]

### SVD-Based Low-Rank Approximation

The goal is to reduce the number of computations during the u-update step by using low-rank approximations via Singular Value Decomposition (SVD). The SVD of a matrix \(M\) is given by:

\[
M = U \Sigma V^T
\]

By retaining only the top \(r\) singular values (with \(r < 50\)), we can approximate the inverse matrix and reduce the number of operations required for matrix multiplication. This reduces the computational cost while maintaining acceptable accuracy.

### Computational Complexity Example:

- The cached inverse matrix is of dimensions \(50 \times 50\), and the remainder of the update equation results in a matrix of dimension \(50 \times 1\).
- Without any low-rank approximation (\(r = 50\)), the number of operations is:

\[
50 \times 50 \times 1 = 2500 \text{ operations}
\]

- By using SVD-based low-rank approximation with \(r = 8\), \(r = 16\), and \(r = 32\), we can reduce the number of operations proportionally.

### Graphs Analysis

The `graphs` folder contains the iteration vs error (primal and residual) graphs for three types of ADMM:

1. **Basic ADMM**
2. **Accelerated ADMM**
3. **Accelerated ADMM with Restart**

For each type of ADMM, the convergence behavior is compared under four scenarios:

1. Cached inverse matrix with no low-rank approximation (\(r = 50\)).
2. Cached inverse matrix with low-rank approximation (\(r = 8\)).
3. Cached inverse matrix with low-rank approximation (\(r = 16\)).
4. Cached inverse matrix with low-rank approximation (\(r = 32\)).

These graphs allow us to analyze the trade-off between computational complexity and convergence accuracy.

