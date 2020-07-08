# 一、論文內容
1. 論文主題的想法
自己目前有想了兩個論文主題，都是跟multivariate gamma distribution有關(似80x80的網格點)，簡要的概念為希望可以貝氏模型以及MCMC的方式估計出不同組別服從的multivariate gamma distribution的參數，進而可以去對各個組別中的data進行預測或是異常值偵測。
(1) 估計網格參數並做預測─
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以針對組別內網格上每個網格的data做下一個時點的預測。
(2) 異常值偵測─
根據不同組別所推估出來的multivariate gamma的參數之後，我就可以去網格上每個網格點的實際data去做比對，將超過3個標準差的網格標記出來。

2. 使用的方法
類似下面介紹2017年李京諭學長論文的方法，透過MCMC去估計Hierarchical Baysian Model(層級貝氏)中不同組服從mutivariate gamma的posterior distribution，來了解不同組別當中不同網格點上的值。

<p align="center">
  <img src="https://drive.google.com/uc?export=view&id=1GnoFbgsrK6OjXhuArTyAeqkxyKMsIM6P" width="400" height="400">
</p>
