# LP/QP Framework
Cleaning up Shogun's HMMS and implementing a gene imputation pipeline

### Mentors
 * [Viktor Gal](http://qfma.de/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
**Advanced**. You need to be able to:
 - Cleanup and optimize C/C++ code
 - optimization theory
 - opencl/cuda knowledge

### Description
This task considers implementation of a framework for LP/QP optimization within Shogun. It shall be as modular as possible, since we want to have a general KKT solver as well as part of this project. The framework would be a thin wrapper that defines mappings for several existing and known optimization libraries (libqp, mosek, glpk, cplex, etc.). Using this framework implement a cone programming (both LP and QP).
