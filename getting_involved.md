## Getting involved with Shogun
Welcome to our FAQ on how to get involved with Shogun and Google Summer of Code. While this FAQ is mostly written for GSoC students, it also contains lots of useful tips for getting involved in general.

If you are looking for the project ideas, you will find them [here](Google Summer of Code 2015 projects), last year's projects are [here](http://www.shogun-toolbox.org/page/Events/gsoc2014_ideas). We are looking for you: After our successful participation in the last four GSoC, we want to take Shogun up another notch with your help. So
 * if you are interested in Machine Learning (ML), Statistics, Optimization, or just C++ coding, framework design
 * if you enjoy working with a vibrant team of experienced Machine Learning scientists
 * if you always wanted to join open-source, you should consider spending the summer working with the enthusiastic and open-minded team of developers that are creating one of the largest ML toolboxes out there

Then GSoC is a great program and lots of fun. You can read some blog posts about our past participation [here](GSoC_follow_ups)

## Applicability - “Am I good enough to do this?”
If your answer to this question is “YES!”, then you are the right person ;) The main skill that we are looking for is motivation - we greatly appreciate people who take initiative, come up with creative ideas and are self-organised in making them happen (with our guidance of course). Since Shogun is about ML, most projects are technically involved in some sense: probability distributions, linear algebra, optimization, as well as object-oriented programing, compilers, and git should be things that do not scare you (not too much at least ;) ). However, we do not require you to be a master in the topics that the projects are about, GSoC is also about enjoying learning new things and all of us started from zero.

## First steps - “Shogun seems huge (and messy), where do I start?”
A good (and sometimes already challenging) start into Shogun is to try to install it. In particular, check out the development repository on [github](https://github.com/shogun-toolbox/shogun/tree/develop) and compile/install it in debug mode with a modular interface of your choice (say Python). If you have troubles doing so, have a look at the [wiki](https://github.com/shogun-toolbox/shogun/wiki) and the (documentation files)[https://github.com/shogun-toolbox/shogun/tree/develop/doc]. If you still have trouble, ask us. If you think that your issue might be worth being documented, we greatly appreciate if you then would update the corresponding README (this is what open-source is about). After having installed Shogun, try running the [C++](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/libshogun) and the [modular](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular) examples. You can also try to run the [unit](https://github.com/shogun-toolbox/shogun/tree/develop/tests/unit) and [integration](https://github.com/shogun-toolbox/shogun/tree/develop/tests/integration) tests that we use to keep Shogun working (more on those later). Once everything is set up and working, have a look at our [IPython notebooks](http://www.shogun-toolbox.org/page/documentation/notebook), and maybe try to run them locally. Those contain writeups on last year’s GSoC projects. Pick an example (C++, (python,octave,java)-modular, IPython) of your choice and play with it. You could for example modify the data that is used, or plug in another algorithm. Again, if you have any problems with that, please get back to us, which brings us to the next point.

## Communication - “I don’t want to bother the Shogun developers with my stupid question”
Wrong! Communication is among the most important things in GSoC and in open-source in general. We will not find out what you are doing and what you are able to do, if you don’t tell us. We also don’t bite :) So ask us if you have problems. Let us know in what you are interested and what your ideas are. The best way to get in touch is via IRC, or the mailing list, see [here](http://www.shogun-toolbox.org/page/contact/contacts), there are also nicknames of the core-developers. Most of us live in European timezones. You are also encouraged to help out other students if you know something that they don’t.

## Projects - “All those projects sound hard-core, what should I choose?”
If you cannot make up your mind, try to ask yourself what you would find most interesting and what matches your skills best. Are you more into mathematical ML or into C++ coding, do you want to implement bleeding edge algorithms or write nice examples for established ones? We are trying to offer a wide range of projects that are suitable for many backgrounds. There are even a few purely software-engineering type ones. While we are open for your own project suggestions, that is usually hard in practice since we need a mentor (who we know). Having said that, we are very open to suggestions or extensions on existing projects. In fact, if you make the description more concrete in terms of what to do exactly, or even write a prototype, this will be a big plus for your application. Speaking of application

## Your application - “How do I convince the Shogun people of myself”
As already mentioned above, you have to commit us of your excitement about Shogun and your selected project. Apart from talking to us directly, the best way to do so is to contribute to Shogun before the student application deadline. In fact, we will not consider application from people who did not send us any code. The higher quality work, the better for your application. We have a number of [issues on our github tracker](https://github.com/shogun-toolbox/shogun/issues), where we collect bugs, problems, and in particular GSoC entrance tasks. The latter are small programming tasks that are meant to be a fun introduction to Shogun while being useful for the GSoC project or Shogun in general. There are both projects related and general ones, some of which are open-ended and some of them are very concrete. If you come up with other things, that is also highly appreciated. For example, writing new notebooks, examples, or documentation is a great way to contribute, as well as fixing bugs (which is a bit harder usually). For the application itself, try to tell a nice story why you are the best candidate. We usually get around 50-100 proposals while being able to offer 5-8 slots, so be aware of competition.

##Commitment - “How much time do I really need to spend on GSoC”
GSoC is a fulltime job (40h/week)! While it is not important where you work, we expect students to hand in code every week at least, so you should work on your project continuously. We also encourage you to stick around in IRC in order to help each other, get involved with the community, and to share the fun. In addition, preparing the GSoC requires quite a bit of time and effort: preparing your application, get involved in Shogun development before the deadline, reading about project details etc.

### Our Expectation - “What you have to deliver”
All code that you write is directly merged into our development branch as we want to avoid you building a separate branch that nobody else sees. This means you will get feedback for every pull request you send us - lots of room for discussion! New code might break existing unit/integration tests. This is checked via [travis](https://travis-ci.org/shogun-toolbox/shogun), which is a web-service that checks your pull request for C++ compile errors and broken unit tests before merging, and our [buildbot farm](http://buildbot.shogun-toolbox.org/waterfall), which, after merging, compiles Shogun under a large variety of configurations and operating systems, and finally runs every test. We expect you to keep our tests green. We expect you to provide unit tests for all the code you write. We also expect you to write C++ and python_modular (aka integration test) mini-examples that demonstrate the API.

In addition, a big part of every GSoC project with us is a final report in the form of an IPython notebook, have a look at the previous ones at. Plan the final two weeks as time to write this notebook - it is the most visible part of your project and therefore it should receive a lot of love. Finally, we plan a peer-review from our students at the end of GSoC. That means you will review one other student’s code with respect to (interface) documentation, usability, and bugs - and he/she will do the same with your work. In the optimal case, you write an example or notebook extension for each other.

As we are aiming to change our license model from GPL to BSD sytle license, we will require all code to be submitted under this new model.

### Shogun development cycle in a nutshell - “How to get my code into Shogun”
Here is a very basic list of things how to get started hacking Shogun. It requires some basic knowledge about Git(Hub), for which you can easily find help online.

1. Register on GitHub.
2. Fork the shogun repository.
3. Clone your fork locally, add the orignal (our) repository as upstream (in order to rebase your clone). Create a develop branch locally and rebase it against the upstream. For example using git pull --rebase upstream develop.
4. Create a new feature branch locally, work (and commit your work) in there. When done, merge this (possibly with the squash option) to your local develop branch. If you want, use [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/) (search in the [archives of our mailing list](http://blog.gmane.org/gmane.comp.ai.machine-learning.shogun) for more information about how we are using Git flow).
5. Push the changes to your fork on github.
6. Send a pull request against the development branch of the original Shogun repository.
7. We hope you did not forget to write a unit test for your changes (or tell us why there is no need).
8. Every pull request will trigger travis to compile and run tests on your branch, see [travis](https://travis-ci.org/shogun-toolbox/shogun). If those are all green, someone of the core-developers will merge after giving feedback. Feedback usually takes a few iterations of you changing things and us commenting in the beginning.
9. Goto 4.

### Useful ressoruces
 * [Develop branch](https://github.com/shogun-toolbox/shogun/tree/develop)
 * [Markdown doc files]([https://github.com/shogun-toolbox/shogun/tree/develop/doc])
 * [C++ examples (aka libshogun examples)]((https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/libshogun))
 * [Python modular examples](https://github.com/shogun-toolbox/shogun/tree/develop/examples/undocumented/python_modular))
 * [Unit tests](https://github.com/shogun-toolbox/shogun/tree/develop/tests/unit)
 * [Integration tests](https://github.com/shogun-toolbox/shogun/tree/develop/tests/integration)
 * [IPython notebooks](http://www.shogun-toolbox.org/page/documentation/notebook)
 * [Contacts](http://www.shogun-toolbox.org/page/contact/contacts)
 * [GitHub issues tracker](https://github.com/shogun-toolbox/shogun/issues)
 * [Shogun in Travis](https://travis-ci.org/shogun-toolbox/shogun)
 * [Buildbots](http://buildbot.shogun-toolbox.org/waterfall)
 * [Git Flow](http://nvie.com/posts/a-successful-git-branching-model/)
 * [Previous GSoC blog posts](GSoC-follow-up-blog-posts)
 * [Mailing list archives](http://blog.gmane.org/gmane.comp.ai.machine-learning.shogun)