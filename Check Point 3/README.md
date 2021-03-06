This is the summary of my reading documentation of the past 2 weeks:<br/>

1. Book Review:<br/>(reference: [Introduction to Applied Bayesian Statistics and Estimation for Social Scientists](https://www.springer.com/gp/book/9780387712642))
   * [Hierarchical models](https://github.com/EnChiSu/Master-Thesis/blob/master/Check%20Point%203/Hierarchical%20Models.md) (Ch9)


2. Literature Review:<br/>
   1. [Small Area Estimation of Expenditure Per-capita in Banyuwangi with Hierarchical Bayesian and Empirical Bayes Methods](http://iptek.its.ac.id/index.php/jos/article/view/3185)<br/>
   In this paper, it presents how to apply Hierarchical Bayesian(HB) and Empirical Bayes(EB) on the Small Area Estimation Method, which is often used to estimate parameters for sub-level in the data and solve the problem that the sub-level of the data isn't large enough. The author shows that with the help of HB and EB, the RMSE of SAE is smaller comparing with direct estimator. Additoinally, the RMSE of estimator from HB is even smaller than the EB. <br/>
   (The mathematical derivation using Hierarchical Bayes can be your reference.)
   2. [Modeling of Per Capital Household Expenditure in Tanzania using Bayesian Two Levels Hierarchical Log-Logistic Approach_The Case Study of Dodoma Region](http://sersc.org/journals/index.php/IJAST/article/view/22911)(這篇品質不是很好，資料來源和分析方法可能都是最後結果不顯著的原因，最前面的introduction可以參考)<br/>
   The paper provides a good reasoning to research in household expenditure (because it’s more stable than household income) and to model household expenditure with hierarchical bayesian model.<br/>
   The micro model represents household characteristics. The macro model represents district characteristics.<br/>
   The result shows that four of the district characteristics, population density, ratio of health facility per capita, ratio of education facility per school age capita, and ratio of healthy person per capita, have significant effect on household expenditure. Contrastively, none of the household characteristics has dominant influence on household expenditure. 

   3. [Toward a Hierarchical Bayesian Framework for Modelling the Effect of Regional Diversity on Household Expenditure](https://www.researchgate.net/publication/274008292_Toward_a_Hierarchical_Bayesian_Framework_for_Modelling_the_Effect_of_Regional_Diversity_on_Household_Expenditure)(這篇是上面那篇的高品質篇，東西是近似的，上篇用Log logistic，這篇用Log normal，但分析和結果的比較精緻)(另外這篇將household expenditure直接與household welfare做連結)<br/>
   The paper provides good mathematical notation and steps illustrating the hierarchical bayesian model.<br/>
   The author also use micro and macro model to explain the household expenditure (or household welfare).<br/>
   The micro model represents household characteristics. The macro model represents district characteristics.<br/>
   The result shows that in terms of household characteristics the housing condition, daily needs facilities in the house, the human capital, the number of people, and level of education of household head. <br/>
   In terms of the district characteristics, accessibilities of public facility(正向), number of small / household industry (正向), and percentage of wetland (負向) have significant effect on household welfare.

   4. [Model Criticism for Log-Normal Hierarchical Bayesian Models on Household Expenditure in Indonesia](https://ieeexplore.ieee.org/document/6396521)<br/>
   In the paper, the author dig into a measuring tool for model comparison, deviance information criterion (DIC). Extend the discussion from the previous paper discussing household expenditure hierarchical Bayesian modeling. The author use the DIC comparison of prediction result from two-parameter log-normal hierarchical model and the three-parameter log-normal hierarchical model to illustrate his idea.
   5. [Determinants Of Household Final Consumption Expenditures In Asian Countries_ A Panel Model, 1991-2015](https://ideas.repec.org/a/eaa/aeinde/v18y2018i1_8.html)<br/>
   The paper illustrates influential economics factors to the household expenditures and compares the model for Asian countries with the globe as baseline. These factors are:
      1. Income (represented by GNI)<br/>
      In models for Asian and the Globe, the income factors are significant in both models. However, in Asian model, this factor is smaller and less significant than Global model when GNI increase by 1%. The possible reason is that Asian has higher propensity to save comparing with the global average.
      2. Population growth<br/>
      Population growth also contributes significantly to the household expenditure in both models. However, it's found that in the Asian model the contribution is much higher per 1% population growth comparing with the global model. One of the possible reasons I'm thinking about is that we Asians emphasize more in education. Parents are willing to devote more resources to their child, such as sending them to study abroad, hoping them to be successful. 
      3. Lending Interest rate (reflect monetary policy)<br/>
      In both models, the lending interest rate has inverse impact on the household expenditure. Higher interest rate leads to lower household expenditure, and vice versa.
      4. Government total expenditure (reflect fiscal policy)<br/>
      Both models present the effect from the government total expenditures. Addtionally, expansionary fiscal policies can be even more efficient in the short-run. The coefficient of the factor is also higher than the monetary factor, which illustrate the importance of its influence.<br/>
      It's also found that the influence of this factor in the Asia region is much higher. My thought of this finding is that Asian countries are more collectively thinking cultures and more tend to be influenced by the public sentiment and floating information around the market. Thus, the impact from the policy might extend longer and stronger than the globe. Plus, the neutralize effect in the global model might also be the factor.
      
   
3. Some idea for the research topic:<br/>
   This [kaggle competition](https://www.kaggle.com/grosvenpaul/family-income-and-expenditure) provides an interesting dataset of household expenditure in Philippines. It seems like the hierarchical model can suit it well.
   

