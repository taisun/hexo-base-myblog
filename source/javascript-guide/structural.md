title: "Javascriptの設計"
date: 2015-05-15 16:47:11
---

JavascriptもHTML/CSS共に設計はとてもじゅうようです。
ここでは文脈（コンテキスト）と論理を意識したコード設計について書いていきます。

Javascriptは普通に書いていくとだらだらと長く読みにくいコードになってしまいます。
ぞくにいうスパゲッティーコードというやつです。

そうならないように各機能の文脈（コンテキスト）を読み取り、適切な粒度に分割していきます。
考え方は論理通りにプログラミングすることです。

Javascriptのまとまりは「ブロック」といいます。
このブロックを利用して分割していけば読みやすく、解りやすく、メンテナンスしやすいコードになります。
「関数」や「配列」はブロックです。
これを使用していきます。

##方法

方法としては「関数型」と「オブジェクト指向」です。
クラスオブジェクト（1つのまとまり）をつくって関数で機能を分割していく方法です。
しかし関数型とかオブジェクト指向とかよく分からないという方が多いと思います。
少しそのあたりを説明していきます。

##命令型と宣言型（関数型）
通常のJavascriptのコードは以下のように考えて書いていく方が多いと思います。

<div class="em-none">Aの高さを取得して、次にBの高さを取得して足して、その次に...</div>

この考えで書いていくとダラダラとしたコードになってしまったり、分割するのが難しいです。
このコードのことを**命令型コード**といいます。

では関数型とはなんなのか以下にサンプルコード書いてみました。

「Aの高さを取得して、次にBの高さを取得して足す」というコードを書いてみます。

**命令型**

```javascript
var a = document.querySelector('.a'),
    b = document.querySelector('.b'),
    aHi = a.clientHeight,
    bHi = b.clientHeight;
    answer = aHi+bHi;

console.log(answer);
```

**関数型**

```javascript

var myfunc = {
  docs: function(a) {
    return document.querySelector(arg);
  },
  plus: function(b, c) {
    return b + c;
  },
  height: function(d) {
    return d.clientHeight
  }
}

var ary = ['.a', '.b'],
    el = ary.map(myfunc.docs),
    hi = el.map(myfunc.height),
    answer = hi.reduce(myfunc.plus);

console.log(answer);

```

少し難しいかもですがまとめることができました。
こうすることで汎用性の高いコードになります。
このような粒度を幾つもつくって管理していくとわかりやすくメンテナンスしやすくなります。

##まとめ

関数型にさらにオブジェクト指向の考えを
プラスするとさらに汎用性が増し良いコードになるでしょう。
分割した設計はパフォーマンス的にも軽くなるのでとても便利です。
ぜひ使ってみてください。
