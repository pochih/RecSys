## DeepFM: A Factorization-Machine based Neural Network for CTR Prediction

Huifeng Guo, Ruiming Tang, Yunming Ye, Zhenguo Li, Xiuqiang He, IJCAI 17'

### Summary
- 任務：做在 CTR (click-through rate)，也就是點擊率預測。基本上就是個 binary classification 問題 (點擊 or 沒點)
- 概念：用 FM (factorization machine) 學習 low-order features，用 DNN 學習 high-order features
- 與之前做法比較
  - FNN 需要 pretrained FM，DeepFM 不用任何 pretrained
  - PNN 主要捕捉 high-order features，比較難捕捉到 low-order features
  - wide & deep 需要大量的人工特徵 (feature-engineering)
- 作法基本上就是剛剛提到的概念
  - FM 與 DNN 共享 dense embedding vector，或者稱作 latent vector。不管是 categorical or continuous data 都能轉成 dense embedding vector
  - FM 捕捉 order-1 (by linear regression) 以及 order-2 (by inner-product of latent vector) 特徵。DNN 捕捉 high-order 特徵
  - FM 以及 DNN 的 output 會 concatenate 在一起，然後丟進 sigmoid classifier，用 cross-entropy 訓練

### Strengths / Novelties
- 解決了之前 NN-based 方法無法捕捉 low-order features 的問題
- 解決了 wide & deep 需要大量特徵工程的低通用性

### Weaknesses / Notes
- 感覺 CTR 的論文都習慣性的把 low-order 以及 high-order feature 分開討論。是否能夠探討一下 low-order & high-order 之間的 interactions，而不是在最後才把他們 concatenate 在一起
