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

- 2つの仮定がとても強い。この論文では、攻撃者の仮定を緩め、より広い状況で攻撃が可能であることを示す。実際にはより弱い仮定で攻撃が可能で、それを防ぐための2つのメカニズムを提案する。このように攻撃者の仮定を緩める（TABLE1）。

### Membership Inference Attack.

- shadow models の訓練データ・そのデザインに基づいた3種類の攻撃者を研究する。モデル・データに依存しない攻撃者まで考える。

- Adversary 1. : target model の訓練データの従う分布と同じ分布に従うデータを持つ。shadow models の仮定を緩和する。

  - 複数のshadow modelsではなく、target model のふるまいを模倣するモデルをたった1つ学習する。MLaaSではモデルの学習にお金がかかるため、shadow modelを1つにすることは、membership inference attack のコストを下げる。

  - 様々なデータセットを通した実験評価によって、1つのshadow model, attack modelでもShokriらと同程度の攻撃が成功した。target model CNNがCIFAR-100で学習したとき、単純化した我々の攻撃が0.95 precision, 0.95 recallとなった(10 shadow models, 100 attack models)。既存(Shokriら, 2017)では0.95 precision, 0.94 recallであった。

  - shadow model が target model と同様に構成されるという仮定を緩和した。異なる構造・パラメータで学習しているが同水準の攻撃を達成。target model がどのML model の構造か知らなくとも攻撃できる shadow model training の方法を提案する。

- Adversary2: target modelの訓練データの従う分布と同じ分布に従うデータを持たないと仮定する。target model の構造も知らない。1つ前よりも現実的な設定である。

  - この設定において、 data transferring attack を提案する。1 shadow model で異なるデータセットを学習する。target model のふるまいを模倣するわけではない。単純にデータ点が訓練されているか否かを把握する。
  
  - data transferring attack によって、攻撃者はtarget model にクエリを投げてわざわざデータ生成する必要がない。既存研究(Shokri et al , 2017)では1つのデータを生成するのに平均156回のクエリを必要とするなど、我々の攻撃手法が効率的であることがわかる。クエリが少ないのだからMLaaS provider にも検知されにくい。
  
  - 実験結果により、mebership inference attack が依然成功することがわかる。few percentage のdrop。全く異なるデータセットでも攻撃が成功することもわかった。20 News groups 訓練モデルを CIFAR-100が画像データセットを使って 0.94 precision, 0.93 recallの攻撃を行った。
  
- Adversary 3: shadow models を用いない。target data points を target model にクエリしたときに得られる posterior にのみ依存する。訓練手続きが必要ない。target model の posterior 上の maximum and entropyを用いる。これはデータ点をtraining かnon-trainingかを十分に分離できる。具体的な攻撃手法とするため、閾値を選択する方法を提案する。実験は単純な攻撃でも複数のデータセット上で効率よく攻撃できることを示す。

- これらすべての実験ではmembership inference が単純かつ効率的にできることを示す。ML models にとって厳しいリスクであることを実証する。

### Defense.



## PRELIMINARIES

### A. Membership Inference Against Machine Learning Models

### B. Datasets Description

#### News.

#### Face.

## TOWARDS MODEL INDEPENDENT MEMBERSHIP INFERENCE ATTACKS (ADVERSARY 1)

### A. Threat Model

### B. One Shadow Model

#### Methodology.

#### Experimental Setup.

#### Results.

#### Evaluation on MLaaS

### C. Target Model Structure

#### Hyperparameters.

#### Target Model’s Algorithm.

## TOWARDS DATA INDEPENDENT MEMBERSHIP INFERENCE ATTACKS (ADVERSARY 2)

### A. Threat Model

### B. Methodology

### C. Evaluation

#### Experimental Setup.

#### Results.

#### Reasoning.

### D. Evaluation On MLaaS

## MODEL AND DATA INDEPENDENT MEMBERSHIP INFERENCE ATTACK WITHOUT TRAINING (ADVERSARY 3)

### A. Threat Model

### B. Methodology

#### Threshold Choosing.

### C. Evaluation

#### Experimental Setup.

#### Results.

### D. Comparison of the Three Attacks

## D. Comparison of the Three Attacks

### A. Dropout

#### Methodology.

#### Evaluation.

### B. Model Stacking

#### Methodology.

#### Evaluation.

## RELATED WORK

#### Membership Inference. 

#### Membership Inference Against Machine Learning.

#### Attacks Against Machine Learning.

#### Privacy-Preserving Machine Learning. 

## CONCLUSION
