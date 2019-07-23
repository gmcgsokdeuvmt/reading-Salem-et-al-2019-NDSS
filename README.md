# reading-Salem-et-al-2019-NDSS

- Authors: Ahmed Salem, Yang Zhang, Mathias Humbert, Pascal Berrang, Mario Fritz, Michael Backes
- Title: ML-Leaks: Model and Data Independent Membership Inference Attacks and Defenses on Machine Learning Models.
- In: 26th Annual Network and Distributed System Security Symposium (NDSS 2019).
- Conference: NDSS - Network and Distributed System Security Symposium

# ML-Leaks: Model and Data Independent Membership Inference Attacks and Defenses on Machine Learning Models.

## Abstract

- 近年注目される機械学習。その核となるのは訓練データ。
- 大きな成功を背景に、インターネット企業は機械学習をサービスとして展開する。(Machine Learning as a Service)
- MLLaS 設定において、memership inference attack によって初めて訓練データの情報が抽出される可能性が示された。
- この問題は、セキュリティ・プライバシーに関係がある。

- 攻撃が実行可能であることは先行研究で示されてきたが、攻撃者に多くの仮定が存在する(multiple shadow models, knowledge of the target model structure, and having a dataset from same distribution as the target model's training data)。
- 我々は、この仮定を緩和する。コストが低くこれまでよりも厳しいリスクを提案する。
- 8つのデータセットを使用して、提案するドメインを超えた攻撃が可能であることを示す。

- 加えて、防御手法を提案する。MLモデルの有用性を高く維持しつつ広く membership inference attack を防ぐ。
