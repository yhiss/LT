# Linguistic Regularities in Continuous Space Word Representations
自然言語処理での単語のベクトル表現


## WHO
- 金融機関でデータ分析
- 自然言語処理を真面目に勉強しようと思っています。
- 単語のベクトル化ついての論文を読みました。
- https://www.aclweb.org/anthology/N13-1090
- word vectorが統語的な規則性をとらえられることを示した論文(2013)
    (King - Man + Woman) = Queen


## Introduction
- word2vecの基になった論文の一つらしい
    word2vec:大量のテキストデータから単語の意味をベクトル表現化して**単語同士の意味の近さを計算できるようにした**もの
- neural network の言語モデルでは、wordsを高次元の実数ベクトルに表現することを行っている。
- 少し前のneural network language modelは伝統的なlanguage modelingのタスクである、**あるwordsが与えられた時に次に来る単語を予測する**ということを達成するもの。


- この論文では、学習されたword representationは実にシンプルな方法で意味のある**構文解析と意味解析**が可能となったと書いてある。
- 均整は単語のペア間の特徴的な関係性をshareするconstant vector offsetとして観察される
    e.g. 単語$$i$$のベクトルを$$x_i$$として表示する場合、下記のように表示する事ができた。
    $$x_{apple} - x_{apples} \approx x_{car} - x_{cars}$$…
- 使っているのは**Recurrent Neural Network(RNN) Model**
## 
## 4. Measuring Linguistic Regularity

**4.1** A Syntactic Test Set(構文解析)

- 右記のような類推問題を設定
    “a is to b as c is to 〇？”
    (e.g. 形容詞:base/比較級/最上級、名詞:単数形/複数形等)
    

**4.2** A Semantic Test Set(意味解析)

- 同じ意味だと推定されるword pairsのグループを利用して、degreeを求める
- 別の類推問題を解く
    e.g.  Class-Inclusion(集合包含):Singular Collective relationのペア***clothing:shirt****があった場合に、同じ関係性のペア****dish:bowl****のdegreeを量る。*
    この場合のanalogyは***“clothing is to shirt as dish is to bowl,”***

恐らくこの後にword2vecの中身であるSkip-Gram modelがつくられたのではないか…

![](https://paper-attachments.dropbox.com/s_63E4835A379FD264FA07F8178A9B7FC028ADE670F5CA982BDA52B0CC7B5B2125_1558764547874_dataset.png)

****## 5. The Vector Offset Method
- 構文解析と意味解析のタスクはanalogy questionに変換される
- cosine distanceに基づいたsimple vector offset methodを活用

 →embedding空間内でのvector offsetとして関係性を定義できる。

![](https://paper-attachments.dropbox.com/s_63E4835A379FD264FA07F8178A9B7FC028ADE670F5CA982BDA52B0CC7B5B2125_1558763026928_2.png)


本モデルでは、下記のanalogy questionを解く
$$a:b,c:d$$ ($$d$$が未知)
embedding vector $$\vec{x_a}$$,$$\vec{x_b}$$,$$\vec{x_c}$$(単位ノルムで正規化)を定義して,$$y$$を計算
(多分ここでRNNを使っている)
$$y = \vec{x_b} - \vec{x_a} + \vec{x_c}$$
もちろん、正確なポジションを厳密に決められるwordはないので、下記の式から*embedding vector* $$y$$*を求める*
$$\omega^{*}=argmax_{\omega}\frac{x_{\omega}y}{||x_{\omega}||||y||}$$
そして*dが与えられたら、*$$cos(x_b - x_a + x_c,x_d)$$*を計算する。*

## 結果
![](https://paper-attachments.dropbox.com/s_63E4835A379FD264FA07F8178A9B7FC028ADE670F5CA982BDA52B0CC7B5B2125_1558764641525_.png)

## これを読んだだけで自然言語処理できるようには全然ならないので、とりあえず言語処理100本ノックを始めた。

http://www.cl.ecei.tohoku.ac.jp/nlp100/#sec00

