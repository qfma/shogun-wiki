#Shogun cloud extensions

### Mentors
 * [Viktor Gal](http://maeth.com/) (github: [vigsterkr](https://github.com/vigsterkr), IRC: wiking)

### Difficulty & Requirements
**Medium**. You need to be able to:
 - distributed computing
 - python
 - docker


### Description
Cloud service of Shogun was introduced with release 3.0. It is basically a simple Flask application that serves docker containers with Shogun and python modular interface with IPython server in it for the users. The code is available here.
There are several issue (extensions) one would need to solve during this task:
  * auto-update docker containers of the users to the latest shogun docker image
  * tunnel using session keys the IPython notebook via the http server instead of revealing the service directly.
  * create a frontend-backend setup, where the front-end node is only responsible for authenticating and registering the users and to optimally allocate resources among the back-end servers who are responsible to run the docker containers.