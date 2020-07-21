# Assess *Performance* of MCMC algorithm
There are two things that we should watch closely when we use MCMC algorithm: **convergence** and **mixing**. "Convergence" means the Markov Chain converges to the appropriate density (the psterior density). "Mixing" means the Markov Chain samples from all areas of the density once it has converged. In these cases, we can promise the distribution we found through the MCMC algorithm approach stablely to our target distribution.<br/>
<br/>
However, you don't know how many iterations would need to reach convergence and mixing well. Convergence and mixing may be especially affected by a number of factors, including:
* The starting values for the parameters
* The shape of the posterior distribution
* The choice of proposal density in an MH algorithm

The following methods can help us to better understand how well our MCMC algorithm perform. It is important to note that there is no definitive way of assessing convergence and mixing. No single method can guarantee that the algorithm have converged or mixed thoroughly. We have to look our result from multiple perspective before making the conclusion.

1. Trace Plot


2. Acceptance rate (of MCMC algorithm)


3. Autocorrelation of parameter



4. Scale Reduction factor



# Assess *Model Fit*
1. Residual Analysis


2. Posterior fit of models


3. Bayes factors


4. Bayesian model averaging
