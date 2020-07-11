### 三、問題討論

1. 關於「模型的架構」─<br/>
   1. 透過Metropolis-Hasting Algorithm以及Gibbs Sampling的方式估計出Multivariate Gamma的parameter，那我們不就有我們想要的參數估計值能夠進行預測了嗎? 為什麼還需要用Gaussian Copula代入估計出的correlation matrix求一個Multivariate Gamma? 
   2. Multivariate Gamma跟Hierarchical Bayesian Model的連結為何?

2. 關於「估計」─<br/>
   1. 在論述層級貝氏的時候學長提到conditional posterior distribution以及posterior distribution分別代表的是什麼? 學長提到conditional posterior distribution用Gibbs Sampling估而posterior distribution用MH algorithm估計，剛好後面談到實際如何去做估計的時候，也談到是用MH algorithm估shape & scale parameter，以及用Gibbs Sampling估correlation matrix of Gaussian Copula，請教學長這個conditional posterior distribution指的就是shape & scale parameter 、posterior distribution 指的就是Gaussian Copula嗎?
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=10aNBlKbC_4BD4cseGxVyB7mHyJlkMJcv" width="1000" height="1200"></p>
   2. 在R的實務操作上，所謂的Metropolis-within-Gibbs是先用Gibbs Sampling將conditional  posterior distribution(也就是multivariate gamma distribution)的參數估計出來，再將這個估計出來的參數值代入Metropolis Hasting中針對multivariate gamma distribution的posterior distribution進行估計嗎?

3. 關於「預測」─<br/>
   1. 在透過Metropolis-within-Gibbs估出Hierarchical Bayesian Multivariate Gamma Model的posterior參數後，我們應該使用它的何種估計值(e.g.平均數)做為下一期的預測值?
   2. 學長使用兩種方式進行預測方法的建立，無論是哪一種，學長在推估下一期的購買間格時間t hat時，學長使用的是Multivariate Gamma Model的平均數作為這個t hat嗎?
   <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1yGiJ8wn3vUW_mIHKt_-7TaTF5dTFro3O" width="1000" height="1200"></p>
