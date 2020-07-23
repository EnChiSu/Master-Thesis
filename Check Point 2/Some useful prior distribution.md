# Some useful prior distribution
1. **Dirichlet distribution**<br/>
   The Dirichlet distribution is a multivariate generalization of the beta distribution. If X is a k-dimensional vector and X~Dirichlet(a1, a2, a3,...), then:
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=1vqq8XPqpCnIzo-ptsIAe2kFMJYE96HHS"></p>
   Just as the beta distribution is a conjugate prior for the binomial distribution, the Dirichlet is a conjugate prior for the multinomial distribution.
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=1SYZeE4_kubcR9XVUIYmKVN8tTJ6nUur_"></p>

2. **Inverse Gamma distribution**<br/>
   If 1/x ~ gamma(a,b), then x ~ IG(a,b). The density function for the inverse gamma distribution is:
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=1JXT89IH-WqkUEexgSfvSIXY5JrUgKei_"></p>
   with x>0. Just as in the gamma distribution, the parameters a and b affect the shape and scale of the curve(respectively), and both must be greater than 0 to make the density proper.
   
   Besides, the **inverse gamma** distribution is used as a conjugate prior for the **variance** in a normal model. If the normal distribution is parameterized with a precision parameter rather than with a variance parameter, the **gamma** distribution is appropriate as a conjugate prior distribution for the **precision parameter**. 
   
   Note: <br/>
   1. In a normal model, if an inverse gamma distribution is used as the prior for the variance, the marginal distribution for the mean is a **t distribution**.
   2. Gamma & inverse gamma are general distribution: 
      1. Gamma(a=1,b) == exp(1/b)
      2. Gamma(a=v/2,b=1/2) == Chi(df=v)

3. **Wishart and Inverse Wishart distribution**<br/>
   Wishart and Inverse Wishart distribution ar emultivariate generalization of the gamma and inverse gamma distributions, respectively. Thus, just as the inverse gamma is a conjugate prior density for the variance in a univariate normal model, the inverse Wishart is a conjugate prior density for the variance-covariance matrix in a multivariate normal model. 
   If X ~ Wishart(S), where S is a scale matrix of dimension d and v is the degrees of freedom, then
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=1W6IlKGydh2vPNLqW7ARXHBp4PNBi_eC2"></p>
   If X ~ inverse Wishart(1/S), then
   <p align="center">
     <img src="https://drive.google.com/uc?export=view&id=1BvyoaiyF2Qro30OfarRXb9skZ7xOR9ca"></p>
   The assuption for both the Wishart and inverse Wishart distributions is that X and S are both positive definite; that is, z^T X z > 0 and z^T S z > 0 for any non-zero vector z of length d.
   
   Note:<br/>
   With an inverse Wishart distribution for the variance-covariance matrix in a multivariate normal model, the marginal distribution for the mean vector is multivariate t.



Reference: Chapter 3.5 of Introduction to Applied Bayesian Statistics and Estimation for Social Scientists by Scott M. Lynch
