# linalg: Unifying Shogun's linear algebra

### Mentors
 * Rahul (github: [lambday](https://github.com/lambday), IRC: lambday)
 * Sergey (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Medium
You need knowledge on
 * Advanced C/C++ (with all the new fancy stuff in C++11)
 * Numerical Linear algebra
 * OpenMP
 * GPU programming (ViennaCL)
 * Shogun algorithms

### Description
This project aims to finalise and polish Shogun's internal framework for linera algebra. The goal is to offer our algorithm coders a *backend independent* interface that they can use for their linear algebra calls, such as
 * factorising matrices
 * linear solves
 * applying the same operation to every element of a large matrix
 * dot products
 * etc
Rather than writing implementation against particular backends (we currently use Eigen3, Lapack, and native), algorithms should be written against ```linalg```. This allows to change backends at compile time, and in particular makes our algorithms independent of the current trend in linear algebra software. It also will allow to put many operations on GPUs *without* changing the implementation (to an extend).

### Details
Rahul, this is for you
 * What has been done?
 * What is to be done?
 * Where do we want to get?
 * A large part will be to read through Shogun's core algorithms and make them use the new interface

### Waypoints and initial work
 * Create github issues on using the existing linalg calls in algorithms
 * Rahul, can you spell out the steps that have to be done? Like which type of operations, that we want them all in Eigen3/LAPACK/OpenMP/Vienna/native, etc?
 * ...

### Optional
Rahul, maybe do an openmp backend for the independent jobs? Not sure here though. What do you think?

### Why this is cool
This project will massively increase both performance and sustainability of Shogun. We will get parallelisation of many algorithms for free and at the same time open up ways for using different, better, backends (such as GPUs) in the future. It will furthermore allow to write algorithms without knowledge of backend internals. Nobody wants to deal with Lapack directly ;)

### Useful ressources
 * [linalg readme](https://github.com/shogun-toolbox/shogun/wiki/README_linalg)