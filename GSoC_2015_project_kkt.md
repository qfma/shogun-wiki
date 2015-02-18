# Solver for the KKT System

### Mentors
 * [Jacky Chow]((jckchow_at_ucalgary.ca))
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
**Medium**. You need to be able to:
 - C++
 - Optimisation theory

### Description
Inequality constraints are frequently encountered in machine learning, geostatistics, and modelling problems. In the past, interior point methods have proven to be an effective and efficient approach for solving large-scale SVMs. This project focuses on developing an interior point solver for solving various problems in Shogun. The developed algorithm will be tested in Gaussian Processes with complex kernels; for example modelling the signal strength of Wi-Fi.  Besides recovery of the unknown parameters, this project will also investigate methods to deliver accurate and consistent uncertainty measures for the parameters.

This project will work closely with the “LP/QP Optimization Framework” to ensure the developed solver is compatible with the framework.

## Why this is cool
Numerical optimization is a fundamental tool is many science and engineering disciplines.  You’ll learn about the interior point method, which is a promising optimization approach with great flexibility to handle different types of constraints.  In addition, you get to apply your results to real-life problems, which is to model the spatial variations of Wi-Fi signal strengths using Gaussian Processes.