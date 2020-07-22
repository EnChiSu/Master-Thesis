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
The acceptance rate can reflect the converge performance of the MCMC. If the acceptance rate is 0%, the algorithm would never converge. In contrast, if the acceptance rate is 99%, the algorithm converge very slowly. The ideal acceptance rate would be around **50% or slightly lower**. More generally, a rate between 25% and 75% is often acceptable.<br/>
Two factors influence the acceptance rate:<br/>

   1. jump size<br/>
   The jump size is determined by the variane or width of the proposal density. The narrower it is the smaller each step is. Thus, it would have higher acceptance rate, but it would also takes a large numver of iterations before the algorithm mixes thoroughly. On the other hand, the wider it is the larger each step is. In this case, the algorithm would move quickly from one end of the posterior density to the other and converge early. However, because of the high rejection rate around the tail, it has the problem that stick in one place for long periods of time before moving.
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=13xvatwT5iOC-cbvuTf0tARHilVLE-4Fw"></p>
      
   2. shape of the proposal density<br/>
   The concordance of the shape of the posterior distribution and proposal density would increase acceptance rate. 
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1ScfEW8LLJaa5TLHiABWhaKNfCc-vkmg9"></p>
    Besides, we should also consider the correlation between different parameters. A conmmon source of poor mixing and/or slow convergence in MH algorithms is strong posterior correlation of the parameters.
    <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1njVEGngcInsYy6W6-BXHIx16bEYUuFwd"></p>
   
3. Autocorrelation of parameter<br/>
High autocorrelation would make algorithm inefficient. Espeically in the slow mixing scenario, which exacerbate autocorrelation, there are two solutions for the problem. 
   1. Thinning the chain<br/>
   Take every k th sampled value. K is determined by the number of lags beyond which autocorrelation of sampled values is small enough to ignore. The function of ACF is
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1oK8IjVdkMI4DKxBSHMB4oe8Xc7Y2Exd-"></p>
       
   2. Batch means<br/>
   Compute the means of every block of k sampled values and treats the batch mean as the sampled value.


4. Scale Reduction factor and Others<br/>
Other method that can test the performance of the MCMC algorithm is through comparing results from multiple MCMC simulations with different starting point or proposal density parameters. One way to test whether the algorithm has converged is through "Scale Reduction factor", which can be computed as 
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1XnRTE5XUrmT_3Cl3_7xO08-vxSS0OgUn"></p>
   Since the variance between chains should decrease as the chains converge, the within variance should approaches the total variance, which make the index close to 1.
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1dGD2-dnBAw6Y-alBxqZ2tRRH6U9G5OKw"></p>


# Assess *Model Fit*
* **Evaluating model fit**
1. Residual Analysis<br/>
Under Bayesian approach, we will get a distribution of the parameters and thus a distribution of residuals for each obesrvation in the data set. With the distribution of errors, we can construct "tests" to determine whether the error distribution is significantly different from 0. Or we can compute the propostion of errors that exceed some value q. A model that produces a relatively high average proportion of errors exceeding the criterion q may be deemed a poorly fitting model.<br/>
One of the limitation of the method is that it is primarily only useful in a regression model setting.


2. Posterior predictive distribution (PPD)<br/>
One of the advantage of PPD is that it captures two undertainties: (1) Parametric uncertainty (2) Sampling uncertainty.<br/>
   1. Parametric uncertainty<br/>
   You can imagine this as the "variance of posterior distribution".
   2. Samping uncertainty<br/>
   It's the sampling density for the data. You can also imagine this as the likelihood function. It is directly associate with the posterior distribution as below shows.
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=10asetiDA0O5GJBEMzgjEaf0LmORol3Zi"></p>
   With the help of probability density for future observations, we can make prediction base on the observed sample data: (y rep denote furutre observation)
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1y9oYH926VCv5KA4y3wQDLEbMEXrlTPNF"></p>
   If a model fits the data well, future data simulated from the model should look like the current data. We can conduct Bayesian p-values to determine whether the simulated and observed data are similar. The p-value is
   <p align="center">
       <img src="https://drive.google.com/uc?export=view&id=1kH0-1Ff572fj-S_-WLxYPBV8kxOiXPp0"></p>
   , which represent the proposrtion of replicated future data sets whose function values T(y rep) exceed that of the function T(y) applied to the original data.<br/>
   <br/>
* **Comparing model fit**
3. Bayes factors


4. Bayesian model averaging


<br/>
<br/>
Reference: Introduction to Applied Bayesian Statistics and Estimation for Social Scientists by Scott M. Lynch 
