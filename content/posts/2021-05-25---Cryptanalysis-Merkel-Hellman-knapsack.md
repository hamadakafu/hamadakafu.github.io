---
title: "解読 Merkel-Hellman-knapsack"
date: "2021-05-25"
template: "post"
draft: false
slug: "2021-05-25---Cryptanalysis-Merkel-Hellman-knapsack"
category: "cryptography"
tags:
  - "cryptography"
  - "CTF"
description: "Merkel-Hellman-knapsackのLLLを用いた解読"
socialImage: "me.png"
---

# Introduction
SECCON Beginners 2021のcryptoのField-tripで出た問題がMerkel-Hellman-knapsackの解読をする問題だった．

LLLが解読でわかりやすく利用されていて勉強になるのでその備忘録．

# Preliminary
LLLについて完結に整理する．
LLLの由来はLenstra-Lenstra-Lovaszの頭文字でそれぞれが人の名前になっている．

## LLLアルゴリズム
$n$次元格子$L$の基底$\{b_1, \cdots, b_n\}$に対して，近似版のSVP(Approximate SVP)を解くアルゴリズムの1つ．

### 第$i$次逐次最小$\lambda_i(L)$
格子$L$に対して$i$番目に小さい格子ベクトルのノルム．

$i$個の格子ベクトルを含む格子上の空間の最小の半径とも言う．

### Approximate SVP
$n$次元格子$L$の基底$\{b_1, \cdots, b_n\}$と近似因子$\gamma(n) \geq 1$があたえれたとき，
$$
|v| \leq \gamma(n) \lambda_1(L)
$$
を満たす格子上のベクトル$v \in L$を見つける問題．


## LLL基底簡約アルゴリズム
LLLアルゴリズムを用いて$n$本の基底$\{b_1, \cdots, b_n\}$に対して，
$b_i$が **ざっくり** 第$i$次逐次最小$\lambda_i(L)$になるように基底を簡約するアルゴリズム．

詳細は省くが部分サイズ基底簡約を繰り返し行い，
Lovasz条件を満たしていなければGSOとかで基底を更新する感じ．

## Merkel-Hellman-knapsack
$n$bitの平文と超増加列$\{a_i\}_n$の内積が暗号文

wikipedia参照[^MHKWIKI]

# Merkel-Hellman-knapsackをLLLで解読
これ[^MHKLLL]に全部書いてある．

アイデアとしてはLLL基底簡約アルゴリズムに$n$bitの平文を解かせたいので，
基底を列ベクトルとして最後の基底に基底の和すなわちknapsackの和である暗号文をしまい，
LLL基底簡約アルゴリズムを実行する．
暗号文の行が0になっていて，その他の行が$0$か$1$になっていたらそれが答えになっている．
LLL基底簡約アルゴリズムをそのまま使っているので，
LLL基底簡約アルゴリズムの**ざっくり**した性質から**必ず問題が解けるとは限らない**．

以下の例では超増加列を$1, 2, 4, 8$とし暗号文を$10$となっている．
$$
\begin{pmatrix}
1 & 0 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 \\
1 & 2 & 4 & 8 & 10 \\
\end{pmatrix}
$$

実行すると（本当は実行していないので細かい数字を知らないが）
以下のような行列が生成されたとして，
$3$列目と5列目が最後$0$になっているので解の候補だが，
$5$列目は-1が含まれていて暗号文として不正．
$3$列目は超増加列の$2$と$8$を選んだことを意味する．

よって平文は$0, 1, 0, 1$になる．
$$
\begin{pmatrix}
? & ? & 0 & ? & 0 \\
? & ? & 1 & ? & -1 \\
? & ? & 0 & ? & 1 \\
? & ? & 1 & ? & 1 \\
3 & 1 & 0 & -1 & 0 \\
\end{pmatrix}
$$


# References
[^MHKWIKI] https://ja.wikipedia.org/wiki/Merkle-Hellman%E3%83%8A%E3%83%83%E3%83%97%E3%82%B5%E3%83%83%E3%82%AF%E6%9A%97%E5%8F%B7
[^MHKLLL] http://www.cs.sjsu.edu/faculty/stamp/papers/topics/topic16/Knapsack.pdf


