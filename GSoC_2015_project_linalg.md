# `linalg`: Unifying Shogun's linear algebra

### Mentors
 * [Rahul](Rahul%20De) (github: [lambday](https://github.com/lambday), IRC: lambday)
 * [Sergey](Sergey%20Lisitsyn) (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
**Medium**. You need knowledge on
 * Advanced C/C++ (knowledge about C++11 is a plus). A reasonable level of comfort with templates, template specialization, partial specialization, SFINAE, ability to read complex templated code
 * Numerical Linear algebra
 * Eigen3, LAPACK (src level familiarity is a plus)
 * GPU programming (OpenCL/ViennaCL)
 * Shogun algorithms
 * OpenMP [Optional]

### Description
This project aims to finalize and polish Shogun's internal framework for linear algebra. The goal is to offer our algorithm coders a *backend independent* interface that they can use for their linear algebra calls, such as
 * factorizing matrices
 * linear solvers
 * eigen solvers
 * applying the same operation to every element of a large matrix
 * dot products
 * various utilities
Rather than writing implementation against particular backends (we currently use Eigen3, Lapack, ViennaCL and Shogun's native implementation), algorithms should be written against ```linalg```. This allows to change backends at compile time, and in particular makes our algorithms independent of the current trend in linear algebra software. It also will allow to put many operations on GPUs *without* changing the implementation (to an extend).

### Details
 * Presently, a handful of operations are there in `linalg`, spread over two different modules, `Core` and `Redux`. See the README file for a complete list of operations.
 * The first target is to **populate `linalg` with most-used linear algebra operations** for both dense and sparse matrices. This includes figuring out a nice way to handle 
    * element-wise operations
    * col/row-wise operations 
    * in-place operations (useful for large matrices)
    * block-based operations 
*while* using different third party/native backend. We'll be using Eigen3, ViennaCL/OpenCL, (optionally) LAPACK. We don't want native implementation for everything, just the ones we've already got. So in most cases native implementation would involve moving existing code from other parts of Shogun to `linalg`. 
 * Most important part of this job is matrix factorization/linear solvers/eigen solvers. This requires some investigation on the benefits/disadvantages of storing the factorization results for successive linear/eigen solver calls. We want at least 
    * Cholesky
    * QR
    * LU
    * Eigen
    * SVD
(see issue #2526, #2527).
 * A large part will be to read through Shogun's core algorithms and make them use the new interface. 

### Waypoints and initial work
 * Create github issues on using the existing linalg calls in algorithms
 * Rahul, can you spell out the steps that have to be done? Like which type of operations, that we want them all in Eigen3/LAPACK/OpenMP/Vienna/native, etc?
 * ...

### Optional
Rahul, maybe do an openmp backend for the independent jobs? Not sure here though. What do you think?

### Why this is cool
This project will massively increase both performance and sustainability of Shogun. We will get parallelism of many algorithms for free and at the same time open up ways for using different, better, backends (such as GPUs) in the future. It will furthermore allow to write algorithms without knowledge of backend internals. Nobody wants to deal with Lapack directly ;)

### Useful resources
 * [linalg README](https://github.com/shogun-toolbox/shogun/wiki/README_linalg)