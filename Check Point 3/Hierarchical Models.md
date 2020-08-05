**Hierarchical models** are models in which there is some sort of hierarchical structure to the parameters and potentially to the covariates if the model is a regression model.<br/>
In this chapter, the author provide two applcations of Hierarchical Models:

1. Capturing the effect and relationship between parameters with hierarchical level
   The Bayes' Theotem is often expressed as:<br/>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=p(\theta|data) \propto p(data| \theta) \times p(\theta)" width="300" height="35"></p>
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=posterior \propto likelihood \times prior" width="300" height="35"></p>
   This equation itself reveals a simple hierarchical structure in the pararmeters, becasue it says that a posterior distribution for a parameter is equal to a conditional distribution for data under the parameter (first level) multivplied by the marginal (prior) probability for the parameter (a second, higher, level). Put another way, the posterior distribution is the prior distribution weighted by the observed information.<br/>
   For example,
   <p align="center">
      <img src="https://render.githubusercontent.com/render/math?math=y_{ig}~Q( \theta_g)"></p>



2. Capturing the linear regression model with hierarchical level
