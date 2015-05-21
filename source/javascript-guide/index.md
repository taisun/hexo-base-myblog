title: "Javascriptガイドライン"
date: 2015-05-13 15:40:35
comments: false
---
Javascriptのガイドラインです。
基本はJavascriptですが一部「**[jQuery](https://jquery.com/)**」& 「**[undescoreJs](http://underscorejs.org/)**」などの記述もあります。
コーディングルール・命名規則などを記述していきます。

両方記述しますが、
命令型は基本として、宣言型を使用して記述していきたいです。

##[Javascriptコーディングルール設計＆思考](/javascript-guide/rule.html)
Javascriptコードの文脈（コンテキスト）を考えた命名規則、手法などのコーディングルールを書いております。

- [コーディングルール設計＆思考](/javascript-guide/rule.html)

##[Javascriptの基礎＆思考](/javascript-guide/basic.html)
Javascriptの基礎について書いています。
基本的な書き方(if・for・関数など)の例と説明をしています。

<!--一つのコードをベースにどう書いていくかを説明しています。-->

- [Javascriptの基礎＆思考](/javascript-guide/basic.html)

##[Javascriptの設計＆思考](/javascript-guide/structural.html)

Javascriptはしっかり設計しないと動作が遅くなってしまうため、
オブジェクト指向ベース宣言型コード（関数プログラミング）の手法につてい書いています。

<!--１つのコードをベースに書いていく。-->

- [Javascriptの設計](/javascript-guide/structural.html)

##[Javascriptのパフォーマンス＆テスト](/javascript-guide/performance.html)

JavascriptはDOM(Document Object Model)などを操作したり、DOM(Document Object Model)を生成したりするとコードが増えたりパーフォマンスが下がります。
<!--特に昨今ではスマートフォンなどの小型端末が普及しよりパーフォーマンスが重視されています。-->
パーフォーマンスを意識したコードやファイルの読み込みやより早いコードを書くためのテスト方法について書いています。
platoやjasmin＆karmaを使用したテスト

- [Javascriptのパフォーマンス＆テスト](/javascript-guide/performance.html)
