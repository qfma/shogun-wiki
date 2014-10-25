##  SWIG
Compiling modular interfaces more and more gets a problem. Both compile time and memory requirements explode with more classes added to Shogun. We already sometimes hit the memory limit of travis, which results in unfinished (gray) builds, for example [this one](https://github.com/shogun-toolbox/shogun/issues/2562)

Furthermore, the SWIG magic might be very interesting for other projects, so it could be a good idea to pull it out from the Shogun source tree into a seperate mini-project.

## Why SWIG is big
Every method in Shogun's header files that are included in the ```modular.i``` generates a couple of lines in the SWIG output. In particular expensive are templated methods as they are instantiated for all basic data-types in Shogun. The way to solve this therefore must be to reduce the number of methods exposed to SWIG. [Here](https://github.com/shogun-toolbox/shogun/issues/2562) is the top 100 list. There are a couple of ways to address this

## D-pointer-like ideas and why they do *not* help
In an optimal world, there is a class that *only* represents the interface to modular interfaces, i.e. how Shogun is used from outside C++. This class in its .cpp file then might call methods of an implementation helper class. See for example the [LMNN](http://www.shogun-toolbox.org/doc/en/latest/LMNN_8cpp_source.html) class, which uses a helper class in its implementation that contains a bunch of helper methods.

This is closely related to D-pointers. We investigated this and concluded that it will not help us.  SWIG only touches public methods. As all helper methods that would go into an implementation class can just be made protected, this problem can easily be solved. 

The other problem with this approach is that there are C++ methods that *need* to be public, but should *not* be in SWIG. The only solution for those is explicitly ignore them (see below). Creating seperate interface classes just for SWIG will not help as instance of them need to be passed around in the modular interfaces, and these instance need to implement certain interfaces on a c++ level.

## What helps?
Here are two suggestions. The first one can be applied to *any* of the classes that blow up SWIG's output, the second involves clean-ups that might need a bit more thought, but are cleaner solutions.

### SWIG's ```%ignore```
 2) There are a number of public methods that *have* to be public (for example the ```CLibSVMFile::get_vector*``` methods that are called from other c++ classes), but that we don not want to expose to SWIG. These can be explicitly ignored. Applies to all cases.

## Clean up ```SGVector``` and similar
All ```SG*``` classes are primarily meant for data exchange with Shogun's interfaces (in particular modular interfaces). As such, they are only meant to represent data, not offer operations on those (apart from fundamental access such as ```[]``` operators and similar. However, currently, those classes contain lots of algrothmic code, see for example [here](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1SGVector.html): ```range_fill, abs, permute```, etc.
Every of those methods will result in a wrapper method in SWIG, for *every* of the template arguments. All such methods should be moved into ```CMath, CStatistics, linalg```, or similar. This way, SWIG produces less code, and separation of concerns is respected: These objects are just there for passing data through Shogun's internal and external interfaces.
