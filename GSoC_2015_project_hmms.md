# Hidden Markov Models for gene imputation
Cleaning up Shogun's HMMS and implementing a gene imputation pipeline

### Mentors
 * [Fabian Zimmer](http://qfma.de/) (github: [qfma](https://github.com/qfma))
 * [Heiko](http://herrstrathmann.de/) (github: [karlnapf](https://github.com/karlnapf), IRC: HeikoS)

### Difficulty & Requirements
**Medium/Advanced**. You need to be able to:
 - Cleanup and optimize C/C++ code
 - Have a good understanding of HMMs  (Knowledge of MCMC is helpful)
 - Have a basic understanding of genotyping and GWAS analysis
 - Visualize imputation results in an iPython notebook

### Description
There are  three major parts to this projects
 - Cleaning up Shogun's HMM implementation (mostly to be done in pre-GSoC phase, see below)
 - Extending HMM with a simple MCMC sampler
 - Build a pipeline to impute genotypes using sample data and data from the 1000 genome project

### Details

Hidden Markov Models (HMMs) have been used extensively in Bioinformatics to solve problems of biological sequence analysis. Among others, HMMs can be used to predict transcription factor binding sites [1], align sequences [2], find conserved sequence motives [3] and statistically infer ("impute") unobserved genotypes for Genome Wide Association Studies ([GWAS](http://en.wikipedia.org/wiki/Genome-wide_association_study)) [4]. One of the most popular tools at the moment that is able to impute genotypes, [Impute 2](https://mathgen.stats.ox.ac.uk/impute/impute_v2.html) [5, 6], uses HMMs and a Markov Chain Monte Carlo type algorithm; however, the software is not available under an open source license and only free for [academic use](http://www.stats.ox.ac.uk/~marchini/software/gwas/gwas.html#licence). In this project you will cleanup and optimize the HMM implementation in the Shogun Toolbox and subsequently use the HMMs to build a Bioinformatics pipeline to statistically impute genotypes in a sample dataset using the densely typed [1000 genome](http://www.1000genomes.org/) data as a background set.

The project is a great opportunity to combine machine learning with some real-world large scale genomic data and would enable the student to deepen her/his understanding of biological sequence analysis and large scale genomics.


### Waypoints and initial work
 * Step 1
 * Step 2
 * ...

### Optional
 TODO

### Why this is cool
The sharp decline in the cost of DNA and RNA sequencing enables genomic research on an unprecedented scale in a multitude of organisms. However, modern biology is challenged by the wast amounts of data generated and depends more and more on machine learning algorithms to analyze the produced data in order to further our understanding of the underlying biology. As such, the student will work in the intersection between machine learning, bioinformatics and genome biology, developing open source tools for the community. These tools could be used in Genome Wide Association Studies ([GWAS](http://en.wikipedia.org/wiki/Genome-wide_association_study)) that aim to enhance our understanding of major diseases like cancer or epidemics such as obesity.

### Useful ressources
 * [Imputation on Wikipedia](http://en.wikipedia.org/wiki/Imputation_(genetics))
 * [MCMC for gene imputation paper](http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1000529)
 * Entrance tasks:
  * [Remove precompiler flags](https://github.com/shogun-toolbox/shogun/issues/2712)
  * [Unit test HMMs](https://github.com/shogun-toolbox/shogun/issues/2713)
  * [Document CHMM](https://github.com/shogun-toolbox/shogun/issues/2714)
  * [Clean up parallelisation](https://github.com/shogun-toolbox/shogun/issues/2715)
  * [Notebook on HMM](https://github.com/shogun-toolbox/shogun/issues/2716)
  * [All (most) HMM issues](https://github.com/shogun-toolbox/shogun/issues?q=is%3Aissue+is%3Aopen+hmm)

[1] Kyoung-Jae W, Bing R and Wei W (2010) Genome-wide prediction of transcription factor binding sites using an integrated model [*Genome Biology*](http://genomebiology.com/2010/11/1/R7)

[2] Eddy SR (2008) A Probabilistic Model of Local Sequence Alignment That Simplifies Statistical Significance Estimation [*PLoS Computational Biology*](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000069#pcbi-1000069-g005)

[3] Eddy SR (2011) Accelerated Profile HMM Searches [*PLoS Computational Biology*](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1002195)

[4]   Howie B,  Marchini j , and Stephens M (2011) Genotype imputation with thousands of genomes [G3: Genes, Genomics, Genetics](http://www.g3journal.org/content/1/6/457.full)

[5] Howie B, Donnelly P, Marchini J (2009) A Flexible and Accurate Genotype Imputation Method for the Next Generation of Genome-Wide Association Studies [*PLoS Genetics*](http://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1000529#pgen.1000529-Marchini1)

[6] Howie B, Fuchsberger C, Stephens M, Marchini J, and Abecasis GR (2012) Fast and accurate genotype imputation in genome-wide association studies through pre-phasing [*Nature Genetics*](http://www.nature.com/ng/journal/v44/n8/abs/ng.2354.html)