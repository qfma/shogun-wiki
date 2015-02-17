#Independent jobs Framework

### Mentors
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
**Advanced**. You need to be able to:
 - distributed computing
 - mesos
 - openmp
 - c++

### Description
Although Shogun has a huge selection of ML algorithms currently it lacks support for parallel processing, i.e. running these algorithm using multiple cores or multiple nodes in a cluster.

2 years ago, as part of a GSoC project an Independent Computing Framework has been introduced to Shogun, but it has been applied in handful of algorithms. Hence one of the objective of this task would be to introduce the framework to other algorithms in Shogun that could benefit from using parallel processing.

The main objective of this project would be to unify the way parallel processing is being done within the library as currently there are algorithms in Shogun that are using OpenMP and others that are using native POSIX pthreads API to do parallel processing. The way this should be done is to define a unified parallel processing API, which supports both multi-core and multi-node distributed computing. A good example for this is Spark where an environmental variable (MASTER) defines whether the tasks are being run on a cluster or different cores of a local machine. Apart from this the API should as well define basic operations like parallel loop.

Ideally, the implemented API should be accessible from the modular interfaces as well.