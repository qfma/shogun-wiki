See also [here](https://github.com/shogun-toolbox/shogun/wiki/SWIG-issues)

## How SWIG works
Shogun exposes its modular interfaces via SWIG (activated via cmake). SWIG reads a bunch of interface files, located in ```shogun/src/interfaces/modular/*.i```, which contain a list of classes to expose to the modular interfaces (and options and technical things).

Roughly speaking, SWIG scans all *header* files of the to be exposed classes, and for every class/method in those, generates some code that is all put into a c++ file. This file is located in ```src/interfaces/python_modular/modshogunPYTHON_wrap.cxx``` (Python version) and is gets quite big. This happens because *all* methods of the classes in the interface files are cause SWIG to generate some code in there. Even more crazy, all templated classes are instantiated with all possible template parameters: ```SGVector<float64_t>``` aka ```RealVector```, ```SGVector<float32_t>``` aka ```ShortRealVector```, and so on.

The file is eventually compiled with the c++ compiler and produces the ```modshogun.py``` (Python) that contains the interface for the modular target language. Note that the compilation process requires quite some memory (2GiB currently, Oct 2014).

SWIG also contains a bunch of typemaps: Those are responsible for mapping memory from say a Shogun ```SGVector``` to a ```numpy.ndarray```, etc. All signatures can be used with the target language types. Great!

## Two public interfaces: SWIG and C++
In order to avoid the SWIG output to explode, we want to minimise the number of methods being exposed in SWIG. There are two types of public interfaces in Shogun:
 * Public c++ methods
 * SWIG methods (subset of the above)

Note that there are methods that belong to the first but *not* the second type. For example helper methods that need to be called from another c++ class, but are usually not called from within the modular interface. A Python example is 
```
fname='fm.csv'
feats=RealFeatures(CSVFile(fname))
```
Here, ```CSVFile(fname)``` is an instance of ```CSVFile```, whose c++ interface implements a bunch of methods to access individual vectors, e.g.,
```virtual void get_vector(float64_t*& vector, int32_t& len);```
in ```CSVFile```. However, those methods should not be exposed in Python as SWIG's output gets too large and users actually do not need those methods -- they just want to pass the instance of ```CSVFile``` to another class (```RealFeatures``` here), which then calls the ```get_vector``` methods to load data.




