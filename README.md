<div id="top"></div>

## 使用技術一覧
<!-- シールド一覧 -->
<p style="display: inline">
  <img src="https://img.shields.io/badge/-Html5-E34F26.svg?logo=html5&style=plastic">
  <img src="https://img.shields.io/badge/-Css3-1572B6.svg?logo=css3&style=plastic">
  <img src="https://img.shields.io/badge/-Javascript-F7DF1E.svg?logo=javascript&style=plastic">
</p>

## 目次

1. [プロジェクトについて](#プロジェクトについて)
2. [作成の経緯](#作成の経緯)
3. [背景知識](#背景知識)
4. [使用方法](#使用方法)
5. [既知の問題](#既知の問題)


## プロジェクト名
Coffee-fitting

## プロジェクトについて
コーヒーの味を維持したまま、出来上がり量を変化させる変換器

## 作成の経緯
「美味しい淹れ方はあるんだけど、200mlじゃなくて300ml作りたいんだよな...」ということがしばしばあり、手軽に量の変換ができるツールがあれば便利だと思ったので作りました。

## 背景知識
この変換器が行っている変換処理の根幹は、「変換前と変換後の最終量から倍率を求め、各注湯プロセスに倍率をかける」という単純な比率変換です。
ここでは、「この比率変換がなぜ味のキープにつながるのか」という点について述べます(コーヒー自体の理論に興味がない方は本節を読み飛ばしても大丈夫です)。

## 使用方法
本リポジトリのファイルをローカルに引っぱって個々で利用することも可能ですし、ブラウザで使用することもできます
([http://hiruge-tools.com/Coffee-fitting](http://hiruge-tools.com/Coffee-fitting/))

より詳細な変換器の使用方法は、[使い方ページ](http://hiruge-tools.com/Coffee-fitting/how-to-use.html)をご覧ください(後でreadmeにも追加予定です)

## 既知の問題
- 湯の抜け
  - この変換器では、豆量変化による流速(湯の抜け)の変化が加味されていません。単純な比率変換であることを理解した上で、変換結果を参考にしてください。
  - 湯の抜けが考慮されていないため、投数が少ない(3投以下)とかなり無理のあるレシピになってしまうことがあります。投数の多いレシピでお試しください。

なお、この問題に対する改善を検討中ですが、現在具体的な改善の目処は立っていません。
