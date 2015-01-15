# Motivation
Linear algebra operations form the backbone for most of the computation components in any Machine Learning library. However, writing all of the required linear algebra operations from scratch is rather redundant and undesired, especially when we have some excellent open source alternatives. In Shogun, we prefer 
- [Eigen3](http://eigen.tuxfamily.org/index.php?title=Main_Page) for its speed and simplicity at the usage level,
- [ViennaCL](http://viennacl.sourceforge.net/) version 1.5 for GPU powered linear algebra operations, and
- [Lapack](http://www.netlib.org/lapack/) for its robustness and maturity.

For Shogun maintainers, however, the usage of different external libraries for different operations can be a painful task. For example, assume that some part of an algorithm was written using Eigen3 API. But a Shogun user wishes that she would use ViennaCL to utilize her new GPU powered system. There is no way to do that without having the algorithm be pretty much rewritten. There is no easy way to compare the performance of the linear algebra operations in Shogun algorithms as well while using different backend libraries. Also, a Shogun developer has to invest significant amount of time and effort to learn each of these external APIs while adding a new algorithm to Shogun.

## Features of internal linear algebra library
Shogun's internal linear algebra library (will be referred as `linalg` hereinafter) is a Work-In-Progress attempt to overcome these difficulties. We divided the supported linear algebra operations under different modules. 
- It provides a uniform API for Shogun developers to choose any specific backend without having to worry about the syntactical differences in the external libraries' operations. 
- All of these operations are designed to handle native Shogun types. 

These operations can be used in two ways
### Use-case 1 : Relying on globally set linalg backend
```c++
shogun::linalg::operation(arg1, ...);
```
- Global setup is used whenever an operation is used without specifying a particular backend.
- Preferred backend can be set via `cmake` options which is set globally for all the linear algebra operations using `linalg`.
```bash
# this will set Eigen3 as the global linalg backend for all modules.
# Use -DUSE_VIENNACL for setting ViennaCL as global linalg backend instead
#
# for other cmake options, please refer to the cmake wiki.
cmake -DUSE_EIGEN3
```
- Module specific global setups can also be possible which is again set via `cmake` options. We presently have 2 modules - Core and Redux
```bash
# this will set Eigen3 for Redux module's global linalg backend
# and ViennaCL for Core module's global linalg backend.
cmake -DUSE_EIGEN3_REDUX -DUSE_VIENNACL_CORE
```
- If no particular setup is specified via `cmake` options (or only one module specific setup is specified), a `Default` backend (Eigen3 at this moment) is used for the unspecified modules.

### Use-case 2 : Using specific linalg backend
```c++
shogun::linalg::operation<Backend::backend_name>(arg1, ...);
```
- It is possible to use a specific backend for some particular operation, which then ignores the global or module specific setup and works with that particular backend.