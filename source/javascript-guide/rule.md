title: "Javascriptコーディングルール"
description: "JavascriptとHTML＆CSSのルールの違いの説明"
---

基本的なルール策定の考え方は[HTML](/html-guide/rule.html)などと同じです。
しかし大きく違うのは「Javascript」はスクリプト言語というコードだということです

Javascriptのコーディングは人によって違うので「Javascript」の場合はコーディングスタイル（記述方法）を決めます。

例えば「if文」

```javascript
if (boolean) {
  return 0;
}

if(boolean)
  return 1;

```

というように同じファイルに記述方法が複数あるとコードがとても読みずらいです。
このようなコーディンスタイルが「バグの原因」となります。
バグの発生を防ぐためにもコーディングスタイルを統一していきましょう。

##命名規則
セマンティックスな命名が一番ですが、
文章のように長くなるとそれだけでコードが読みにくくなります。
逆に短くしすぎても分けがわからなくなります。

原因は文脈を理解できていないためです。
これを解決するのは文脈を理解しそれにあった名前をつけることです。

例えば「クリックするといろが赤く変わるボタン」だと

```javascript
var buttonClickChangeColorRed = function(){};
```

これだと長すぎます文脈（コンテキスト）で重要なのは「色が変わる」ということです。

```javascript
var changeColor = function(){};
```

こうすることで色が変化するのがわかると思います。
また汎用性の高いコードになると思います。

##実装方法

サイトを制作していくと、イロイロな機能を実装していくとファイルサイズが膨大になってしまうことがあります。
実際私も何千行というJavascriptファイルを見たことがあります。

こうなってしまうとメンテナンスもできないし、パフォーマンスもとても悪くなってイケてないサイトになってしまいます。
こうならないためにもJavascriptコードを書くときは考え方もそうですが、切り分けて実装するのがいいと思います。

その実装方法ですが方法はいくつかあると思います。
人によってJavascriptの技術レベルが違うと思うので、プロジェクトにあった実装方法決めていきます。
大きく以下の２つに分けることができると思います。

- 命令型
- 宣言型（関数型）
- オブジェクト指向

私は「宣言型+オブジェクト指向」を強く勧めますがJavascriptを理解していないと実装は難しいと思います。
では「命令型」で進めるのことがおおいと思いますが、ここで注意が必要です。
「命令型」で書いていくとコードが膨大になってカオスなJavascriptになってしまいます。
どう書くかを最初に決めることはとても重要なのでしっかり決めていきましょう。

##プラグイン

プラグインを使用するときに基本となるライブラリを決めておきます。
「jQuery」は一般的で皆さん使用されているかと思います。
このように必ず使うプラグインを最初に決めておくことで、
今使っているプラグインがなにでライセンスがなにでと管理もとてもしやすくなります。

これを決めていないとプラグインを選ぶのに時間がかかり無駄な時間になってしまいます。
あとプラグインをわざわざ使用しなくても実装できるものはプラグインを読むと多少なりとパフォーマンスが下がるので、
実装可能なものは自分で作りましょう。

##まとめ

Javascriptの場合は使用も含め最初に決めることがHTMLやCSSに比べ多いですが、
このルールを決めればさくさく開発が進むはずです。
ポイントとしては他と同じですが文脈（コンテキスト）を理解し論理を考え細かく細分化していくということです。
自分なりのルールを考えてみましょう。
