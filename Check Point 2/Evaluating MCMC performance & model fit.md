# Assess *Performance* of MCMC algorithm
There are two things that we should watch closely when we use MCMC algorithm: **convergence** and **mixing**. "Convergence" means the Markov Chain converges to the appropriate density (the psterior density). "Mixing" means the Markov Chain samples thoroughly from all areas of the density once it has converged. In these cases, we can promise the distribution we found through the MCMC algorithm approach stablely to our target distribution.<br/>
<br/>
However, you don't know how many iterations would need to reach convergence and mixing well. Convergence and mixing may be affected by a number of factors, including:
* The starting values for the parameters
* The shape of the posterior distribution
* The choice of proposal density in an MH algorithm

The following methods can help us to better understand how well our MCMC algorithm perform. It is important to note that there is no definitive way of assessing convergence and mixing. No single method can guarantee that the algorithm have converged or mixed thoroughly. We have to look our result from multiple perspective before making the conclusion.

1. Trace Plot<br/>
We can firstly use trace plot to inpsect visually and calculate the mean and standard deviation of certain number of iterations. For example, after 400 iterations the MCMC converge, but if we iterate even further we can find that after 1000 iterations the posterior distribution might cover broader range than we thought. Thus, it is important to use different methods to inspect our result.
<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1BLG2f9fL0QmaJ599f_BGwd9El0wWU905">
</p>

2. Acceptance rate (of MCMC algorithm)<br/>
The acceptance rate can reflect the converge performance of the MCMC. If the acceptance rate is 0%, the algorithm would never converge. In contrast, if the acceptance rate is 99%, the algorithm converge very slowly. The ideal acceptance rate would be around 50% or slightly lower. More generally, a rate between 25% and 75% is often acceptable.

3. Autocorrelation of parameter<br/>



4. Scale Reduction factor<br/>



# Assess *Model Fit*
1. Residual Analysis


2. Posterior fit of models


3. Bayes factors


4. Bayesian model averaging



Reference: Introduction to Applied Bayesian Statistics and Estimation for Social Scientists by Scott M. Lynch 
