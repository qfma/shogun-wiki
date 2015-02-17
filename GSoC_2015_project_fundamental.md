# Fundamental Machine Learning Algorithms, Part 2
**Linear Latent Gaussian Models: Linear and non-linear output**
Project proposed by [Heiko](Heiko%20Strathmann) & [Alessandro](https://github.com/ialong)


### Mentors
 * [Fernando](Fernando%20Iglesias) (github: [iglesias](https://github.com/iglesias), IRC iglesias)
 * [Heiko](Heiko%20Strathmann) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)
 * [Lars Buesing](http://www.gatsby.ucl.ac.uk/~lars/) ?

### Difficulty & Requirements
Easy/medium/advanced.
You need:
 * C++ coding
 * Gaussians
 * Kalman filter
 * EM algorithm
 * Variational & EP approximations

### Description
A number of fundamental Machine Learning models and algorithms will be implemented as part of this project. The focus is on latent linear models, namely ones comprising a set of latent variables which have a linear relation among themselves and/or the observed variables. In their simplest form (PPCA and Factor Analysis) these models represent the observed variables as a noisy linear transformation of the marginally independent latents. If we apply this sort of structure to time-series analysis, the most essential model (the Linear Gaussian State Space Model) features a "chain" of latent variables encoding the linear-Gaussian evolution of the system. At each time-step, an observation is generated as a linear transformation of the latent variable plus Gaussian noise. 
In this setting, inference on the latent variables is exact and learning can be carried out effectively (through EM or spectral methods). However, if we relax the assumption of Gaussianity of the output noise and take the observed variables to be generated according to a Generalized Linear Model (GLM), parameterized by a linear transformation of the latents, inference becomes intractable. We gain greatly, though, in terms of the expressiveness of the model as we can now describe data-points following all sorts of distributions (especially exponential family ones, using canonical link functions). Hence, in this case, we would like to apply various approximation methods to exploit this powerful model.
 
Overall, the following should be implemented.

 **Models:**
 * PPCA
 * Factor Analysis
 * Linear Gaussian State Space Model (LGSSM)
 * Generalised Linear Output State Space Model (with linear Gaussian latent dynamics)

 **Algorithms:**
 * Expectation Maximization (as a general framework, for both the exact and the approximate setting)
 * (Kalman) Filtering
 * (Kalman) Smoothing
 * Spectral/SSID Methods (Ho-Kalman and non-linear Ho-Kalman [5]) 
 * Approximate inference:
   * Variational Inference
   * Expectation Propagation
 * Gradient/Optimization methods for likelihood ascent and Variational inference (e.g.[1]) 

Given the number of closely related variations of these models and algorithms, the project should put special care in building a clean framework of core classes, where specific or more complex cases (i.e. approximations and generalizations) can be easily implemented by extending a simpler structure. 

A first outline of the core classes might be:
 * Likelihood function
 * Inference/Learning routines
 * Expectation/Maximization steps
 * Matrices and quantities used in spectral analysis
 * State Space Model (general enough to be implemented both as LGSSM and Generalised Linear SSM)
 * Filtering recursion
 * Smoothing/forward-backward/message-passing recursions
 * Variational framework (with various optimization methods)
 * Convergence/Eigenvalue/Positive-Definiteness tests
 * Evaluation metrics for learned parameters (dynamics and output loading matrices), especially: subspace angles, eigenvalue/eigenvector comparison

Clear, explanatory IPython notebooks should be produced for the main algorithms by way of documentation and tutorial.


(Models: State space dynamics are linear Gaussian
Observation links might be Gaussian but can also be non-linear.
Both learning and inference.

Models:
 * LGSSM
   * Kalman filter for inference
   * EM for learning
   * HO-Kalman for fast EM learning
 * Non-linear GSSM: Let's focus on exp-family link functions
   * Inference: variational, EP for the E-step
   * Learning: variational EM, See BÃ¼sing & Macke "Non-linear Kalman"

Other ideas:
 * Use existing EM framework for the variational apprixmate methods
 * Could be that we need to change it, maybe even another iteration on GMMs
 * HMM re-implementation. Viterbi, Baum Welch, all neat and clean? Notebook?
 * Other Linear Gaussian models: FA, PPCA, also work with the above algorihtms (EM, gradient descent)
 * ARD for LGMs. Prior on columns of projection matrix, compute posterior)


### Details
Write about details of the project here.

### Waypoints and initial work
 * More Random forests (BART)
 * Please put your ideas here

### Optional
 * Attempt other approximations for inference (e.g. Laplace approximation)
 * Implement the Extended Kalman Filter (widely used for navigation/GPS systems) [2]
 * Implement the Recurrent Linear Model (a reformulation of the Kalman Filter that can be used for learning, not just inference) [3]

### Why this is cool
State Space Models are simple yet powerful tools. They can be used in essentially any field involving data with a temporal evolution and, especially in the linear-Gaussian case, have been employed in anything from Neuroscience to Ballistics. 
This project is a great chance to implement these models in C++ with a special attention to efficiency and to building up a clear, general framework for all their variations and related methods. It will cover both inference and learning, thus ranging over a considerable, and fundamental, part of statistical Machine Learning with the potential of being used by a great number of scientists in very exciting interdisciplinary settings.
For instance, in modern computational neuroscience these models (especially ones with Poisson output) have already shown great promise in analyzing neural dynamics, recovering essential, low-dimensional, representations of noisy neural processes involving hundreds of neurons [3,4,5,6]. This kind of work helps us understand how the brain might work at a deeper level than that of single neurons.

### Useful resources

 * [Factor Analysis on Wikipedia](http://en.wikipedia.org/wiki/Factor_analysis)
 * [Kalman Filter on Wikipedia](http://en.wikipedia.org/wiki/Kalman_filter)

[1] Mark Schmidt [*minFunc*](http://www.cs.ubc.ca/~schmidtm/Software/minFunc.html)

[2] [*Wikipedia - Extended Kalman Filter*](http://en.wikipedia.org/wiki/Extended_Kalman_filter)

[3] Pachitariu M, Petreska B, Sahani M (2013) Recurrent linear lodels of simultaneously-recorded neural populations [*NIPS*](http://papers.nips.cc/paper/4877-recurrent-linear-models-of-simultaneously-recorded-neural-populations.pdf)

[4] Macke J H, Buesing L, Cunningham J P, Byron M Y, Shenoy K V, Sahani M (2011) Empirical models of spiking in neural populations [*NIPS*](https://bbuseruploads.s3.amazonaws.com/mackelab/pop_spike_dyn/downloads/Macke_Buesing_2012_Empirical.pdf?Signature=uWSfUKZ%2BhM1dQHa2GSiSs7BLiVI%3D&Expires=1424177382&AWSAccessKeyId=0EMWEFSGA12Z1HF1TZ82)

[5] Buesing L, Macke J H, Sahani M (2012) Spectral learning of linear dynamics from generalised-linear observations with application to neural population data [*NIPS*](https://bbuseruploads.s3.amazonaws.com/mackelab/pop_spike_dyn/downloads/Buesing_Macke_2013_PLSID.pdf?Signature=Qegy3oNWdd%2BR1QmjE8Kn2b4G2mA%3D&Expires=1424177567&AWSAccessKeyId=0EMWEFSGA12Z1HF1TZ82)

[6] Paninski L, Ahmadian Y, Ferreira D G, Koyama S, Rad K R, Vidne M, Vogelstein J, Wu W (2010) A new look at state-space models for neural data [*Journal of Computational Neuroscience*](http://link.springer.com/article/10.1007/s10827-009-0179-x/fulltext.html) 
