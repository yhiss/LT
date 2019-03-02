# How (not) to use Machine Learning for time series forecasting: Avoiding the pitfalls
@yhiss
shinjuku もくもくプログラミング #35


## WHO
- 金融機関でデータ分析
- 今日はkaggleと時系列データの理解を進めてました

(**towards datascienceの記事をしました**)


## 時系列データ
- ***時系列***（じけいれつ、Time Series）とは、ある現象の時間的な変化を、連続的に（または一定間隔をおいて不連続に）観測して得られた値の系列（一連の値）のこと。[wikipedia]
- 時間的に順序を追って一定間隔毎に観測され、相互に統計的依存関係が認められるようなデータ系列[コトバンク]
- 一般的な例:株価等


## 時系列データ分析に使われるアルゴリズム
- LSTM(Long short-term memory)Network:言語処理等に使われる
- その他のNeural Network:TDNN([time delay neural networks](https://en.wikipedia.org/wiki/Time_delay_neural_network))、[feedforward neural network](https://en.wikipedia.org/wiki/Feedforward_neural_network)等
- シンプルなアルゴリズム:[random forest](https://en.wikipedia.org/wiki/Random_forest), [gradient boosting regressor](https://en.wikipedia.org/wiki/Gradient_boosting)等
## **本記事では、どのようなアルゴリズムを使うかよりも、データをどのように評価するかに主眼を置いている**


## **Example case: Prediction of time series data**
- e.g. the yearly evolution of a stock index(株価指数)
- 赤:training、実績データ、青:予測データとする
![](https://d2mxuefqeaa7sj.cloudfront.net/s_4E76E00D82738D7B0FD9B4553C04A87836AAE0C221F0BE5783D8D5F246EBDB84_1550300890927_1.png)


筆者が作ったモデルの予測値を縦軸、実際の値を横軸として相関をとるとR2が0.89と良い相関を取っている

![](https://d2mxuefqeaa7sj.cloudfront.net/s_4E76E00D82738D7B0FD9B4553C04A87836AAE0C221F0BE5783D8D5F246EBDB84_1550302005393_2.png)

## 見た目良さげなモデルだが、この指標をそのまま信じると失敗しがち…
## 株価指数で使われる数学的モデル
- ランダムウォークプロセス(次に現れる位置が無作為に選ばれる)
- そのため、シンプルに過去のデータを使っても予測することができない
## **Time delayed predictions and autocorrelations**
- 時系列データは名前の通り、時間的な特徴を捉える必要があるのが他のデータと異なる。
- 時間的な要素が増えるので、使用することができる特徴量としては増やすことができるが、扱いが難しい側面もある
## stock indexをシンプルにLSTMで予測してみると…
![](https://d2mxuefqeaa7sj.cloudfront.net/s_4E76E00D82738D7B0FD9B4553C04A87836AAE0C221F0BE5783D8D5F246EBDB84_1550303097842_3.png)

## 基本的に1日前の値を予測している
- 時系列データは時間と相関がある傾向があり、特徴的なautocorrelation(自己相関)を持つ
- 自己相関:データを時間的な要素等でシフトさせた場合に相関を持つこと(半年毎の周期性を持っていたりする)
## 予測値と実績値のcross correlation(相互相関関数)を取ると
![](https://d2mxuefqeaa7sj.cloudfront.net/s_4E76E00D82738D7B0FD9B4553C04A87836AAE0C221F0BE5783D8D5F246EBDB84_1550303713866_4.png)

## 思いっきり1日前の実績と同じ…
## まとめ
- 時系列データに対してモデリングする際には評価指標に気を付ける必要があるよ
- 割といろんなデータを予測できる機械学習でも何も考えずにモデル化すると痛い目に合うかもよ
- 時系列データを扱う時にはその対象にあった統計モデルを使うのがより適切なアプローチとなります
- なんだかんだ簡単な時系列データは機械学習でもよかったりはする(矛盾)
- (ちなみに決定木系の回帰はモデルを作ったときの範囲を超える値を出してはくれません…)
## 今後
- 時系列データの統計的なモデルの理解を深める
- サンプル使ってやる


