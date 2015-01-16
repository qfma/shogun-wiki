# Internal linear algebra library
## Motivation
Linear algebra operations form the backbone for most of the computation components in any Machine Learning library. However, writing all of the required linear algebra operations from scratch is rather redundant and undesired, especially when we have some excellent open source alternatives. In Shogun, we prefer 
- [`Eigen3`](http://eigen.tuxfamily.org/index.php?title=Main_Page) for its speed and simplicity at the usage level,
- [`ViennaCL`](http://viennacl.sourceforge.net/) version 1.5 for GPU powered linear algebra operations, and
- [`Lapack`](http://www.netlib.org/lapack/) for its robustness and maturity.

For Shogun maintainers, however, the usage of different external libraries for different operations can lead to a painful task. 

- For example, consider some part of an algorithm originally written using `Eigen3` API. But a Shogun user wishes to use `ViennaCL` for that algorithm instead, hoping to obtain boosted performance utilizing a GPU powered platform. There is _no way_ of doing that without having the algorithm _rewritten_ by the developers using `ViennaCL`, which leads to _duplication_ of code and effort.
- Also, there is no way to do a _performance comparison_ for the developers while using _different_ external linear algebra libraries for the _same_ algorithm in Shogun code.
- It is also somewhat frustrating for a _new_ developer who has to invest significant amount of time and effort to learn each of these external APIs _just_ to add a new algorithm in Shogun.

## Features of internal linear algebra library
Shogun's **internal linear algebra library** (will be referred as `linalg` hereinafter) is a work-in-progress attempt to overcome these issues. We designed `linalg` as a modularized internal **header only** library in order to
- provide a uniform API for Shogun developers to choose any supported backend without having to worry about the syntactical differences in the external libraries' operations,
- handle native Shogun types for linear algebra operations without having to convert to external types,
- have the backend set for each operations at compile-time (for lesser runtime overhead) and therefore intended to be used internally by Shogun developers.

### Using `linalg` operations
The operations can be used in two ways:
#### Relying on globally set `linalg` backend
- Global setup is used whenever an operation **does not specify a particular backend**.
```c++
shogun::linalg::operation(arg1, ...);
```
- Preferred global backend can be specified via `cmake` options which sets that backend for **all** the `linalg` operations used in this fashion.
```bash
# this will set Eigen3 as the global linalg backend for all modules.
# Use -DUSE_VIENNACL for setting ViennaCL as global linalg backend instead
#
cmake -DUSE_EIGEN3
```
[for other cmake options, please refer to the [cmake wiki](README_cmake).]
- Module specific global setups can also be done via `cmake` options. We presently have 2 modules - `Core` and `Redux`.
```bash
# this will set Eigen3 for Redux module's global linalg backend
# and ViennaCL for Core module's global linalg backend.
cmake -DUSE_EIGEN3_REDUX -DUSE_VIENNACL_CORE
```
[see below for a complete list of supported operations under these modules].
- If no particular setup is specified in the `cmake` options, a `DEFAULT` backend is used as a global backend.
- Also, if module specific setup is specified but not for _all_ modules, then for the modules the setup is unspecified, `DEFAULT` backend is used.
[see below for the `DEFAULT` backend settings].
```bash
# this will set ViennaCL for Redux module's global linalg backend
# and Default for the rest of the modules
cmake -DUSE_VIENNACL_REDUX
```
#### Using operation specific `linalg` backend
```c++
shogun::linalg::operation<Backend::backend_name>(arg1, ...);
```
- It is possible to use a specific backend for some particular operation, which then ignores the global or module specific setup and works with that particular backend.
