# submarine_problem
潜水艦ゲームを数理最適化(gurobipy)で解く

# 潜水艦ゲームとは
![スクリーンショット (24)](https://user-images.githubusercontent.com/108399244/176718961-428fed99-c919-4443-8e12-e4e951e21903.png)

できるだけ少ない爆弾(印)で、見えない潜水艦を撃破するというのがこのゲームの意図と思われる

答えの例

![スクリーンショット (25) - コピー](https://user-images.githubusercontent.com/108399244/176719224-56e25396-9421-4bb5-a5f6-7bf5bb44d63d.png)

どの1×4マス部分を取り出しても、必ず☓が1つ含むのが分かる

今回はこれを一般化し、1×4マス以外にN×Mマスの場合にも解けるプログラムを作成した。

# 実行環境
windows 10 64bit

Anaconda 4.13.0

gurobipy 9.5.1

# プログラムの使い方
変数N, Mに盤面の縦の大きさ、横の大きさを入力


