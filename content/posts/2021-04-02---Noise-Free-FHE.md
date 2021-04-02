---
title: "Noise-Free FHE"
date: "2021-04-02"
template: "post"
draft: false
slug: "2021-04-02-noise-free-fhe"
category: "cryptography"
tags:
  - "cryptography"
  - "FHE"
description: "Noise-FreeなFHEについて"
socialImage: "me.png"
---

# NoiseなFHE
NoiseなFHEっていうのはすなわち格子暗号をベースにしてるFHEのこと．

まぁ他にもあるかもしれないが．．．

NoiseなFHEでは連続して演算を続けるとNoiseが大きくなっていってしまうので，
何らかの方法でNoiseを減らす作業をする必要があるが，
それが俗に言う`bootstrapping`とか`modulus switching`のこと．
TFHE[^TFHE]ではキーサイズが一度増えるが、キーサイズを小さくする際に`bootstrapping`をやっている．
`keyswitching`っていうのかもしれない．

格子暗号周りの課題として`bootstrapping`の高速化がある．

# Noise-FreeなFHE
iacrでいっぱい見られるらしい(?)

Noise-Freeだと`bootstrapping`が不要になるのでそんな悩みがなくなる．
Noise-FreeなFHEとして
- Octonionを使った[^YAG] [実装した](https://github.com/hamadakafu/octonion)
  - 大体2000bitの$q$がいいって書いてた
- 暗号文が$n+1$のベクトルの[^LIU]
  - ちゃんと読んでないが和はベクトルの和で積がpublickeyを使って要素同士の積みたいな感じだった．
- これもOcotonion[^WANG] OctoMっていうschema
  - [^LIU]への攻撃方法とかも書いてる
  - Lie群$G_2$とか言ってた
- Sedenion(16元数)のやつ[^SED]

# 主なAttack Modeについてのまとめ
## COA (Ciphertext-only attack)
Ciphertextにしかアクセスすることができず一番弱い攻撃

modernな暗号はだいたいこれに耐性がある．

Modern crypto schema is immune from the COA.

## wCOA (weak COA)
いくつかのciphertextに対して，その中にどれかに対応するplaintextを当てる攻撃
[^WANG]の`def 2.3`
これに耐性があるとき，
$$
P[\text{wCOA}(\kappa) = 1] \le \text{negl}(\kappa)
$$

## CPA (Chosen-plaintext attack)
攻撃者はいくつかのplaintextを任意に選ぶことができ，それに対応するciphertextを取得できる．

## CPA2 (Adaptive CPA)
攻撃者は連続したplaintextを取得でき，各ステップで前の結果を利用することができる．

## CCA (Chosen-ciphertext attack)
攻撃者はいくつかのciphertextを任意に選ぶことができ，それに対応するplaintextを取得できる．

## CCA2 (Adaptive CCA)
CPA2と同じ

# References
[^TFHE] https://eprint.iacr.org/2018/421.pdf

[^YAG] https://eprint.iacr.org/2017/763.pdf

[^LIU] https://eprint.iacr.org/2015/468.pdf

[^WANG] https://webpages.uncc.edu/yonwang/papers/octonionAlgebra.pdf

[^SED] https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=9134724

attack model https://en.wikipedia.org/wiki/Attack_model

