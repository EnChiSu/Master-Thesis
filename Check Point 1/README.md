### 一、論文內容
1. 論文主題的想法
自己目前有想了兩個論文主題，都是跟multivariate gamma distribution有關(似80x80的網格點)，簡要的概念為希望可以貝氏模型以及MCMC的方式估計出不同組別服從的multivariate gamma distribution的參數，進而可以去對各個組別中的data進行預測或是異常值偵測。
   1. 估計網格參數並做預測─<br/>
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以針對組別內網格上每個網格的data做下一個時點的預測。
   2. 異常值偵測─<br/>
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以去網格上每個網格點的實際data去做比對，將超過3個標準差的網格標記出來。

2. 使用的方法
類似下面介紹2017年李京諭學長論文的方法，透過MCMC去估計Hierarchical Baysian Model(層級貝氏)中不同組服從mutivariate gamma的posterior distribution，來了解不同組別當中不同網格點上的值。

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1jvzL9UHtbsPQIwRvdHoUCUZP3LgwNvn0">
</p>
<br/>

### 二、這兩周的進度
在這兩周我完整讀了2017年統研所李京諭學長所撰寫的「以多變量Gamma Distribution探討多品項購買期間的相關性」(https://www.airitilibrary.com/Publication/alDetailedMesh1?DocID=U0001-2306201712014100)，並且了解當中使用的三個方法(MCMC、Hierarchical Bayesian Model、Copula)和Python及R的實作方式。論文當中還有一些概念間的串接自己還沒完全領悟，以下會概括描述自己對整篇論文的理解，以及在三個所使用方法所做的認識。

這篇論文中，學長混和MCMC的Gibbs Sampler以及Metropolis Hasting去建構Hierarchical Bayesian Multivariate Gamma Model，進而去預測兩兩不同商品的購買時間間格，並與MLE法估計copula建構出的層級貝式模型去做比較。針對Hierarchical Baysian Multivariate Gamma Model中的Shape以及Scale parameter，由於並不清楚posterior distribution的樣態而使用Metropolis Hasting估計。而由於為多維度必須考慮不同維度之間的相關性，因此此篇論文使用Gaussian copula作為變數間相關性的基礎，透過產生Multivariate standard normal distribution再轉為multivariate gamma distribution的方式，描繪出模型當中的correlation參數。
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=17W6WdYEJ8wPvLv6kKjmTOLULBI0jwuef"></p>
      
1. MCMC：<br/>
使用的緣由是我們沒有使用conjugate prior的情況下，並不知道posterior的分布長甚麼樣子，透過對這個posterior進行多次的抽樣了解這個分布在不同位置的density。這樣的概念下開發出幾個不同的演算法，包含Metropolis Hasting Algorithm、Gibbs Sampling，主要的概念都是透過guess(隨機提一個proposal，也就是隨機抽樣)，然後check(看這個樣本的機率有沒有大過你設定的門檻，如果有則跳到這個新的proposal的位置並提下一個proposal繼續探索，如果沒有則在原位置提新的proposal，如此可以慢慢建立出posterior分布的輪廓。然而，這樣方法的問題在於它並沒有限制proposal的方向，所以可能會提了很多最後被 reject掉的proposal造成演算法很沒有效率。(https://www.youtube.com/watch?v=OTO1DygELpY)
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1_ISh5EZ-izq67fm5MKijcjclskPPSjOR"></p>
    新進的方法是Hamiltonian Monte Carlo(HMC)，即為目前很多建構機器學習方法的gradient decent(梯度下降)，將先前沒有特定方向的proposal改用梯度下降的方式(想像在一個碗裡面彈出一個鐵球)去引導proposal，因而每次提出的proposal都會往density大的方向前進(也就是碗底的方向)，不再有reject的情況，而變得非常有效率。而梯度下降演算法中鐵球的重量、重力的大小、跳的次數這些參數都可以調整，會進一步影響對posterior distribution建構的效率，因而需要進行調整。 (https://www.youtube.com/watch?v=v-j0UmWf3Us)

2. Hierarchical Bayesian Model：<br/>
層級貝氏模型混和單一模型(common mean model)與個別模型(individual model)，使可以將模型無法解釋的部分拆解為組間的差異以及組內的差異。
層級貝氏的作法就像是傳統回歸(也就是單一模型)的進一步延伸，傳統回歸背後假設資料服從一個特定平均數、變異數的常態分配。層級貝氏則往上加一層，資料所服從的分配的參數會服從另一個分配(也就是hyperparameter所代表的)。(https://www.youtube.com/watch?v=VssgU4Ey7ss)
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1Xb_TPxHxU_mydFQrs2H59c9HRcPNmOgL" width="700" height="400"></p>
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1AkM1EGuDFwVIdGHKjOYOIuuZ8LCpdVzl" width="1000" height="400"></p>
    因而若想要使用MCMC估計層級貝氏所產生的posterior，在進行MCMC的迴圈時，必須將不同組的效果另立一個變數做代表，針對不同組跑回圈，使可以利用MCMC估計不同組的posterior。
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1ell7YNilD1RbGBkODnDu1WRuotv4Mvkh" width="800" height="400"></p>
    R的實作如以下兩個連結。<br/>
    https://opendatascience.com/building-your-first-bayesian-model-in-r/  (單純用MCMC估計貝式posterior的R實作)<br/>
    https://medium.com/@ODSC/hierarchical-bayesian-models-in-r-9a18e6acdf2b  (加入層級貝氏用MCMC估計每一組posterior的R實作)

3. Gaussian copula：<br/>
    Copula是用來描繪兩個不同變數關係的function。假定H(x,y)為一bivariate distribution，F(x)、G(y)為x、y的pdf，則存在一個唯一的copula函數C，使得H(x,y)=C(F(x),G(y))，因而可知C(u,v)=H(inverse F(u), inverse G(u))。而Gaussian copula即為假設F和G皆為Normal的情況。<br/>
    在學長的論文當中，學長透過如同我們在鄭主任的R語言視覺化課程中模擬的方式，這定特定的correlation下隨機去產生Bivariate standard normal distribution並轉換成cdf (uniform distribution)，根據這個cdf再轉換到bivariate gamma distribution，使得這個bivariate joint distribution能夠捕捉到前面設定的這個correlation。(https://twiecki.io/blog/2018/05/03/copulas/)
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1BOwBrZEQvq-ghGQkEM9iCwLj9GL24thX"></p>
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1ZLCi7-I57sXIKIJ6GEiolppU_kVHCxk9"></p>
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=13tb2QaofqG8jstdhAsDSAjK_eZAN1iEH"></p>
    透過這個Gaussian copula我們就能夠描繪Hierarchical Bayesian Multivariate Gamma Model中的correlation。(Gaussian copula的correlation matrix透過Gibbs Sampler估計，因為我們已知posterior distribution屬於何種分布)
    <br/>

### 三、問題討論

1. 論文的方向及可行性<br/>

2. 論文當中讀不懂的地方<br/>
   1. 產生multivariate gamma distribution的模擬後，與Hierarchical Bayesian Multivariate Gamma Model之間的關聯為何?<br/>
   2. Metropolis-within-Gibbs當中，使用Gibbs sampler估計conditional posterior distribution，而用Metropolis-Hasting估計posterior distribution，是因為我們已知 conditional posterior distribution的分布樣態，而不知 posterior distribution的樣態嗎? 這個conditional  posterior distribution以及posterior distribution在這次購買間格的研究中又代表的是甚麼? Metropolis-within-Gibbs這種混和的方法單純就是將 Gibbs sampler以及Metropolis-Hasting混合使用嗎? 有沒有需要調校模型參數或權重? <br/>
   3. 在透過MCMC建構好層級貝氏模型的posterior後，如何進行預測的實現? 每個data丟入模型，應該會產生一個相對應的posterior參數，我們是使用這個估計出來的posterior mean作為我們的預測值嗎?<br/>
   4. 如果網格不是方形的話(橫軸的變數數與縱軸的變數數不同)，還可以使用multivariate gamma進行推估嗎?
