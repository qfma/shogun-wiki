This is a rough sketch of things to do to get a more slim and easier maintainable Shogun. Every item has dependencies that need to be done first. Starting from leafs of this tree, we have an action list.

## Reduce Shogun's base class overhead
 * Drop Parameter framework
  * Drop Model-selection framework and/or move inside Shogun modules
   * Drop GP-model selection (quite feasible)
   * Drop Grid-search model selection, not necessary, see [here](https://github.com/shogun-toolbox/shogun/issues/1251)
  * Drop Serialisation.
   * Drop non-c++ integration tests
     * Clean up Shogun's testing framework
      * There are currently two sets of integration tests from python (```tester.py``` and ```test_one.py```).
      * Modular examples should only be executed, algorithms tested within c++
      * Test SWIG typemaps, only need to test them since algos tested as above
      * Turn all hand-crafted integration tests into c++ tests (unit or something else), unless we loose test coverage
        * Add c++ integration testing framework based on googletest

## Reduce Shogun's build complexity
 * Drop static interfaces
  * Make Matlab work from SWIG
  * Port all static integration tests to c++
 * Build-folder should be the only thing modified by CMake. Get rid of other hacks.
    