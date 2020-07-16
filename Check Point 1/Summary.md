### 一、論文內容
1. 論文主題的想法<br/>
自己目前有想了兩個論文主題，都是跟multivariate gamma distribution有關(似80x80的網格點)，簡要的概念為希望可以貝氏模型以及MCMC的方式估計出不同組別服從的multivariate gamma distribution的參數，進而可以去對各個組別中的data進行預測或是異常值偵測。
   1. 估計網格參數並做預測─<br/>
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以針對組別內網格上每個網格的data做下一個時點的預測。
   2. 異常值偵測─<br/>
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以去網格上每個網格點的實際data去做比對，將超過3個標準差的網格標記出來。

2. 使用的方法<br/>
類似下面介紹2017年李京諭學長論文的方法，透過MCMC去估計Hierarchical Baysian Model(層級貝氏)中不同組服從mutivariate gamma的posterior distribution，來了解不同組別當中不同網格點上的值。

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1jvzL9UHtbsPQIwRvdHoUCUZP3LgwNvn0">
</p>
<br/>

### 二、這三周的進度
在這兩周我完整讀了2017年統研所李京諭學長所撰寫的「[以多變量Gamma Distribution探討多品項購買期間的相關性](https://www.airitilibrary.com/Publication/alDetailedMesh1?DocID=U0001-2306201712014100)」，並且了解當中使用的三個方法(MCMC、Hierarchical Bayesian Model、Copula)和Python及R的實作方式。論文當中還有一些概念間的串接自己還沒完全領悟，以下會概括描述自己對整篇論文的理解，以及在三個所使用方法所做的認識。

這篇論文中，學長混和MCMC的Gibbs Sampler以及Metropolis Hasting去建構Hierarchical Bayesian Multivariate Gamma Model中的Shape、Scale parameter以及Correlation matrix of Copula model，進而去預測兩兩不同商品的購買時間間格，並與MLE法估計建構出的層級貝式模型去做預測上的優劣比較。<br/>

針對本篇的主要方法Hierarchical Baysian Multivariate Gamma Model中的Shape以及Scale parameter，由於並不清楚posterior distribution的樣態而使用Metropolis Hasting algorithm估計。同時由於為多維度必須考慮不同維度之間的相關性，因此此篇論文使用Gaussian copula作為變數間相關性的基礎，透過產生Multivariate standard normal distribution再轉為multivariate gamma distribution的方式，描繪出模型當中的correlation參數。
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=17W6WdYEJ8wPvLv6kKjmTOLULBI0jwuef"></p>
      
1. MCMC：<br/>
使用的緣由是我們沒有使用conjugate prior的情況下，並不知道posterior的分布長甚麼樣子，透過對這個posterior進行多次的抽樣了解這個分布在不同位置的density。這樣的概念下開發出幾個不同的演算法，包含Metropolis Hasting Algorithm、Gibbs Sampling，主要的概念都是透過guess(隨機提一個proposal，也就是隨機抽樣)，然後check(看這個樣本的機率有沒有大過你設定的門檻，如果有則跳到這個新的proposal的位置並提下一個proposal繼續探索，如果沒有則在原位置提新的proposal，詳見下一段Metropolis Hasting的說明例子)，如此可以慢慢建立出posterior分布的輪廓。然而，Metropolis Hasting這樣的方法的問題在於它並沒有限制proposal的方向，所以可能會提了很多最後被 reject掉的proposal造成演算法很沒有效率，相對應能夠避免此問題的演算法包含Gibbs Sampling以及Hamiltonian Monte Carlo。<br/>

   * MCMC的Metropolis Hasting & Gibbs Sampling詳細介紹：<br/>
   1. Monte Carlo<br/>
   設定一個分配，從這個分配中進行無限次的隨機抽樣(例如：Normal(0,1)，每次抽樣都來自這個平均數為0的Normal分布)

   2. Markov Chain<br/>
   你的下一次抽樣(只)會受到這次資料的影響。在MCMC中代表的是我下次起跳基準點會來自左這次Monte Carlo抽樣的起跳基準點(例如：這次的起跳基準點是Normal(0.5,1)，是因為上次從Normal(0,1)跳到0.5，也就是每次Monte Carlo抽樣的分配參數都會不同)

   3. Metropolis Hasting<br/>
   透過posterior的ratio比較新的proposal的機率與上一次的機率，如果大於1(也就是新的proposal的posterior大於前次的postrior)則我們一定接受這次的proposal，如果小於1則拿這個ratio去與一個從univorm(0,1)隨機抽出的機率比較，如果較大則我們接受這次的proposal，跳到那裡，如果較小則我們拒絕這次的proposal，留在原本的位置。(如此重複無限次，慢慢就會收斂到我們想估計參數的posterior上，我們可以透過對這些歷史跳動點取平均的方式，作為對這個參數的估計值)<br/>
   實作範例：1. https://github.com/Joseph94m/MCMC/blob/master/MCMC.ipynb<br/>
               2. https://twiecki.io/blog/2015/11/10/mcmc-sampling/
    [<p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1_ISh5EZ-izq67fm5MKijcjclskPPSjOR"></p>](https://www.youtube.com/watch?v=OTO1DygELpY)
      
    4. Gibbs Sampler<br/>
    使用Gibbs Sampling的先決條件是必須要知道個別變數condition on其他所有變數的conditional distriubtions。在已知conditional distribution下，我就可以針對個別維度去進行抽樣，隨著取樣次數越多，個別維度會收斂趨近到真實的分布，將這些不同維度上模擬出來的資料點combine在一起得到的joint distribution也就會趨近那個你想要了解的posterior distribution(因為個別維度模擬的資料也都服從相對應的conditional distribution)。<br/>
    若碰到conditional distriubtions未知的情況，針對該維度的conditional distriubtions可以用Metropolis Hasting的方式求，搭配其餘已知的conditional distribution使用Gibbs Sampling求，結合在一起求得想了解的joint distirubtion(postrior distribution)，這樣的方法稱為[Metropolis within Gibbs](https://people.duke.edu/~ccc14/sta-663/MCMC.html#gibbs-sampler)。<br/>
    因而Gibbs Sampler其實可以視為一種特殊形態的Metropolis Hasting，它每一次新的proposal都是沿著特定某個維度方向上跳動，且每次跳動一定都被接受，因而大幅增進效率。但它的缺點是當不同維度之間彼此具有高度相關性時，可能會很沒有效率(因為每次跳動都是沿著某個維度跳動，下個跳動換另一個維度跳，也就是跳動受限於單一維度，不能斜著跳)。
    [<p align="center">
      <img src="https://drive.google.com/uc?export=view&id=17PokSmbplh_GUkHbXEYb93lD2U217cRj" width="500" height="450"></p>](https://www.youtube.com/watch?v=ZvCYW8Ggby8)
      
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

3. [Gaussian copula](https://twiecki.io/blog/2018/05/03/copulas/)：<br/>
    Copula是用來描繪兩個不同變數關係的function。假定H(x,y)為一bivariate distribution，F(x)、G(y)為x、y的pdf，則存在一個唯一的copula函數C，使得H(x,y)=C(F(x),G(y))，因而可知C(u,v)=H(inverse F(u), inverse G(u))。而Gaussian copula即為假設F和G皆為Normal的情況。<br/>
    
    在本篇論文中，由於商品購買間格時間服從multivariate gamma distribution並且不同變數間具有某種相關性，但我們無法透過資料求出這個multivariate gamma distribution變數間相關性的close form解，因而透過gaussian copula轉換的方式(將原始分布透過cdf轉為Gaussian distribution)，將這些實證資料從multivariate gamma distribution轉換我們熟知的multivariate standard normal distribution，由於各個維度的conditional distribution皆為已知，因而就可以透過Gibbs Sampling的方式找出最符合資料的multivariate standard normal參數，以及我們想要了解的相關係數矩陣。
    
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1BOwBrZEQvq-ghGQkEM9iCwLj9GL24thX"></p>
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=1ZLCi7-I57sXIKIJ6GEiolppU_kVHCxk9"></p>
    <p align="center">
      <img src="https://drive.google.com/uc?export=view&id=13tb2QaofqG8jstdhAsDSAjK_eZAN1iEH"></p>
    透過這個Gaussian copula我們就能夠描繪Hierarchical Bayesian Multivariate Gamma Model中的correlation。(Gaussian copula的correlation matrix透過Gibbs Sampler估計，因為我們已知posterior distribution屬於何種分布)
    <br/>
