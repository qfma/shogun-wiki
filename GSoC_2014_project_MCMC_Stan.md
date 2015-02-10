# Enabling MCMC based inference via Stan
(yet incomplete)

### Mentors
 * Fernando (github: [iglesias](https://github.com/iglesias), IRC: iglesias)
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Advanced.
You will need knowledge about:
 * Stan itself, how to use it, basics about its internals
 * Building C++ code and modifying builds
 * MCMC and Bayesian modelling mainly to structure and write documentation
 * Documentation skills
 * Shogun's probabilistic models
 * Optional: Automatic differentiation in Stan
 * Optional: SWIG

### Description
Markov Chain Monte Carlo (MCMC) is a fundamental tool for inference in Bayesian models. As Shogun contains a number of models that fall in the category (e.g. Gaussian Processes, Gaussian Mixture Models), we would like to enable MCMC based inference for them. Stan is the de-facto standard for defining real valued models and perform automatic inference for them via a state-of-the-art Hamiltonian Monte Carlo sampler. We would like to use Stan from within Shogun, which is not trivial.

### Details
Stan models are defined via the Stan language, which is then parsed by the Stan compiler and translated to C++ code, which itself is then compiled to a binary. This binary contains the model and everything that is needed to perform sampling/optimisation on it. In particular, the Stan compiler performs automatic differentiation to generate C++ code for all gradients of the user-defined log-pdf code of the model.

As models in Shogun are fixed, one way to combine them with Stan would be to implement the models in Stan, and integrate the generated C++ code into Shogun in our build process in an automated way.


### Why this is cool

### Useful ressources
 * [Stan website](http://mc-stan.org/)