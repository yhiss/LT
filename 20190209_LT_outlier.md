# 外れ値検出
@yhiss
shinjuku もくもくプログラミング #34


## WHO
- 金融機関でデータ分析
- 初めてdropbox paper使ったので、勝手がよくわかっていない
- 今日は~~kaggle~~と外れ値検出手法の理解を進めてました

(**ACM SIGKDD 2018 Workshop:**
Making sense of unusual suspects - Finding and Characterizing Outliers)


# 概要
## 外れ値(outlier)とは…
## [統計](https://ja.wikipedia.org/wiki/%E7%B5%B1%E8%A8%88)において他の値から大きく外れた値である。測定ミス・記録ミス等に起因する[異常値](https://ja.wikipedia.org/w/index.php?title=%E7%95%B0%E5%B8%B8%E5%80%A4&action=edit&redlink=1)とは概念的には異なるが、実用上は区別できないこともある。(wikipediaより)
## どのようなものか？
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549683342026_1.png)

# 外れ値の何がうれしくない？
- **基本的にモデルの精度が下がる!!**
- 下の表でいう赤の行が外れ値:
  Requests countを予測したい場合、Query entropyとの関係性が他の行と違う
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549684703658_2.png)

## **基本的な外れ値へのアプローチ:データから除外**
## **どれが外れ値かを判定するのが課題…**
- 統計的な手法:四分位とか分散とか
- **機械学習的な手法:教師あり学習や教師なし学習**

→今回の発表では、後者で解決しようとしている

## **機械学習的手法**
- 教師あり学習
  - 一般的に精度は高め
  - training dataにラベル付け(正解を決める)をすることが必要
  - 新しいタイプの外れ値ができた場合に対応できない
- 教師なし学習
  - 教師ありに比べるとパフォーマンスは劣る
  - ラベル付けは不要
  - 新しいタイプの外れ値の対応〇
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549685774224_3.png)



## **論文でのアプローチ法…教師あり学習と教師なし学習を組み合わせる!!(超機械学習的発想)**
- 通常の変数(下図x1,x2…)に加えて、新しい変数を加えて教師あり学習
- 新しい変数:教師なし学習で変数を追加(Φ1(x),Φ2(x)…)
- 教師なし学習:様々なタイプの外れ値検知手法を**組み合わせる(機械学習的発想)**
  - Different outlier detection algorithms:  kNN-outlier, LOF, ABOD, COP, SOD, … , 
  - Different parameter settings, 
  - Different distance functions, 
  - Different subspaces, 
  - …
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549686575300_4.png)

## 結果…
## なんかいい感じで特徴量を作ることができ
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549687039352_4.png)

## 精度も上がったらしい
- グラフ:ROC曲線
- 不均衡(e.g.正解を0と1に分けると0がやたら多い)なデータの時によく使われる指標)
- カーブが上に盛り上がっている程性能が良い
![](https://d2mxuefqeaa7sj.cloudfront.net/s_92BADB5E1BE714C2B71FF27B3C91EAEA48B0DDAD9C519E56694D9A7F22BBBB8C_1549687071892_5.png)

# おわり

