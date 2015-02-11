# Density Estimation in Infinite Dimensional Exponential Families

(I know it sounds ridiculously complicated, but it *is* quite cool!)

### Mentors
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Medium.
The mathematics behind this are very interesting, though not absolutely necessary to implement the algorithms, which are quite simple.

You need knowledge of:
 * Kernel methods in general
 * Density estimation basics
 * Basic (math+numerical) linear algebra. In particular linear systems
 * Come C++ knowledge, including designing class hierarchies

### Description
Density estimation is the technique of fitting a statistical model to data that comes from an unknown density.
This project is about implementing a new form of non-parametric density estimation, from [this paper](http://arxiv.org/abs/1312.3516). The idea is to learn the parameters of an un-normalised exponential family model whose parameters are elements of Reproducing Kernel Hilbert Spaces (RKHS). The estimation technique is based on [score-matching](http://www.cs.helsinki.fi/u/ahyvarin/papers/JMLR05.pdf), which is an estimation method that is based on matching gradients of the true and estimated model. The technique works better than the standard kernel density estimator (KDE), in particular in high dimensions.

### Details
The project involves re-thinking Shogun's classes for density estimation (there are existing methods). As this estimates the un-normalised density (as opposed to say KDE), a small base class hierarchy would be useful. We would have to work out interfaces etc before implementing algorithms.

The algorithm itself works via solving a linear system. Most work is to build this system, which involves gradients of kernel functions (these exist but may have to be slightly extended).

Free parameters of the algorithm are usually tuned via cross-validation, for which we want to use Shogun's framework, of course. The user should be able to just press a single button to get the best possible estimator.

### Waypoints and initial work
 * Come up with class design for density estimation
 * Put existing classes into that framework
 * Implement at least two different versions: The "exact" one from the paper, and an approximate one that is computationally cheaper. We will provide notes for the second
 * Carefully unit test against Python implementation (that we provide)
 * Stress test the implementation on large numbers of samples
 * Write a nice IPython notebook that reproduces experiments from the paper, which is a comparison against KDE

### Optional
None so far, but we might add.

### Why this is cool
The project implements a new cutting-edge research technique (that we use in our own research). You will learn about kernel methods, regularisation, and density estimation, which are all interesting subjects. You will help to keep Shogun's leading position in efficient kernel methods :)

### Useful ressources
 * [Infinite exponential family paper](http://arxiv.org/abs/1312.3516)
 * [Score matching paper](http://www.cs.helsinki.fi/u/ahyvarin/papers/JMLR05.pdf)
 * Kernel density estimation [notebook](http://www.shogun-toolbox.org/static/notebook/current/KernelDensity.html) and [wikipedia](http://en.wikipedia.org/wiki/Kernel_density_estimation)