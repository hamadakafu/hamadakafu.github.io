---
title: "Noise Free FHE"
date: "2021-04-02"
template: "post"
draft: false
slug: ""
category: "cryptography"
tags:
- "cryptography"
description: "Noise FreeなFHEについて"
socialImage: "me.png"
---
# NoiseなFHE
NoiseなFHEっていうのはすなわち格子暗号をベースにしてるFHEのこと．

まぁ他にもあるかもしれないが．．．

NoiseなFHEでは連続して演算を続けるとNoiseが大きくなっていってしまうので，
何らかの方法でNoiseを減らす作業をする必要があるが，それが俗に言う`BootStrapping`のこと．

# 主なAttack Modeについてのまとめ

## COA (Ciphertext-only attack)
Ciphertextにしかアクセスすることができず一番弱い攻撃．

modernな暗号はだいたいこれに耐性がある．
Modern crypto schema is immune from the COA.

## CPA (Chosen-plaintext attack)
攻撃者はいくつかのplaintextを任意に選ぶことができ，それに対応するciphertextを取得できる．

## CPA2 (Adaptive CPA)
攻撃者は連続したplaintextを取得でき，各ステップで前の結果を利用することができる．

## CCA (Chosen-ciphertext attack)
攻撃者はいくつかのciphertextを任意に選ぶことができ，それに対応するplaintextを取得できる．

## CCA2 (Adaptive CCA)
CPA2と同じ

