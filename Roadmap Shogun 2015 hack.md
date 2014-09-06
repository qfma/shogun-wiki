# Shogun hack 2015 Ideas
This is a list of topics to address when all Shogun developers get together. We aim to have a structured list of items, with links to existing or newly created github issues. Feel free to merge this with content from the other Wiki pages or discussions.

## Usability.
* A meta-langauge for Shogun example: [#2508](https://github.com/shogun-toolbox/shogun/issues/2508). 
* Website updates (Kevin had some ideas?)
 * Developer information (wiki or website?) [#2533](https://github.com/shogun-toolbox/shogun/issues/2533)
* Manifest "What is Shogun? What tries Shogun to be?"
* Notebooks of things that are not yet covered
* Binary packages for various OS 
 * Ubuntu LTS [#2520](https://github.com/shogun-toolbox/shogun/issues/2520)
 * OSX [#2521](https://github.com/shogun-toolbox/shogun/issues/2521)
* Improve [Shogun development guidelines](Shogun development guidelines)
* Scheduling a separate release for "easier installation": packages and scripts for Ubuntu/Debian/MacOSC
  https://github.com/shogun-toolbox/shogun/milestones/Shogun%203.4.1

## Efficiency & Clean-ups
* Efficient and flexible data structure for n-dimensional array [#2123](https://github.com/shogun-toolbox/shogun/issues/2123) [#2530](https://github.com/shogun-toolbox/shogun/issues/2530) 
* Modularise Shogun to reduce compile memory requirements [#2437](https://github.com/shogun-toolbox/shogun/issues/2437) (some prototype is https://github.com/lisitsyn/aer)
* Serialisation via external library (Viktor?)
* General polishing of base classes [#2113](https://github.com/shogun-toolbox/shogun/issues/2113)(Thoralf?)
* DPointers (again https://github.com/lisitsyn/aer)

## Computing Backends.
* Parallelism backend interface
 * Batch cluster backend (PBS/SGE,SLURM,etc) [#1622](https://github.com/shogun-toolbox/shogun/issues/1622)
 * Pthread/openMP backend [#1623](https://github.com/shogun-toolbox/shogun/issues/1623)
 * Director classes to use Shogun as scheduler from modular interface [#1624](https://github.com/shogun-toolbox/shogun/issues/1624)
 * Add dependencies between jobs [#2524](https://github.com/shogun-toolbox/shogun/issues/2524)
 * Graphlab backend [#2525](https://github.com/shogun-toolbox/shogun/issues/2525)
 * Zookeeper coordination?
* Populate internal Linear algebra interface
 * Add matrix factorisations [#2526](https://github.com/shogun-toolbox/shogun/issues/2526)
 * Add linear solves [#2527](https://github.com/shogun-toolbox/shogun/issues/2527)
* Stan for autodiff and MCMC [#1875](https://github.com/shogun-toolbox/shogun/issues/1875) [#1998](https://github.com/shogun-toolbox/shogun/issues/1998) [#1929](https://github.com/shogun-toolbox/shogun/issues/1929) 
* Vowpal Wabbit update

## SHOGUN goes large-scale
* Investigate how non-toy examples scale in SHOGUN.
* Increase awareness of benchmarking and profiling:
 * Identify hotspots using selected examples and right tools (gprof?).
 * Create minimal example(s!) which covers hotspot and benchmark.
 * Start optimizing minimal example(s!) and benchmark again.
* Developers should know how to benchmark and profile: Small document to describe this?
* If you know examples that scale better in other frameworks, please document them here, so we can investigate:
 * ...
* Better support of sparse-datastructures and online-algorithms.

