### Keras與Tensorflow的簡短發展史：
> ● Keras 最初是由 Google AI 開發人員 / 研究人員 Francois Chollet 創建並開發的。
> ● Francois 於 2015 年 3 月 27 日將 Keras 的第一個版本 commit 並 release 到他的 GitHub。
> ● 一開始，Francois 開發 Keras 是爲了方便他自己的研究和實驗。但是，隨着深度學習的普及，許多開發人員、程序員和機器學習從業人員都因其相較於其他當時的API(Torch、Theano、Caffe
)易於使用而涌向 Keras。
<br/>
> ● 爲了訓練你自己的自定義神經網絡，Keras 需要一個**後端**。*後端是一個計算引擎——它可以構建網絡的圖和拓撲結構，運行優化器，並執行具體的數字運算*。
<br/>
> ● 一開始，在 v1.1.0 之前，Keras 的默認後端都是 Theano。與此同時，Google 發佈了 TensorFlow，這是一個用於機器學習和神經網絡訓練的符號數學庫。Keras 開始支持 TensorFlow 作爲後端。漸漸地，**TensorFlow 成爲最受歡迎的後端**，這也就使得 TensorFlow 從 Keras v1.1.0 發行版開始成爲 Keras 的默認後端。
<br/>
> ● 隨着越來越多的 TensorFlow 用戶開始使用 Keras 的簡易高級 API，越來越多的 TensorFlow 開發人員開始考慮將 Keras 項目納入 TensorFlow 中作爲一個單獨模塊，並將其命名爲 tf.keras。TensorFlow v1.10 是 TensorFlow 第一個在 tf.keras 中包含一個 keras 分支的版本。現在 TensorFlow 2.0 已發佈，keras 和 tf.keras 已經處於同步狀態，這意味着儘管 keras 和 tf.keras 仍是獨立的兩個項目，但是開發人員應該開始使用 tf.keras，因爲 keras 軟件包僅支持錯誤修復。
<br/>
> ● Google在 2019 年 6 月發佈 TensorFlow 2.0 時，他們宣佈 Keras 現在是 TensorFlow 的官方高級 API，用於快速簡單的模型設計和訓練。

> ● Keras 2.3.0 的發佈，Francois 聲明：1. 這是 Keras 首個與 tf.keras 同步的版本；2. 這也是 Keras 支持多個後端（即 Theano，CNTK 等）的最終版本；3. 所有深度學習從業人員都應將其代碼轉換成 TensorFlow 2.0 和 tf.keras 軟件包。

### Summary:<br/>
簡單來說，Keras是易於使用的機器學習前端API介面，而Tensorflow則是API介面背後負責運算的引擎。目前Tensorflow 2.0已經納入Keras包裹，並且為Keras持續更新的包裹(又稱tf.keras)，原本獨立於Tensorflow之外的Keras包裹將不再更新(或說只會針對現有的進行錯誤修復，但不會有新的功能)，因而往後應使用tf.keras包裹進行模型訓練。


<br/>
Reference: https://www.chainnews.com/zh-hant/articles/916826219156.htm
