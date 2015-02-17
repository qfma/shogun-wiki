#Native MS Windows port

*High priority project*, may be part of the [installation project](GSoC_2015_project_installation)

### Mentors
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
**Medium**. You need to be able to:
 - visual c++

### Description
Shogun is missing native MS Windows port. Because of this we are missing a big user base as there's still a lot of researchers and developers who use MS Windows primarily.

Currently the only way to compile Shogun in a MS Windows environment is to use CygWin. Although with the help of CMake one can generate an MS Visual Studio solution file, the code in current state cannot be compiled with Visual C++. I have started to work on this task, but a lot of macros are still required to be able to compile Shogun with VC++.

Although it does not sound like a major task, it is, because one has to take care of all the little things of MS VC++ that makes it a not-so standard C++ compiler.
