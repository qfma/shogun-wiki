# A (yet incomplete and to be polished) list of potential GSoC 2015 projects.
Please create a new wiki page for each project that you describe (to keep this page small). Name them as "GSoC_2015_project_MCMC" etc. Here is a [template](GSoC_2015_project_template)

# Main focus
This year's GSoC is about improving Shogun, rather than extending it. Exceptions allowed.

 * *Fewer* new algorithms. Rather improve existing ones: Usability, efficiency, documentation, application
 * *Fewer* students. More intense mentoring, interaction between students, blogging, documenting
 * Projects on
   * Clean ups of: framework, build process, algorithms, usability, documentation
   * Removing legacy code
   * Efficiency: High performance computing, parallelisation, cloud, benchmarking
   * Applications: Using Machine Learning as a tool to improve the world, rather than toy examples
   * Pipelines & Framework: Improve usability on standard workflow pipelines
   * Usablity: Building and Installing Shogun has to be easier


# Finished descriptions
 * [HMMs for biological data](GSoC_2015_project_hmms)

## New things:
The projects we would like to limit in numbers.
 * [MCMC & Stan](GSoC_2015_project_MCMC_Stan)
 * [Density Estimation in Infinite Dimensional Exponential Families](GSoC_2015_project_kernel_infinite_exponential)


# TODO list
## Ideas to port from last year's list:
 * LP/QP optimisation framework.
 * [Easy installation on major platforms](GSoC_2015_project_installation)

## New ideas for which we need descriptions:
 * [Unifying Shogun's linear algebra](GSoC_2015_project_linalg)
 * [Deep learning](GSoC_2015_project_deep_learning)
 * [Fundamental ML: LGSSMs](GSoC_2015_project_fundamental)
 * [HMMs for biological data](GSoC_2015_project_hmms)

## Other ideas:
 * Cool pipelines
   * A kaggle pipeline for supervised prediction.
   * Spectrometer (there is an open-source hardward project on this)
   * Music brainz predictions (The cool hair guy at GSoC is the one we should talk to here)
   * Some bio thing?
   * Collaboration with MLPack for toolkit wide performance/accuracy testing

## Infrastructure:
 * Easy Model selection!
 * Easy linalg
 * Get rid of static interfaces, migrate all tests etc
 * Matlab swig bindings
 * [REST interface](GSoC_2015_project_rest)

## Clean ups:
 * Modularise Shogun
 * Replace parameter framework
 * Benchmark existing algos and improve!