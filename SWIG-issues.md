##  SWIG
Compiling modular interfaces more and more gets a problem. Both compile time and memory requirements explode with more classes added to Shogun. We already sometimes hit the memory limit of travis, which results in unfinished (gray) builds, for example [this one](https://travis-ci.org/shogun-toolbox/shogun/jobs/38982676)

Furthermore, the SWIG magic might be very interesting for other projects, so it could be a good idea to pull it out from the Shogun source tree into a seperate mini-project.

## Top 100 classes in SWIG's output
Thoralf made [this list](https://github.com/shogun-toolbox/shogun/issues/2562) of how much impact all classes have in SWIG's output

## Clean up ```SGVector``` and similar
All ```SG*``` classes are primarily meant for data exchange with Shogun's interfaces (in particular modular interfaces). As such, they are only meant to represent data, not offer operations on those (apart from fundamental access such as ```[]``` operators and similar. However, currently, those classes contain lots of algrothmic code, see for example [here](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1SGVector.html): ```range_fill, abs, permute```, etc.
Every of those methods will result in a wrapper method in SWIG, for *every* of the template arguments. This is likely to be one reason why SWIG grew to big. All such methods should be moved into ```CMath, CStatistics, linalg```, or similar. This way, SWIG produces less code, and separation of concerns is respected: These objects are just there for passing data through Shogun's internal and external interfaces.

## Wrapper/Impl classes?
In order to further minimise the code that SWIG touches or generates, we have to think about a way to hide things from it. In an optimal world, there is a class that *only* represents the interface to modular interfaces, i.e. how Shogun is used from outside C++. This class in its .cpp file then might call methods of an implementation helper class. See for example the [LMNN](http://www.shogun-toolbox.org/doc/en/latest/LMNN_8cpp_source.html) class, which uses a helper class in its implementation that contains a bunch of helper methods.

Another way to get the same functionality is to make all methods that should not go into SWIG private. However, the issue here might be that developers might need to have certain public methods (to be called from other classes), which however should not go into SWIG.

One solution here could be to move all helper methods into implementation classes that are not visible in header files.