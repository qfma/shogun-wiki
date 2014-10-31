This is a rough sketch of things to do to get a more slim and easier maintainable Shogun. Every item has dependencies that need to be done first. Starting from leafs of this tree, we have an action list.

 * Drop Parameter framework
  * Drop Model-selection framework and/or move inside Shogun modules
   * Drop GP-model selection (quite feasible)
   * Drop SVM model selection, not necessary, see [here](https://github.com/shogun-toolbox/shogun/issues/1251)
  * Drop Serialisation.
   * Drop integration tests
    * Clean up Shogun's testing framework
     * modular examples should only be exectuted, algorithms tested within c++
     * Test SWIG typemaps, only need to test them since algos tested as above
     * Turn all hand-crafted integration tests into c++ tests (unit or something else), unless we loose test coverage

    