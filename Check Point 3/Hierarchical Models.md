**Hierarchical models** are models in which there is some sort of hierarchical structure to the parameters and potentially to the covariates if the model is a regression model.<br/>
In this chapter, the author provide two applcations of Hierarchical Models:

1. Capturing the effect and relationship between parameters with hierarchical level (the model parameters are structured hierarchically)<br/>
   The Bayes' theorem is often expressed as:<br/>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=p(\theta|data) \propto p(data| \theta) \times p(\theta)" width="300" height="35"></p>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=posterior \propto likelihood \times prior" width="300" height="35"></p>
   This equation itself reveals a simple hierarchical structure in the pararmeters, becasue it says that a posterior distribution for a parameter is equal to a conditional distribution for data under the parameter (first level) multiplied by the marginal (prior) probability for the parameter (a second, higher, level). Put another way, the posterior distribution is the prior distribution weighted by the observed information.<br/>
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
   The remaining unkown part is the parameters of hyperprior, C and D. Given parameters C and D, the mean of a gamma distribution is equal to C/D, and the variance is equal to C/D^2. We my choos e to set these parameters at values that reflect our prior knowledge.The typical poll conducted throughout the fall by different polling organizations consisted of about 500 or potential voters, roughly half of the voters are expected to vote for Kerry. So, we may choose C/D=250. We can capture prior uncertainty in this estimate by specifying the variance to be large since we have little knowledge about it. For example, we assume the variance C/D^2=10000. Thus, we can find C=6.25 and D=0.025. From now on, we know all the conditional posterior distribution for each parameter, and can use Gibbs Sampler to do the inference.<br/>  
   
   
2. Capturing the linear regression model with hierarchical level (the data are measured at differenct levels / hierarchical sttructure to the data, need multilevel modeling)<br/>
   1. Random Intercept model<br/>
      1. with intercept model to illustrate the random effect<br/>
         <p align="center">
         <img src="https://render.githubusercontent.com/render/math?math=y_{it}= \alpha_i %2B e_{it}" width="100" height="35"></p>
         where alpha is group level variable and e is individual random error term as below
         <p align="center">
         <img src="https://render.githubusercontent.com/render/math?math=\alpha_i ~ N(\alpha, \tau^2) " width="100" height="35"></p>
         <p align="center">
         <img src="https://render.githubusercontent.com/render/math?math=e_{it} ~ N(0, \sigma^2)" width="100" height="35"></p>
         which can also present as:
         <p align="center">
         <img src="https://drive.google.com/uc?export=view&id=1TU_rkJGLiiwHPIOPDNGr1B5pHAH30odb"></p>
         To derive the estimate for each parameter, we can follow steps as the previous section shows, which we derive the posterior distribution
         <p align="center">
         <img src="https://drive.google.com/uc?export=view&id=1BERmI2fzyEsUhVNQqEzd7j5Zpdo56V7v"></p>
         and then we derive conditional posterior distribution of each parameter. Finally, we can use Gibbs Sampler or Metropolis Hasting to make the inference.   
      
      2. use a regression to illustrate the random effect
         1. add a binary variable (e.g. sex)
            <p align="center">
            <img src="https://drive.google.com/uc?export=view&id=1a_ndUpPRjMFkKGJ1N4I8Rw-2iaX1sZ9v"></p>
            we can further derive estimastes for each parameter following previous steps. 
         
         2. add a continuous variable (e.g. Internet usage amount)
            <p align="center">
            <img src="https://drive.google.com/uc?export=view&id=1cHHzSNwadBmGOB0lHBEQpbRw2_Gcvke7"></p>
            we can further derive estimastes for each parameter following previous steps.
      
   2. Random coefficient model<br/>
   In the previous section, we use single coefficient to represent the effect from the Internet variable. However, the effect may be different among different individual levels. Thus, by adding this variation (with one more sub-index under alpha), our model becomes:
      <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1yNg-Ilx1cWA1uq3qLq4ezu3H3qGVtYHi"></p>   
      Consider the interaction between different variable, we can put our two variables under different levels, then it becomes
      <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1f5a1dUjaQy-rm4eEIgR_9pFtqfzRFeiR"></p>  
      In a traditional regression form, it looks like:
      <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=182V9WVxpijcL8iKFttTJc4uCA29njbMC"></p>  
      , which can be rewritten as
      <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1H5JyS7COGEO4QZ4jf-vRKa2ODP1IJnw6"></p>  
   3. Growth model<br/>
      Besides, in social science, we usually want to look at the effect under different timeframe and use time as our explanatory variable. Then, our model may look like:
      <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1qg_050mebdFd5Zr2XTzPeLmdTjPI-LdG"></p>  
   
   
