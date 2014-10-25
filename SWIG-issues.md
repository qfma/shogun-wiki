##  SWIG
Compiling modular interfaces more and more gets a problem. Both compile time and memory requirements explode with more classes added to Shogun. We already sometimes hit the memory limit of travis, which results in unfinished (gray) builds, for example [this one](https://github.com/shogun-toolbox/shogun/issues/2562).

Furthermore, the SWIG magic might be very interesting for other projects, so it could be a good idea to pull it out from the Shogun source tree into a seperate mini-project.

## Why SWIG is big
Every method in Shogun's header files that are included in the ```modular.i``` generates a couple of lines in the SWIG output. In particular, templated methods are expensive as they are instantiated for all basic data-types in Shogun. The way to solve this therefore must be to reduce the number of methods exposed to SWIG. [Here](https://github.com/shogun-toolbox/shogun/issues/2562) is the top 10 list of classes with most methods exposed to the modular interfaces.

## D-pointer-like ideas and why they do *not* help
In an optimal world, there is a class that *only* represents the interface to modular interfaces, i.e. how Shogun is used from outside C++. This class in its .cpp file then might call methods of an implementation helper class. See for example the [LMNN](http://www.shogun-toolbox.org/doc/en/latest/LMNN_8cpp_source.html) class, which uses a helper class in its implementation that contains a bunch of helper methods.

This is closely related to D-pointers. We investigated this and concluded that it will not help us.  SWIG only touches public methods. As all helper methods that would go into an implementation class can just be made protected, this problem can easily be solved. 

The other problem with this approach is that there are C++ methods that *need* to be public, but should *not* be in SWIG. The only solution for those is explicitly ignore them (see below). Creating separate interface classes just for SWIG will not help as instances of them need to be passed around in the modular interfaces, and these instances need to implement certain interfaces on a C++ level. Let's clarify this through an example. Consider the following code from the Python modular interface:

```
fname='fm.csv'
feats=RealFeatures(CSVFile(fname))
```

The class `CSVFile` implements a bunch of methods to read data from disk, e.g. `get_vector(float*& vector, int& len)`. This method needs to be public to be accessible from feature classes (such as RealFeatures). However, it does not need to be accessible at all from the modular interfaces provided by SWIG. Therefore, it must be a public method of `CSVFile`, but we don't want SWIG to generate any bindings for it.

## What helps?
Here are two suggestions. The first one can be applied to *any* of the classes that blow up SWIG's output, the second involves clean-ups that might need a bit more thought, but are cleaner solutions.

### SWIG's ```%ignore``` and ```#ifndef SWIG // SWIG should skip this``` guards
There are a number of public methods that *have* to be public (for example the ```CLibSVMFile::get_vector*``` methods that are called from other C++ classes), but that we do not want to expose to SWIG. These can be explicitly ignored.

## Clean up ```SGVector``` and similar
All ```SG*``` classes are primarily meant for data exchange with Shogun's interfaces (in particular modular interfaces). As such, they are only meant to represent data, not offer operations on those (apart from fundamental access such as ```[]``` operators and similar). However, currently, those classes contain lots of algrothmic code, see for example [here](http://www.shogun-toolbox.org/doc/en/latest/classshogun_1_1SGVector.html): ```range_fill, abs, permute```, etc.
Every of those methods will result in a wrapper method in SWIG, for *every* of the template arguments. All such methods should be moved into ```CMath, CStatistics, linalg```, or similar. This way, SWIG produces less code, and separation of concerns is respected: These objects are just there for passing data through Shogun's internal and external interfaces.


## Examples and their impact
### SWIG's %ignore
Adding in ```LibSVMFile.h```
```
#ifdef SWIG // Methods to hide from SWIG
%ignore get_vector;
%ignore get_matrix;
%ignore get_ndarray;
%ignore get_sparse_matrix;
%ignore get_string_list;
%ignore get_sparse_matrix;

%ignore set_vector;
%ignore set_matrix;
%ignore set_ndarray;
%ignore set_sparse_matrix;
%ignore set_string_list;
%ignore set_sparse_matrix;
#endif
```
and compiling reduces the number of lines in ```modshogunPYTHON_wrap.cxx``` by roughly 20k.
In particular:
```
$ cat src/interfaces/python_modular/modshogunPYTHON_wrap.cxx |  grep get_vector | grep LibSVMFile
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_0(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int8_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int8_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_1(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint8_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint8_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_2(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "char *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "char *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_3(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int32_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int32_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_4(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint32_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint32_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_5(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "float64_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "float64_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_6(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "float32_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "float32_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_7(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "floatmax_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "floatmax_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_8(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int16_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int16_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_9(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint16_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint16_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_10(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int64_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "int64_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector__SWIG_11(PyObject *self, PyObject *args) {
  if(!PyArg_UnpackTuple(args,(char *)"LibSVMFile_get_vector",2,2,&obj1,&obj2)) SWIG_fail;
    SWIG_exception_fail(SWIG_ArgError(res1), "in method '" "LibSVMFile_get_vector" "', argument " "1"" of type '" "shogun::CLibSVMFile *""'"); 
    SWIG_exception_fail(SWIG_ArgError(res2), "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint64_t *&""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "2"" of type '" "uint64_t *&""'"); 
    SWIG_exception_fail(SWIG_ArgError(res3), "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
    SWIG_exception_fail(SWIG_ValueError, "invalid null reference " "in method '" "LibSVMFile_get_vector" "', argument " "3"" of type '" "int32_t &""'"); 
SWIGINTERN PyObject *_wrap_LibSVMFile_get_vector(PyObject *self, PyObject *args) {
          return _wrap_LibSVMFile_get_vector__SWIG_0(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_1(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_2(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_3(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_4(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_5(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_6(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_7(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_8(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_9(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_10(self, args);
          return _wrap_LibSVMFile_get_vector__SWIG_11(self, args);
  SWIG_SetErrorMsg(PyExc_NotImplementedError,"Wrong number or type of arguments for overloaded function 'LibSVMFile_get_vector'.\n"
    "    shogun::CLibSVMFile::get_vector(int8_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(uint8_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(char *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(int32_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(uint32_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(float64_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(float32_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(floatmax_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(int16_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(uint16_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(int64_t *&,int32_t &)\n"
    "    shogun::CLibSVMFile::get_vector(uint64_t *&,int32_t &)\n");
  { "get_vector", (PyCFunction) _wrap_LibSVMFile_get_vector, METH_VARARGS, (char*) "\n"

```
Doing the same command when the ```%ignore``` are added leaves the output empty.
*Note:* I believe that these SWIG ignores should *not* be in a separate file (currently ```modshogun_ignores```). It's way harder to maintain. Doing those in the interface classes makes it very easy to get a feeling for where its forgotten, etc.