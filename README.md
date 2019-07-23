# reading-Salem-et-al-2019-NDSS

- Authors: Ahmed Salem, Yang Zhang, Mathias Humbert, Pascal Berrang, Mario Fritz, Michael Backes
- Title: ML-Leaks: Model and Data Independent Membership Inference Attacks and Defenses on Machine Learning Models.
- In: 26th Annual Network and Distributed System Security Symposium (NDSS 2019).
- Conference: NDSS - Network and Distributed System Security Symposium

# ML-Leaks: Model and Data Independent Membership Inference Attacks and Defenses on Machine Learning Models.

## Abstract

- 近年注目される機械学習。その核となるのは訓練データ。大きな成功を背景に、インターネット企業は機械学習をサービスとして展開する(Machine Learning as a Service)。MLaaS 設定において、memership inference attack によって初めて訓練データの情報が抽出される可能性が示された。この問題は、セキュリティ・プライバシーに関係がある。

- 攻撃が実行可能であることは先行研究で示されてきたが、攻撃者に多くの仮定が存在する(multiple shadow models, knowledge of the target model structure, and having a dataset from same distribution as the target model's training data)。 我々は、この仮定を緩和する。コストが低くこれまでよりも厳しいリスクを提案する。8つのデータセットを使用して、提案するドメインを超えた攻撃が可能であることを示す。

- 加えて、防御手法を提案する。MLモデルの有用性を高く維持しつつ広く membership inference attack を防ぐ。

## INTRODUCTION

- 機械学習が熱い流れで MLaaS が熱い。MLaaS はユーザがデータセットを投入すれば訓練されたMLモデルが返ってくるblack-boxAPIである。MLモデルに対してセキュリティ・プライバシー攻撃を行う例がある（model inversion, adverserial examples, model extraction）。特に membership inference attack に注目する。あるデータ点が訓練に使用されたか否かを推定する。攻撃例: 特定の病気にかかった人を対象に学習したモデルがあった場合、ある人のデータ点が訓練に使用されたか否かを推定することでその人の病気がわかってしまう。

- Shokri ら(2017)は初めてメンバーシップ推定攻撃を導入した。target modelのふるまいを模倣した複数の shadow modelsを生成する攻撃手法を提案。

- Shokriら(2017)の攻撃者の仮定は2つある。1. 攻撃者は target model と同じ構造をした shadow model を複数作る必要がある。shadow modelの訓練に同じMLaaSを使うことがこのシチュエーションにあたる。2. shadow models の訓練に使用するデータセットの従う分布が訓練データの従う分布に等しい。2番目の仮定を緩和するためにShokriらは人工的にデータ生成を行う手法も提案している。効率の点から、実際の実験では2値表現のデータセットについて適用している。

- 2つの仮定がとても強い。この論文では、攻撃者の仮定を緩め、より広い状況で攻撃が可能であることを示す。実際にはより弱い仮定で攻撃が可能で、それを防ぐための2つのメカニズムを提案する。

### Membership Inference Attack

### Defence

