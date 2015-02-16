# Hidden Markov Models for gene imputation
Cleaning up Shogun's HMMS and implementing a gene imputation pipeline

### Mentors
 * [Fabian Zimmer](http://qfma.de/) (github: [qfma](https://github.com/qfma))
 * [Heiko](http://herrstrathmann.de/) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Easy/medium/advanced.
You need to be able to
 * get confused by C/C++
 * trim beards
 * count socks

### Description
There are  three major parts to this projects
 * Cleaning up Shogun's HMM implementation (mostly to be done in pre-GSoC phase, see below)
 * Extending CHMM with a simple MCMC sampler
 * Build a workflow chain to impute genes

### Details
In genetics unobserved genotypes are often imputed from a more complete dataset, see [Imputation on Wikipedia](http://en.wikipedia.org/wiki/Imputation_(genetics)). One of the most popular tools uses Markov chain Monte Carlo to accomplish this [paper](http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1000529).

Fabian needs to put more details here.

### Waypoints and initial work
 * Step 1
 * Step 2
 * ...

### Optional
Parts of the project that would be cool once the core is finished.

### Why this is cool
Motivation to get involved here.

### Useful ressources
 * [Imputation on Wikipedia](http://en.wikipedia.org/wiki/Imputation_(genetics))
 * [MCMC for gene imputation paper](http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1000529)
 * Entrance tasks:
  * [Remove precompiler flags](https://github.com/shogun-toolbox/shogun/issues/2712)
  * [Unit test HMMs](https://github.com/shogun-toolbox/shogun/issues/2713)
  * [Document CHMM](https://github.com/shogun-toolbox/shogun/issues/2714)
  * [Clean up parallelisation](https://github.com/shogun-toolbox/shogun/issues/2715)
  * [Notebook on HMM](https://github.com/shogun-toolbox/shogun/issues/2716)
  * [All (most) HMM issues](https://github.com/shogun-toolbox/shogun/issues?q=is%3Aissue+is%3Aopen+hmm)