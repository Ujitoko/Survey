Maxout Networks
--

# Abstract

* モデルの汎化のための*dropout*というテクニックの問題を考える
* 我々は *maxout* というシンプルなモデルを考案した
  * 入力のセットのうち最大なものを出力するためこのように命名
* 目的は2つ
  * dropoutによる最適化を促進すること
  * dropoutの高速なapproximate model averaging techniqueの正確性を向上すること
  * 実験により上記を達成したことを確認した
    * MNIST, CIFAR-10, CIFAR-100, SVHN

# Introduction

* Hinton et al.のdropoutは，安価で簡易なアンサンブルなモデルの訓練手法だ
  * パラメータを共有し，モデルの予測を平均化する
  * しかしdeep architectureにはこれまで試されてこなかった


* dropoutのための理想的なoperating regimeは．パラメータ更新が大きく行われる際だ．パラメータ共有の制約下でアンサンブル学習すること
* これはstochastic gradientのregimeと全く異なる
  * １つのモデルが小さいステップで進行していく


* 別の懸念として，deep modelsでは，dropout model averagingはただのapproximation（近似）にすぎないことである
  * この近似誤差を小さくすることは，dropoutのパフォーマンスを良くすることにつながる


* *maxout* を提案する
  * 最適化と，dropoutを使ったmodel averagingに有効な特徴がある


# Review of dropout

* output *y*
* input vector *v*
* series of hidden layers ${h = \{{h^{(1)},..., h^{(L)}}}\}$
*

* dropoutはアンサンブルなモデルをtrainする
  * それぞれ，$v$と$h$のサブセットをもっている


* 同じ $\theta$ を $p(y|v;\theta,\mu)$ に対して使う
  * $\mu \in M$ はバイナリマスク．それはどの変数をモデルに含むかを決める


* Droput trainingはbagging（Breiman, 1994）に近い
  * 違う多くのモデルが，異なる入力に対して訓練する
* dropoutは次の点でbaggingと異なる
  * 1stepだけ訓練し，パラメータは全モデルで共有する点


* functional formは，全サブモデルの予測をアンサンブルするときに重要となってくる
  * どう平均するか？
  * 幸運なことに，幾何平均を算出するのは簡単
  * $W/2$ をすればよい...**（なぜ)**


# 3. Description of maxout

$x \in \mathbb{R}^d$ を入力とするとき，
maxout hidden layerは以下の関数をとる.

$$
h_i(x) = \max_{j \in [1,k]} z_{ij}
$$

ただし $z_{ij} = x^T W_{...ij} + b_{ij}$であり，
$W \in \mathbb{R}^{d×m×k}$ と $b \in \mathbb{R}^{m×k}$ は学習パラメータとする．

* maxoutはこれまでのactivation functionとは異なる特徴を持つ
  * maxoutによる表現は密である
  * localにはlinearである．
* これらを考えるとうまくいくとは思えないのだが，実際にはロバストで学習しやすく，驚異的なパフォーマンスを示す．


# 4. Maxout is a universal approximator

* standardなMLPはuniversal approximatorであるように，
maxoutもuniversal approximatorだ

# 7. Model averaging

* 効果的なモデルであることは実験でわかった




# 次に読みたい論文

* dropout論文（Hinton el al.,2012）
