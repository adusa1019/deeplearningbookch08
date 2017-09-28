# deeplearningbook Chapter 08
## Optimization for Training Deep Models

---
## Leed
- 要約

---
## 8.1 How Learning Differs from Pure Optimization
- 要約

+++
### 8.1.1 Empirical Risk Minimization

+++
### 8.1.2 Surrogate Loss Functions and Early Stopping

+++
### 8.1.3 Batch and Minibatch Algorithms

---
## 8.2 Challenges in Neural Network Optimization
- ニューラルネットワークの最適化における有名な課題を列挙する
- どの課題がニューラルネットワークの最適化の本質的な難しさであるかはまだわかっていない

+++
### 8.2.1 Ill-Conditioning
- 凸最適化において、ヘッセ行列の悪条件であることが課題となることが知られている
- NN においても同様のことが言える
- 凸最適化では悪条件の場合にニュートン法が利用される
- しかしニューラルネットワークに適用するにはアルゴリズムに大きな変更が必要である

+++
### 8.2.2 Local Minima
- 目的関数が非凸であるため、極小値に落ちることがある
- 実務家(研究者ではなくNNで実問題を解くものを指していると思われる)は最適化の難しさを極小値によるものと考える傾向にある
- 最近の研究では、十分大きなNNでは極小値のコストは小さくなることが多いことがわかってきた

+++
### 8.2.3 Plateaus, Saddle Points and Other Flat Regions
- 高次の非凸関数では鞍点は極小値に比べて多くなる
- ただし経験的に勾配法は鞍点を避けることが知られている
- 一方、平坦な領域は任意の最適化手法で問題が生じる
    - 凸最適化の場合、平坦な領域は最適値となるため問題にならなかった

+++
### 8.2.4 Cliffs and Exploding Gradients
- 目的関数の勾配が急なところでパラメータが大きくジャンプしてしまう
- 勾配クリッピングにより回避可能
    - 更新量の上限を決めて勾配方向に更新するイメージ
- RNN で生じやすい
    - 同じ因子を繰り返し掛け算することによるとのこと
    - おそらく 8.11 式
+++
### 8.2.5 Long-Term Dependencies
- 同じパラメータを繰り返し利用する場合に発生する
    - ex. RNN
        - 再帰のステップ数を $$t$$, 重みを $$W$$ とすると $$W^t$$
- 勾配爆発 or 勾配消失を引き起こす
    - 理由は 8.11 式を見ればわかる
- FFNN では層毎の重みが異なるため起こらない

+++
### 8.2.6 Inexact Gradients
- 必ずしも正確に勾配を求められるわけではない
    - 目的関数が複雑なため
    - サンプリングを行うため など
- NN のために設計された最適化手法は不正確さな勾配でもうまく動くよう作られている

+++
### 8.2.7 Poor Correspondence between Local and Global Structure
- 勾配方向をたどっていっても必ずしもコストを十分下げられるわけではない
    - 極小値におちるという**意味ではない**
    - 極小値にすら(もちろん最小値にすら)たどり着かずに学習が終わることが多い
- うまい初期値を選択できれば回避できる
    - のでその研究が進められている
+++
### 8.2.8 Theoretical Limits of Optimization
- どの最適化手法に対しても NN の性能に理論限界があることが示されている
    - 実務的には大きな問題にはならない

---
## 8.3 Basic Algorithms
- 要約

+++
### 8.3.1 Stochastic Gradient Descent

+++
### 8.3.2 Momentum

+++
### 8.3.3 Nesterov Momentum

---
## 8.4 Parameter Initialization Strategies
- 要約
