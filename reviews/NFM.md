## Neural Factorization Machines for Sparse Predictive Analytics

Xiangnan He, Tat-Seng Chua, SIGIR '17

### Summary
- 任務：做在 CTR (click-through rate)，也就是點擊率預測
- 賣點：對 FM (factorization machine) 的 output 做些改動，用 DNN 抽取更高 order 的 features
- 模型
	- 這篇論文引進了 bilinear interaction pooling (bi-interaction)，整個模型的架構是 input -> FM -> bi-interaction -> DNN -> prediction。prediction 可以是 regression or classification
	- How to bi-interaction?
		- FM 是 latent vector 兩兩做內積，bi-interaction 概念很簡單，就只是把內積換成 element-wise product，然後把所有 element-wise product 的東西加起來
		- 因此 FM 的 output 是一個 scalar，bi-interaction 的 output 是一個 vector (維度跟 latent vector 一樣)
	- FM 是 NFM 的一種特例，如果 bi-interaction 的 output vector 跟一個 one-vector 內積就變成 FM
- 實驗
	- bi-interaction 的 output 後面只接一層 layer 效果最好
	- bi-interaction 的 output 後面加 dropout 更好
	- bi-interaction 的 output 以及之後的 layer 都加 batch normalization

### Strengths / Novelties
- FM 只能捕捉到 order-2 的 features。用 DNN 可以補足這個缺點
- 為了接 DNN，作者引入了 bilinear interaction pooling

### Weaknesses / Notes
- 以直覺來說，bi-interaction 那段似乎很容易 over-fitting。有認識的人把 bi-interaction 做在 graph embedding 上，模型的上限有超越 related work，但下限也很低，需要非常仔細的 tuning
