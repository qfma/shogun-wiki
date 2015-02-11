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

As models in Shogun are fixed, one way to combine them with Stan would be to implement the models in Stan's language, and integrate the generated C++ code into Shogun in our build process in an automated way. Tricky because
 * Reproducing Shogun's models in Stan requires to understand the code in all explicit details
 * The Shogun build has to be modified to "compile" the Stan code, which then interacts with Shogun

### Waypoints and initial work
One of the first steps would be to try to expose Stan's distributions (sampling, log-pdf & gradients) within Shogun, see also the [github issues](https://github.com/shogun-toolbox/shogun/issues?q=is%3Aissue+is%3Aopen+stan) on that topic. From there, stepping to full Stan models is the next step.

 * Write a wraper class that exposes a given C++ Stan model within Shogun's framework. This also is great for the Stan people as their models will be usable from all of Shogun's modular targets. It includes data IO.
 * Implement a single Shogun model (say GP regression) in Stan and make sure the semantics are the same. Use above point to expose it
 * Design a Shogun class framework that allows to easily interact with Stan's MCMC mechanics, so that the above wrapper classes can be used to use MCMC for inference
 * Reproduce the output of an existing (exact or approximate) inference algorithm in Shogun with the new MCMC based Stan bindings.

### Optional
The automatic differentiation of Stan is something any ML toolbox should take advantage of. An optional part of the project would be to explore way to enable autodiff in Shogun via Stan. One idea
 * Select a single kernel, say ```CGaussianKernel```
 * Re-implement in Stan
 * Create new class (or a member of ```CSGObject```) that contains a wrapper to the C++ code produced by Stan which contains all the gradients. This member/class would only be available if Shogun is compiled with Stan/autodiff enabled
 * Reproduce a hard-coded gradient with this automagically generated one
 * Systematically enable the use of these autodiff wrappers within all Shogun objects
 * Benchmark speed
 * Replace existing gradients if faulty or slower
 * Document for future use

### Why this is cool
Stan is an übercool project to learn about. MCMC is an amazing inference technique that will massively broaden Shogun's applicability. It is in particular cool to contemplate our growing set of fixed approximate inference algorithms with the full MCMC alternative. There does not exist a tool which contains *both* MCMC and fast approximate inference for a general set of Bayesian models. Automatic differentiation is a fascinating tool which should be used whenever gradients are needed -- no more manual derivations (with mistakes) and implementations (with more mistakes).

### Useful ressources
 * [Stan website](http://mc-stan.org/)