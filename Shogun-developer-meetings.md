# Meeting 1, August 8, 2013
IRC Logs http://shogun-toolbox.org/irclogs/%23shogun.2013-08-08.log.html#t22:01

1. Developer meeting organization
   * Every month
   * Take turns in organization. Organization involves setting up doodle, set up topics, lead meeting and write this documentation afterwards
   * Next one: @wiking

2. Doc-Sprint application
   * @karlnapf wrote a draft, everyone should read and tune unit **tomorrow**
   * Try to be less mathy, more general this time

3. CMake
   * Now merged, usable
   * @lisitsyn will update the README so that everyone know how to do things
   * Debian packages still need some hacking
   * @wiking is great

4. Shogun foundation
   * @sonney2k sends Heiko the list with signatures
   * @HeikoS will write a protocol of the founding process
   * @iglesias will set up a voting for the leader once Heiko collected all adresses
   * @sonney2k will take everything and bring it to a Notar in Germany

# Meeting 2, August 27, 2013

1. Preparations for the next (post-GSoC) Shogun release
  * fixing the remaining issues with buildbots, e.g. static interfaces, cygwin etc
  * fix CPACK scripts for creating tar.gz and .deb, .rpm and .mpkg packages
  * create a page on our site where we will upload the nightly built packages
  * start generating and uploading nightly ipython notebooks

2. Serialisation framework
  * fix the remaining issues in feature/SerialUTests branch and merge it
  * add a more precise JSON back-end like msgpack

3. Integration tests
  * see the discussion at issue #1253
