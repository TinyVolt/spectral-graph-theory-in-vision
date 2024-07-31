# spectral-graph-theory-in-vision
Repo for the sharing on applications of spectral graph theory in computer vision

## Notes
- [A primer on Spectral Graph Theory](https://hackmd.io/@vinsis/B1V4tkX_s)
- [Algebriac Connectivity](https://en.wikipedia.org/wiki/Algebraic_connectivity)
- [EAGLE](https://micv-yonsei.github.io/eagle2024/)

## A hand-wavy explanation of algebriac connectivity and Laplacian eigenvalues

Consider the adjacency matrix shown below:

Consider the adjacency matrix shown below with non-negative entries:

```math
 \begin{bmatrix}
p & q & r \\
q & s & t \\
r & t & u 
\end{bmatrix}  
```

Then the Laplacian matrix is

```math
L = \begin{bmatrix}
q+r & -q & -r \\
-q & q+t & -t \\
-r & -t & r+t 
\end{bmatrix}
```

Now consider the bilinear form $vTLv$ where $v^T = [x,y,z] $:

```math
v^TLv = \begin{bmatrix} x & y & z \end{bmatrix} \begin{bmatrix}
q+r & -q & -r \\
-q & q+t & -t \\
-r & -t & r+t 
\end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix} = q(x-y)^2 + r(x-z)^2 + t(y-z)^2
```

Since the Laplacian is symmetric positive semi-definite, all eigenvalues are non-negative.

We can draw a few observations from the above form:
1. The value is non-negative. Thus its minimum value is 0 when $x = y = z$. Thus the vector $1$ is the eigenvector with the corresponding eigenvalue 0.
2. The second smallest eigenvalue can be seen as an optimization (minimization) of the expression $q(x-y)^2 + r(x-z)^2 + t(y-z)^2$. We need to find an interpretation of this expression.

    2.1  This expression can be written in a more human readable form as: `sum of v[i]-v[j] squared and weighted by the edge i-j`.
    
    2.2 To minimize this sum, the weight corresponding to a large `v[i]-v[j]` should be the small.

    2.3 In other words, whenever the edge `i-j` is _weak_ (i.e. small), the corresponding coordinate values `v[i]` and `v[j]` will be large - in other words, they will most likely have opposite signs.

    2.4 Similarly, whenever the edge `i-j` is _strong_, the corresponding coordinate values `v[i]` and `v[j]` will be small - in other words, they will most likely have similar signs.

This argument can be extended to a matrix of any dimension.
