# Fundamental Machine Learning Algorithms, Part 2
Linear Latent Gaussian Models: Linear and non-linear


### Mentors
 * Fernando (github: [iglesias](https://github.com/iglesias), IRC: iglesias)
 * Heiko (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
Easy/medium/advanced.
You need to be able to
 * get confused by C/C++
 * trim beards
 * count socks

### Description
Models: State space dynamics are linear Gaussian
Observation links might be Gaussian but can also be non-linear.
Both learning and inference.

Models:
 * LGSSM
   * Kalman filter for inference
   * EM for learning
   * HO-Kalman for fast EM learning
 * Non-linear GSSM: Let's focus on exp-family link functions
   * Inference: variational, EP for the E-step
   * Learning: variational EM, See Büsing & Macke "Non-linear Kalman"

Other ideas:
 * Use existing EM framework for the variational apprixmate methods
 * Could be that we need to change it, maybe even another iteration on GMMs
 * HMM re-implementation. Viterbi, Baum Welch, all neat and clean? Notebook?
 * Other Linear Gaussian models: FA, PPCA, also work with the above algorihtms (EM, gradient descent)
 * ARD for LGMs. Prior on columns of projection matrix, compute posterior

### Details
Write about details of the project here.

### Waypoints and initial work
 * More Random forests (BART)
 * Please put your ideas here

### Optional
Parts of the project that would be cool once the core is finished.

### Why this is cool
Motivation to get involved here.

### Useful ressources
 * Put a list of ressources/links here