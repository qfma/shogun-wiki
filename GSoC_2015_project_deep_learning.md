# Hip Deep learning

Taking [last year's project](https://www.google-melange.com/gsoc/project/details/google/gsoc2014/khalednasr92/5657382461898752) to a new level.

### Mentors
 * Theofanis Karaletsos
 * Sergey (github: [lisitsyn](https://github.com/lisitsyn), IRC: lisitsyn)

### Difficulty & Requirements

Pretty difficult. Requires:

 * C++ programming
 * Understanding what neural nets are and how do we learn them
 * OpenCL programming is a plus 
 * Understanding Of inference in graphical models, variational inference is a plus
 * Experience with Stochastic Optimization is a plus

### Description

Last year we had an introductory project completed by Khaled Nasr on deep learning which introduced most essential components to use neural networks with Shogun. This project considers extending and improving things we already have with some cutting edge algorithms.

### Details

### Waypoints and initial work

* First of all, you'd have to dive into the existing goods. We believe the easiest way to do that is to improve the code through small iterative changes that improve code quality
* Training neural nets with CPU only is really slow and we're actually pretty near to have GPU training in Shogun so the next step is to finish up GPU training and finally train some deep net with a GPU


### Optional

* We expect this project to consider active research problems so probably you can even come up with something really-really new!

### Why this is cool
Deep learning is *everywhere* - it is on the bleeding edge of research. 
Most importantly, in recent attempts deep learning is getting the benefit of a bayesian treatment and the goal of this project is to marry deep nets and variational inference in the spirit of Reverend Bayes.

### Papers
- [Auto-Encoding Variational Bayes](http://arxiv.org/abs/1312.6114) by Kingma and Welling
- [Stochastic Backpropagation and Approximate Inference in Deep Generative Models](http://arxiv.org/abs/1401.4082) by Rezende et al
- [Neural Variational Inference and Learning in Belief Networks](http://arxiv.org/abs/1402.0030) by Mnih and Gregor
- [Deep Exponential Families](http://arxiv.org/abs/1411.2581) by Ranganath, Blei et al

### Useful resources

- "Neural Networks for Machine Learning" by Geoffrey Hinton (https://www.coursera.org/course/neuralnets) 
- "Deep learning" by Yoshua Bengio, Ian Goodfellow and Aaron Courville (http://www.iro.umontreal.ca/~bengioy/dlbook/) 

### Entrance level tasks

- [Implement new initializations for neural nets as per MSR paper](https://github.com/shogun-toolbox/shogun/issues/2700)
- [~~Add leaky ReLU neural layer~~](https://github.com/shogun-toolbox/shogun/issues/2699)
- [Reproduce "Text understanding from scratch" neural model with a notebook](https://github.com/shogun-toolbox/shogun/issues/2701)
- [Support DotFeatures in neural networks](https://github.com/shogun-toolbox/shogun/issues/2709)
- [Add preprocessor layer for neural network](https://github.com/shogun-toolbox/shogun/issues/2710)