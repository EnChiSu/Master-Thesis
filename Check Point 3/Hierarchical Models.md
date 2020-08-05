**Hierarchical models** are models in which there is some sort of hierarchical structure to the parameters and potentially to the covariates if the model is a regression model.<br/>
In this chapter, the author provide two applcations of Hierarchical Models:

1. Capturing the effect and relationship between parameters with hierarchical level<br/>
   The Bayes' theorem is often expressed as:<br/>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=p(\theta|data) \propto p(data| \theta) \times p(\theta)" width="300" height="35"></p>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=posterior \propto likelihood \times prior" width="300" height="35"></p>
   This equation itself reveals a simple hierarchical structure in the pararmeters, becasue it says that a posterior distribution for a parameter is equal to a conditional distribution for data under the parameter (first level) multivplied by the marginal (prior) probability for the parameter (a second, higher, level). Put another way, the posterior distribution is the prior distribution weighted by the observed information.<br/>
   For example,
   We know that the election polling result follow beta distribution as below,
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=x_i~Beta(\alpha, \beta, K)" width="200" height="35"></p>
   Our goal is to know the posterior distribution's parameters given our data as below,
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1V4dP23rIzLve2LyqheMLlx02XDXETIhU"></p>
   Since we also know likelihood follows binomial distribution, which can be shown as:
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1Y5unJ0ELkxKYsHiB7yNoZGQAYrJmIquB"></p>
   and prior for each K follows beta distribution, 
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1Bru45oJpgnUuA377YCdIx2nzeg7Revs9"></p>
   , we can derive the posterior distribution,
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1Kp4wMrmidR5uADF5apktOj8NW2Tu2W8k"></p>
   We can further simplify the posterior distribution leaving items related to our parameters, which becomes
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1_t6d3_gmOBs66o9HmT31N9i7r0fT9SU4"></p>
   As we know the posterior distribution, we can find the conditional posterior distribution for each parameter repectively to further derive the proper estimation using MCMC. The conditional posterior distribution for K is
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1TMK7avAtMBHTdg7JOQxSf4SNDx68uUJX"></p>
   The conditional posterior distribution for alpha is (which need a little trick to simplify it)
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=13i1HNUsG8KYns4V031d5KSBsCvAm47Vw"></p>
   The conditional posterior distribution for beta is (which need a little trick to simplify it)
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1OQB_7dQcFOegk1gyLPFMCfnqdfID0SWU"></p>
   Since the joint marginal distribution p(a,B) is unkown, we assume an appropriate distribution that would constrain thes parameters to be non-negative is the gamma distribtuion. The two parameters in gamma distribution we use C and D the represent. Besides, we assume that the alpha and beta have independent prior distributions, then the joint marginal distribution would equal to the product of each one's marginal distribution, which can be shown as
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1S05qW8YbdBjzehXrB3kxil08FNPIlwHN"></p>
   Then, we can derive the full conditional posterior distribution for alpha: (A comparable result can be obtained for beta)
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1qqZFzwXwn1NhyvW92gGK0b8xg2SaQMJr"></p>
   
   
2. Capturing the linear regression model with hierarchical level<br/>
   1. Random Intercept model<br/>
   
   
   
   2. Random coefficient model<br/>
   
   
   3. Growth model<br/>
   
   
   
