> タイトル<br>
Efficient Transformers in Reinforcement Learning using Actor-Learner Distillation  
Actor-Learner Distillationを用いた強化学習における効率的なトランスフォーマー
<br>

記入欄
***

> 論文リンク<br>
https://openreview.net/forum?id=uR9LaO_QxF
<br>

記入欄
***

> 要約メモ<br>
ロボット工学などの多くの実世界のアプリケーションでは、電力や計算量に厳しい制約があり、強化学習（RL）エージェントの実行可能なモデルの複雑さが制限されています。同様に、多くの分散型RL環境では、アクティングはCPUのような加速しないハードウェア上で行われ、同様にモデルサイズが制限され、実験の実行時間が長くなるのを防いでいます。このような「アクター・レイテンシー」の制約は、最近の教師付き学習で大きな成果を上げているモデルの複雑さのスケールアップを妨げる大きな要因となっています。我々は、大容量のモデルを利用しつつ、アクティング時にシステムが課す制限内で動作できるようにするために、大容量の学習者モデルから小容量のアクターモデルに学習の進捗を転送する継続的な形式の蒸留を利用した「アクター・学習者蒸留」（ALD）手順を開発しました。ケーススタディとして、部分的に観測可能な環境の文脈でこの手順を開発しました。ここでは、変換モデルがLSTMよりも大幅に改善されていますが、その代償として計算量が大幅に増加しています。学習者に変換モデル、アクターにLSTMを用いて、いくつかの困難な記憶環境において、アクター-学習者蒸留法を用いることで、LSTMアクターモデルの高速な推論と短縮された総学習時間を維持しつつ、変換学習者モデルの明確なサンプル効率の向上をほぼ回復することを実証する。
<br>

記入欄
***

> どんなもの？<br>

<br>

記入欄
***

> 先行文献と比べてどこがすごい？

<br>

記入欄
***

> 技術や手法のキモは？

<br>

記入欄
***

> どうやって有効性を証明した？

<br>

記入欄
***

> 議論はある？

<br>

記入欄
***

> 分からない単語、調べた内容メモ

<br>

記入欄
***

> 参考リンク

<br>

記入欄
***