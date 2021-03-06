> タイトル<br>

<br>

https://openreview.net/forum?id=uAX8q61EVRu  
モノラル音声からのバイノーラル音声の脳内合成  


***

> 論文リンク<br>

<br>

記入欄
***

> 要約メモ<br>

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

> 本文直訳

<br>

### abstract

本研究では，現実的で空間的に正確なバイノーラルサウンドをリアルタイムで生成できる，バイノーラルサウンド合成のためのニューラルレンダリング手法を提案する．このネットワークは，1チャンネルの音源を入力とし，音源に対するリスナーの相対的な位置と向きを条件として，2チャンネルのバイノーラルサウンドを合成して出力する．本研究では，生の波形に対するl2-lossの欠点を理論的に検討し，この欠点を克服する改良型l2-lossを導入した．  
実証的な評価では，我々のアプローチが，（実際の録音で測定された）空間的に正確な波形出力を生成する最初の方法であり，定量的にも知覚的な研究においても，既存のアプローチをかなりのマージンで上回ることを立証した．データセットとコードはオンラインで入手可能です。

### introduction
拡張現実や仮想現実における人工的な空間の増加に伴い、正確な空間化されたオーディオの効率的な制作が必要となっています。  
空間聴覚（両耳の信号から空間的な手がかりを解釈する能力）は、3D環境での方向性を決めるのに役立つだけでなく、脳に一致した音響と視覚の入力を与えることで、空間への没入感を確立します（Hendrix & Barfield, 1996）。  
バイノーラルオーディオ（左耳と右耳）は、複数人での会話でも私たちを導いてくれます。ビデオ通話で複数の人が話していて、会話についていくのが難しいというシナリオを考えてみましょう。実際の環境で同じ状況に置かれた場合、私たちは難なく個人のスピーチに集中することができます(Hawley et al., 2004)。実際、シーン理解のための入力モダリティとしては、視覚よりも聴覚の方が優先されます。  
(1) 聴覚刺激は視覚刺激に比べて反応時間が速い (Jose & Praveen, 2010)   
(2) 聴覚は、視覚の方向性とは対照的に、空間の周囲を把握することができる。  
これらの理由から、正確な2値信号の生成は、人工的な空間への完全な没入に不可欠である。  

バイノーラルオーディオ生成のほとんどのアプローチは、伝統的なデジタル信号処理（DSP）技術に依存しており、頭部関連の伝達関数、室内音響、周囲の雑音などの各コンポーネントは、線形時不変システム（LTI）としてモデル化されます（Saviojaら、1999年、Zotkinら、2004年、Sunderら、2015年、Zhangら、2017年）。  
これらの線形系はよく理解されており、数学的にモデル化することが比較的容易で、知覚的にもっともらしい結果が得られることが示されており、これが今でも広く使用されている理由である。しかし、実際の音響伝搬には、LTIシステムでは適切にモデル化できない非線形波動効果があります。その結果、DSPアプローチは、動的なシナリオにおいて知覚的な信憑性を達成できず（Brinkmann et al.  

本論文では、正確で精密なバイノーラルオーディオを効率的に合成することで、これらの制限の多くを克服するエンドツーエンドの神経合成アプローチを紹介します。このエンド・ツー・エンドの学習方式は、音波の伝搬による線形および非線形効果を自然に捉え、完全な畳み込み方式であるため、コモディティハードウェア上で効率的に実行できます。  
我々の主な貢献は、  
(1)既存の技術を凌駕する新しい2値化モデル、  
(2)生の波形に対する `2-loss' の欠点の分析と、これらの欠点を緩和する新しいloss、  
(3)無響室で撮影された実世界のバイノーラルデータセット  
です。

### related work
最新のDSP技術では，バイノーラルサウンドの空間化を，それぞれがLTIシステムである音響コンポーネントのスタックとしてアプローチしています．部屋のインパルス応答の正確な波動シミュレーションは、計算コストが高く、詳細な幾何学的情報と材料情報が必要なため、ほとんどのリアルタイムシステムは簡略化された幾何学的モデルに依存しています（Valim ¨ aki et al.   
頭部関連の伝達関数は無響室で測定され(Li & Peissig, 2020)、高品質な空間化には約10kの異なる空間位置でのバイノーラル録音が必要です(Armstrong et al., 2018)。バイノーラルオーディオを生成するために、DSPベースのバイノーラルレンダラーは通常、これらのコンポーネントインパルス応答との一連のコンボリューションを実行します（Savioja et al., 1999; Zotkin et al., 2004; Sunder et al., 2015; Zhang et al., 2017）。より詳細な議論については、付録A.4を参照してください。  

音声合成での成功（Wang et al., 2017）を受けて、ニューラルネットワークは最近、オーディオ生成のために注目を集めた。ほとんどのアプローチは周波数領域のモデルに焦点を当てていますが（Choi et al., 2018; Vasquez & Lewis, 2019）、生の波形モデルは、高周波のオーディオ信号の長距離依存性をモデル化することが難しいため、長い間無視されていました。  
しかし、WaveNet（Van Den Oord et al., 2016）の成功により、直接的な波動モデルへの関心が高まり（Fu et al., 2017; Luo & Mesgarani, 2018; Donahue et al., 2019）、スピーチエンハンスメント（Defossez et al., 2020）やノイズ除去（Rethage et al., 2018）、音声合成（Kalchbrenner et al., 2018）、音楽スタイル翻訳（Mor et al., 2019）において大きな改善を示しています。  
さらに最近では、神経的な音の空間化に向けた最初のステップが行われている。  
Gebruら（2021）は、生の波形で学習したニューラルネットワークによって、HRTFを暗黙的に学習できることを示した。  
視覚情報を条件とした空間的な音の予測に着目し、Morgadoら（2018）による研究では、360◦ビデオを条件とした音の空間化を目指している。  
しかし、彼らの研究は一次アンビソニックスに限定されており、詳細なバイノーラル効果をモデル化することはできません。  
より密接に関連するのは、Gao & Grauman (2019b)による2.5Dビジュアルサウンドシステムに由来する一連の論文である。  
この作品では、物体の位置が音の発生源に寄与するようなビデオフレームの埋め込みを条件として、バイノーラルオーディオを生成しています。Yang et al. (2020); Lu et al. (2019); Zhou et al. (2020) も同じアイデアに基づいています。  
残念ながら、これらの研究に共通しているのは、空間化タスクをアップミキシング問題として提起していること、すなわち、これらのモデルは、左耳と右耳のバイノーラル録音の混合物を擬似的にモノラル入力として学習されていることです。これらの方法では、音源とリスナーの位置の違いによって生じる時間遅延や残響効果をモデル化することができません。  

### A NEURAL NETWORK FOR BINAURAL SYNTHESIS
ここでは，長さTのモノラル（シングルチャンネル）信号x1:T = (x1, ... , xT )を，条件付けの時間信号c1:Tを与えて，リスナーの左耳と右耳を表すバイノーラル（ステレオ）信号y (l) 1:T , y (r) 1:Tに変換するという問題を考える。  
この条件付け信号は、ソースとリスナーのそれぞれの位置と方向である。ここで，xt，およびそれに対応するy (l) tとy (r) tは，時間tにおけるオーディオ・サンプルを表すスカラーである。 言い換えれば，我々は，関数を生成することを目的としている。  

ここで，∆は時間的受容野である。それぞれのct∈R14には、ソースとリスナーの3次元位置（それぞれ3つの値）と、それらの方向を四元数（それぞれ4つの値）で表しています。実際には、cは入出力信号x1:Tやy(l/r)1:Tよりも低い周波数であることが多く、ソースとリスナーの位置は48kHzではなく、30-120Hzなどの一般的なカメラのフレームレートで更新される可能性が高いことに注意してください。表記を簡単にするために、cはすでにオーディオ信号と同じ時間解像度にアップサンプリングされていると仮定します。  

全体の枠組みを図1に示します。ニューラル・タイム・ワーピング・モジュールは，まず1チャンネルの入力信号x1:Tを2チャンネルの信号x(l/r)1:Tに変換します（チャンネルは左耳と右耳を表します）。  
タイムワーピングは、音源とリスナーの間の距離に起因する粗い時間的効果と、左右の耳への音の到達時間の違いを補正する。  
図1の2番目のブロックは、N個の層のスタックで、それぞれの層は、条件付き超コンボリューション（セクション2.2参照）に続いて、より高い周波数をモデル化するのに有効であることが示されているサイン・アクティベーションを行います（Sitzmann et al.、2020）。  
WaveNetの設計に従って、カーネルサイズ2を使用し、各層の拡張係数を2倍にして受容野を増やしています。  
この一時的なConvNetは、部屋の残響、頭や耳の形状、頭の向きの変化などによって生じる微妙な効果をモデル化します。  

###  NEURAL TIME WARPING
タイムワーピングは、ソースの時間的シーケンスをターゲットのシーケンスにマッピングするタスクであり、時間的信号処理において長い伝統を持っています。  
最も顕著なのは、ダイナミック・タイム・ワーピング（DTW）が、音声認識（Juang, 1984）や音声検索（Deng & Leung, 2015）などのタスクに応用されていることです。  
DTWは、ソース信号x1:Tをターゲット信号xˆ1:Tにワープさせるワープフィールドρ1:Tを、信号間の距離が最小になるように見つけることを特徴とする。


### evaluation
> dataset  

男性4名、女性4名の計8名のスピーカーから、モノラルとバイノーラルのペアデータを48kHzで計2時間録音しました。聴取者は、耳にバイノーラルマイクを装着したマネキンです。参加者は半径1.5mの円を描くようにマネキンの周りを歩き、台本のない会話をしてもらいました。  
OptiTrackシステムを用いて，キャプチャ中の音源とリスナーの位置と向きを追跡しました。私たちの知る限り，このようなサイズの自然界（無響室で録音されていない）のバイノーラルデータセットは，これが唯一のものです。各参加者の検証用シーケンスと最後の2分間をテストデータとして使用し，残りのデータでモデルを学習します。より詳細な説明は，付録A.5を参照してください。

> neteork architecture  

WarpNetのアーキテクチャは、セクション2.1で説明したとおりです。時間的な畳み込みネットワークは、3つの連続したブロックで構成されています。  
各ブロックは、64チャンネル、カーネルサイズ2のハイパーコンボリューション層を10個重ねたもので、各層の後にダイレーションサイズを2倍にしています。  
Adamオプティマイザーを用いて，100回のエポックでモデルを学習します．2つのエポックの間にトレーニングセットの損失が改善されなかった場合、学習率は低下します。  
推論の結果，このモデルはリアルタイムでバイノーラル音声を生成することができます．  


### conclusion
私たちのニューラルサウンドバイノーラル化アプローチは、従来の最先端のバイノーラル化手法と比較して説得力のあるパフォーマンスを示す、  
初めての純粋なデータ駆動型のエンドツーエンドモデルです。我々のモデルの有効性は、定量的にも、知覚的なユーザー調査でも示すことができました。さらに、このタスクだけでなく、他の生成的なオーディオ問題にも影響を与える、生の波形に対する`2-最適化の基本的な問題を明らかにし、軽減することができました。

***
