# 潜水艦ゲームを数理最適化で解く
「潜水艦ゲーム」と呼ばれる数学パズルを数理最適化ソルバーgurobipyを用いて解くプログラムを作成した。

## 潜水艦ゲームとは
![スクリーンショット (24)](https://user-images.githubusercontent.com/108399244/176718961-428fed99-c919-4443-8e12-e4e951e21903.png)

海の上(盤面)から、できるだけ少ない爆弾(印)で、見えない潜水艦を撃破するというのがこのゲームの意図と思われる

答えの例

![スクリーンショット (25) - コピー](https://user-images.githubusercontent.com/108399244/176719224-56e25396-9421-4bb5-a5f6-7bf5bb44d63d.png)

1×4の大きさの潜水艦がどの位置にいても、必ず☓を1つ含む(撃破した)のが分かる。

今回はこれを一般化し、任意の大きさの潜水艦の場合でも解けるプログラムを作成した。

## 実行環境
windows 10 64bit

Anaconda 4.13.0

gurobipy 9.5.1

## プログラムの使い方
変数${N, M}$に盤面の縦の大きさ、横の大きさを入力

変数${P, Q}$に潜水艦の縦の大きさ、横の大きさを入力

以上を済ませて実行すると、上記の潜水艦ゲームの解をnumpy.ndarrayで出力する。

(1)5×6の盤面　2×3の潜水艦の場合

![image](https://user-images.githubusercontent.com/108399244/176725295-33273157-6425-437b-81d9-a766213a78b4.png)

(2)17×17の盤面　3×5の潜水艦の場合

![スクリーンショット (26)](https://user-images.githubusercontent.com/108399244/176726116-ad05f634-1519-433f-9960-7aa4061d661f.png)

## 最適化の数理モデル
0-1バイナリ変数を要素とした${N×M}$の二次元配列$X$を用意する。$X$の${(i, j)}$成分の値${X(i, j)}$を盤面の$i$行$j$列のマスと対応させて、
変数が0の時は印がない状態、変数が1の時は印がある状態と考える。

### 制約条件
潜水艦が横向きの場合、印が少なくとも1つ含まれる制約を入れる。
制約の数は${(N-P+1)(M-Q+1)}$個。

$$\sum_{p=0}^{P-1} \sum_{q=0}^{Q-1} X(i+p, j+q) \geq 1,\quad i=1, 2,...,N-P+1.\quad j=1, 2,...,M-Q+1.$$

潜水艦が縦向きの場合、印が少なくとも1つ含まれる制約を入れる。上の式から$p$と$q$,$P$と$Q$を入れ替えたもの。
制約の数は上の式と等しい。

$$\sum_{p=0}^{P-1} \sum_{q=0}^{Q-1} X(i+q, j+p) \geq 1,\quad i=1, 2,...,N-Q+1.\quad j=1, 2,...,M-P+1.$$

### 目的関数
印の数をできるだけ少なくしたいため、すべての変数の合計を最小化する

$$minimize \sum_{i=1}^N \sum_{j=1}^M X(i, j)$$



