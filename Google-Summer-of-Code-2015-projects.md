# A (yet incomplete and to be polished) list of potential GSoC 2015 projects.
Please create a new wiki page for each project that you describe (to keep this page small). Name them as "GSoC_2015_project_MCMC" etc. Here is a [template](GSoC_2015_project_template)

# Main focus
This year's GSoC is about improving Shogun, rather than extending it. Exceptions allowed.

 * *Fewer* new algorithms. Rather improve existing ones: Usability, efficiency, documentation, application
 * *Fewer* students. More intense mentoring, interaction between students, blogging, documenting
 * Projects on
   * Installation: most important
   * Clean ups of: framework, build process, algorithms, usability, documentation
   * Removing legacy code
   * Efficiency: High performance computing, parallelisation, cloud, benchmarking
   * Applications: Using Machine Learning as a tool to improve the world, rather than toy examples
   * Pipelines & Framework: Improve usability on standard workflow pipelines
   * Usablity: Building and Installing Shogun has to be easier


# Projects
## Improving Shogun
 * [**Easy installation on major platforms**](GSoC_2015_project_installation)
 * [Native MS Windows port](GSoC_2015_windows)
 * [HMMs for biological data](GSoC_2015_project_hmms)
 * [Unifying Shogun's linear algebra](GSoC_2015_project_linalg)
 * [Shogun cloud extensions](GSoC_2015_cloud_shogun)
 
## Extending Shogun:
The projects we would like to limit in numbers.

### Algorithms
 * [Fundamental ML 2: LGSSMs](GSoC_2015_project_fundamental)
 * [Solver for the KKT System](GSoC_2015_project_kkt)
 * [LP/QP Framework](GSoC_2015_project_lpqp)
 * [Density Estimation in Infinite Dimensional Exponential Families](GSoC_2015_project_kernel_infinite_exponential)
 * [Hip Deep learning](GSoC_2015_project_deep_learning)

### Framework
 * [Independent jobs Framework](GSoC_2015_cluster_shogun)
 * [MCMC & Stan](GSoC_2015_project_MCMC_Stan)


# TODO list
## Other ideas:
 * Cool pipelines
   * A kaggle pipeline for supervised prediction.
   * Spectrometer (there is an open-source hardward project on this)
   * Music brainz predictions (The cool hair guy at GSoC is the one we should talk to here)
   * Some bio thing?
   * Collaboration with MLPack for toolkit wide performance/accuracy testing

## Infrastructure:
 * Easy Model selection!
 * Get rid of static interfaces, migrate all tests etc
 * Matlab swig bindings
 * [REST interface](GSoC_2015_project_rest)

## Clean ups:
 * Modularise Shogun
 * [Replace parameter framework](GSoC_2015_project_parameters)
 * Benchmark existing algos and improve!