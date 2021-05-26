> タイトル<br>
Rethinking Embedding Coupling in Pre-trained Language Models  
学習済み言語モデルへの結合の埋め込みに関する再考
<br>

記入欄
***

> 論文リンク<br>
https://openreview.net/forum?id=xpFFI_NtgpW
<br>

記入欄
***

> 要約メモ<br>
本稿では、最新の学習済み言語モデルにおいて、入力埋め込みと出力埋め込みの間で重みを共有するという標準的な手法を再評価する。その結果、非結合型の埋め込みによってモデリングの柔軟性が向上し、多言語モデルの入力埋め込みにおけるパラメータ割り当ての効率を大幅に改善できることを示した。入力エンベッディングのパラメータをTransformer層で再配分することで、微調整時に同じ数のパラメータで標準的な自然言語理解タスクの性能を劇的に向上させることができる。また、出力エンベッディングに追加の容量を割り当てることで、出力エンベッディングが事前学習後に破棄されたとしても、微調整の段階でモデルに持続的な利益をもたらすことを示す。これは、出力エンベッディングを大きくすることで、モデルの最後の層が訓練前のタスクに過度に特化することを防ぎ、Transformerの表現をより一般的なものにして、他のタスクや言語への移植性を高めることができるという分析結果です。これらの知見を活用することで、微調整段階でパラメータ数を増やすことなく、XTREMEベンチマークで強力なパフォーマンスを達成するモデルを学習することができます。
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