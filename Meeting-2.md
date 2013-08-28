**date**: August 27, 2013

[IRC Logs](http://shogun-toolbox.org/page/contact/irclog/2013-08-27/#t10:24)

1. Preparations for the next (post-GSoC) Shogun release, version 3.0
  * all the required tasks that we've discussed during the meeting are added to the [Shogun 3.0](https://github.com/shogun-toolbox/shogun/issues?milestone=3&state=open) milestone
  * fixing the remaining issues with buildbots, e.g. static interfaces, cygwin etc see issue: [#1401](https://github.com/shogun-toolbox/shogun/issues/1401) [#1402](https://github.com/shogun-toolbox/shogun/issues/1402) [#1411](https://github.com/shogun-toolbox/shogun/issues/1411) [#1415](https://github.com/shogun-toolbox/shogun/issues/1415) [#1416](https://github.com/shogun-toolbox/shogun/issues/1416) [#1479](https://github.com/shogun-toolbox/shogun/issues/1479) 
  * fix CPACK scripts for creating tar.gz and .deb, .rpm and .mpkg packages [#1488](https://github.com/shogun-toolbox/shogun/issues/1488) [#1487](https://github.com/shogun-toolbox/shogun/issues/1487) [#775](https://github.com/shogun-toolbox/shogun/issues/775) [#353](https://github.com/shogun-toolbox/shogun/issues/353)
  * create a page on our site where we will upload the nightly built packages [#1481](https://github.com/shogun-toolbox/shogun/issues/1481) 
  * start generating and uploading nightly ipython notebooks as well integrate it into the webpage [#1482](https://github.com/shogun-toolbox/shogun/issues/1482) @sonney2k, @wiking, @iglesiasg
  * slowly start pushing (gsoc) commiters to fix their buildbot warnings 
  * live demos integration into the webpage [#1483](https://github.com/shogun-toolbox/shogun/issues/1483)
  * check how we could autotest demos [#1484](https://github.com/shogun-toolbox/shogun/issues/1484)
  * restructure NEWS, INSTALL, README [#1471](https://github.com/shogun-toolbox/shogun/issues/1471) [#1386](https://github.com/shogun-toolbox/shogun/issues/1386)
  * update http://shogun-toolbox.org/page/about/information [#1485](https://github.com/shogun-toolbox/shogun/issues/1485)

2. Serialisation framework
  * fix the remaining issues in feature/SerialUTests branch and merge it [#1464](https://github.com/shogun-toolbox/shogun/issues/1464). Basically JSON does not support NaN or INF. Solution: just SG_ERROR in JSON writer if it is about to write out INF or NaN.
  * add a more precise JSON back-end like msgpack @wiking

3. Integration tests
  * see the discussion at issue [#1253](https://github.com/shogun-toolbox/shogun/issues/1253)

4. Application to NIPS workshop
  * **deadline**: october 9
  * @Heiko organizing the whole application, possibly going and present it as well

5. auto generate obtain_from_generic function for all classes
  * see issue [#1348](https://github.com/shogun-toolbox/shogun/issues/1348) @wiking

6. Sergey's idea about auto setter/getter
  * Sergey is going to create a feature branch. More info and discussion at [#1265](https://github.com/shogun-toolbox/shogun/issues/1265)
