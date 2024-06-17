# プロジェクト概要:Coffee-fitting

コーヒーの味を維持したまま、出来上がり量を変化させる変換器です。

## 使用技術一覧
<!-- シールド一覧 -->
<p style="display: inline">
  <img src="https://img.shields.io/badge/-Html5-E34F26.svg?logo=html5&style=plastic">
  <img src="https://img.shields.io/badge/-Css3-1572B6.svg?logo=css3&style=plastic">
  <img src="https://img.shields.io/badge/-Javascript-F7DF1E.svg?logo=javascript&style=plastic">
  <img src="https://img.shields.io/badge/-Jquery-0769AD.svg?logo=jquery&style=plastic">
</p>

## 目次

1. [作成の経緯](#作成の経緯)
2. [基本原理と背景知識](#基本原理と背景知識)
3. [使用方法](#使用方法)
4. [既知の問題](#既知の問題)
5. [今後実装しようとしている機能](#今後実装しようとしている機能)
6. [不具合等](#不具合等)

## 作成の経緯

「美味しいいれ方はあるんだけど、200mlじゃなくて300ml作りたいんだよな...」ということがしばしばあり、手軽に量の変換ができるツールがあれば便利だと思ったので作りました。

## 基本原理と背景知識

この変換器が行っている変換処理の根幹は、「変換前と変換後の最終量から倍率を求め、各注湯プロセスに倍率をかける」という単純な比率変換です。

ここでは、「この比率変換がなぜ味のキープにつながるのか」という点について述べます(コーヒー自体の理論に興味がない方は本節を読み飛ばしても大丈夫です)。

<details>
<summary>単純な比率変換が味のキープに結びつく理由</summary>
  
まず、コーヒーの粉から溶け出す成分には、「溶け出す順番」というものがあります。

抽出の際には湯を注ぐので、親水性のものから疎水性のものという順番で溶け出してくるというわけです。

しかし溶け出す成分の種類はとても多く、それら一つ一つを特定してコントロールするということはほぼ不可能に近いです。

ですが、この溶け出す順番には経験則的にいわれているある程度の大まかな流れがあります。それは、 **「香り→酸味→甘み→苦味→雑味」** の順に溶け出すという流れです。下図のように、溶け出しやすさのピークがこの順番に来るというイメージですね。
<div align="center">
  <img src="images/how-to-description/extraction-graph.png" width="80%">
</div>

さて、本ツールを理解する上で重要なのは、 **「どの味をどれだけ抽出するか」** という点です。

「甘み」がピークの時点で大量に湯を注げば、甘味成分の多いコーヒーが全体量中の多くを占め、苦味が少なく、酸味や甘みの多いコーヒーになります。一方、「苦味」の時点で大量に湯を注げば、甘みの割合が比較的少なくなって甘みを感じにくくなります。

つまり本ツールでは、元レシピにおける各タイミングでの注湯配分を維持することで、「どの味が出やすいタイミングで」「全体量のどれだけを占める分注ぐのか」を維持し、コーヒーの味を保っているというわけです。

余談ですが、これは「抽出をどの程度進めるかによって味を決定できる」という話でもあり、一般的に好みの味を探る際には、湯温や用いる器具、粉の粒度などを調整することで抽出の進度を調整することで、理想の味を探るという方法が有効と思われます。

</details>

## 使用方法

本リポジトリのファイルをローカルに引っぱって個々で利用することも可能ですし、ブラウザで使用することもできます
([https://hiruge-tools.com](https://hiruge-tools.com))

<details>
<summary>より詳細な変換器の使用方法</summary>

[使い方ページ](https://hiruge-tools.com/how-to-use.html)にも同様の以下の説明と同様の内容が書いてあります。

1. **変換前レシピ入力欄**：変換する前のレシピの情報を入力します。

   <img src="images/how-to-description/originRecipeForm.png" width="40%">

   投数、豆の量、そして各投入段階の経過時間と注湯量を記入します。<br>
      ※ 投数を入力すると、その分だけレシピ入力欄が生成されます。<br>
   アイスコーヒーを入れたい場合は、アイスモードをONにし、氷量を入力します。

   <img src="images/how-to-description/originRecipeForm[ice-mode].png" width="40%">

2. **変換目標入力欄**：変換後のレシピの情報を入力します。

   <img src="images/how-to-description/targetParameterForm[bean,water].png" width="40%">

   目標とする豆の量、総湯量、そして豆と湯の比率を指定します。

   **倍率変換**

     変換目標の入力が手間かと思い、倍率を入力するだけで変換できる機能を実装しました

      <img src="images/how-to-description/targetParameterForm[convertRate].png" width="40%">

   **入力補助**

     豆量と総湯量の両方が入力されると自動的に比率が計算・入力されます。<br>
     また、豆量あるいは総湯量のいずれかが入力された状態で比率が入力されると、もう一方が更新されます。<br>
     クリアボタンを押すと、変換目標入力欄の値が全てクリアされます。

      ※ 入力補助機能がある都合上、豆量・総湯量・比率が全て入力されていると目標値の変更が難しくなる問題を確認したため本機能を実装しました。

   **蒸らし固定ボタン**

      蒸らし固定は基本的にONをオススメします。<br>
      経験則ですが、蒸らし湯量の変化が味に与える影響は大きいものと見られます。<br>
      (大幅な最終量変化がある場合は固定OFFでも良いかも知れません)

3. **変換後レシピの出力**：変換されたレシピが表形式で表示されます。

   <img src="images/how-to-description/convertedRecipe.png" width="40%">   

4. **ストップウォッチ機能**：抽出時の経過時間を計測する機能です。

   <img src="images/how-to-description/stopWatch.png" width="40%">

   スタートボタンを押すと計測が始まり、ストップボタンを押すと計測が終了します。

</details>

## 既知の問題

### 湯の抜け
  
この変換器では、豆量変化による流速(湯の抜け)の変化が加味されていません。単純な比率変換であることを理解した上で、変換結果を参考にしてください。<br>
湯の抜けが考慮されていないため、投数が少ない(3投以下)とかなり無理のあるレシピになってしまうことがあります。投数の多いレシピでお試しください。

なお、この問題に対する改善を検討中ですが、現在具体的な改善の目処は立っていません。

## 今後実装しようとしている機能

### プリセットレシピの呼び出し機能
  
4:6メソッドのような有名なレシピをプリセットから呼び出して、変換元として利用できる機能を実装しようと考えています
  
## 不具合等

バグ修正等はGitHubの[issue](https://github.com/Hiruge-1/Coffee-fitting/issues)まで連絡ください。
