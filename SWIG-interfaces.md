See also [here](https://github.com/shogun-toolbox/shogun/wiki/SWIG-issues)

## How SWIG works
Shogun exposes its modular interfaces via SWIG (activated via cmake). SWIG reads a bunch of interface files, located in ```shogun/src/interfaces/modular/*.i```, which contain a list of classes to expose to the modular interfaces (and options and technical things).

Roughly speaking, SWIG scans all *header* files of the to be exposed classes, and for every *public* class/method in those, generates some code that is all put into a C++ file. This file is located in ```src/interfaces/python_modular/modshogunPYTHON_wrap.cxx``` (Python version) and is gets quite big. This happens because *all* methods of the classes in the interface files are cause SWIG to generate some code in there. Even more crazy, all templated classes are instantiated with all possible template parameters: ```SGVector<float64_t>``` aka ```RealVector```, ```SGVector<float32_t>``` aka ```ShortRealVector```, and so on.

The file is eventually compiled with the C++ compiler and produces the ```modshogun.py``` (Python) that contains the interface for the modular target language. Note that the compilation process requires quite some memory (2GiB currently, Oct 2014).

SWIG also contains a bunch of typemaps: Those are responsible for mapping memory from say a Shogun ```SGVector``` to a ```numpy.ndarray```, etc. All signatures can be used with the target language types. Great!

## Two public interfaces: SWIG and C++
In order to avoid the SWIG output to explode, we want to minimise the number of methods being exposed in SWIG. There are two types of public interfaces in Shogun:
 * Public C++ methods
 * SWIG methods (subset of the above)

Note that there are methods that belong to the first but *not* the second type. For example helper methods that need to be called from another C++ class, but are usually not called from within the modular interface. A Python example is 
```
fname='fm.csv'
feats=RealFeatures(CSVFile(fname))
```
Here, ```CSVFile(fname)``` is an instance of ```CSVFile```, whose C++ interface implements a bunch of methods to access individual vectors, e.g.,

```virtual void get_vector(float64_t*& vector, int32_t& len);```

in ```CSVFile```. However, those methods should not be exposed in Python as SWIG's output gets too large (method exists for *every* type) and users actually do not need those methods -- they just want to pass the instance of ```CSVFile``` to another class (```RealFeatures``` here), which then calls the ```get_vector``` methods to load data.

## How to do this
 * Write Shogun C++ interface
   * *Only* includes from ```<shogun/*>``` are allowed in header files, no external ones
   * Public methods can only contain Shogun data-types
     * Allowed: ```SGVector, float64_t, CSGObject```
     * *Not* allowed: Eigen3, STL, etc
   * Make all helper methods protected/private (SWIG ignores them then)
     * This also means that one can use non-Shogun types in them (only forward declared)

Finally: For helper methods that need cannot be private (as called by other classes), one can do
```
public:
#ifndef SWIG //SWIG should ignore this
     SGVector<T> public_method_to_ignore();
#endif // #ifndef SWIG //SWIG should ignore this
```
This will cause SWIG to ignore the method in between. It will not be available in the modular interfaces (and though not appear in the C++ file that SWIG outputs). Note that the ```SWIG``` flag is true if and only if SWIG scans the header files. That is why the above code leaves only hides the method when SWIG scans the file. C++ itself will see it.

Alternatively, one can do
```
#ifdef SWIG
%ignore public_method_to_ignore;
#endif // #ifdef SWIG
```
The first option is clearly better as no pattern/type/signature matching has to be done.

Shogun also has a blacklist where we used to add methods to ignore: 
```shogun/src/interfaces/modular/modshogun.i```

This file is very hard to maintain, and is therefore *not* recommended to use. Excluding methods from SWIG in the C++ interface file puts both of Shogun's public interfaces (as listed above) in one place and therefore allows to easily get an overview.

## Summary
When writing a new Shogun class
 * Think about the interface
 * Don't include any non-Shogun objects in there
 * Try to make all helper methods private/protected to hide them from SWIG
 * For helper methods that cannot be private (as need to be called by other classes), mark them to be ignored by SWIG.

World domination.


