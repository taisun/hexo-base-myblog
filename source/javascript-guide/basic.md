title: "Javascriptの基本"
date: 2015-05-15 16:47:36
---
難しくいうと、
> Javascriptはインタプリタ言語です。
> インタプリタとは実行環境上でコードを動かすことができるため開発がしやすい言語です。

なんのことかよくわからないので要約すると「簡単にブラウザなどの環境で実行ができて、開発しやすく導入しやすい」ということです。
(あってるかな？)

基本的HTMLとCSSを操作するための言語です。
特徴としては上記では難しくいっていますがJavascriptはスクリプト言語です。
スクリプト言語とはコンパイルしなくても実行できる言語のことです。

ここでは基本的な記述方法の紹介とJavascriptの性質についてかきます。

##記述方法

以下は基本的な使用するものをあげました他にもたくさんありますが全部は書くことができないのでよく使用するものだけあげています。

###宣言文

```javascript

/**
 * 変数宣言文
 */
var 変数名;
var 変数名, 変数名;　//複数

/*
 * 関数宣言文
 */

function 関数名(引数, 引数, ...){
  //実行内容
}


var 関数 = function(引数, 引数, ...){ //リテラル式
  //実行内容
}
```

###制御文

```javascript
/**
 * if-else文
 */

if(条件1){
  //実行内容
} else if(条件2) {
  //実行内容
} else {
  //実行内容
}

/**
 * switch-case文
 */

switch (式){
  case 式1:
    文
    break;

  case 式2:
    文
    break;

  default:
    文
    break;
}
```
###繰り返し文

```javascript
/**
 * while文
 */

while(条件){
  //実行内容
}

/**
 * do-while文
 */
do {
  文
} while (条件);

/**
 * for文
 */
for(初期化式; 条件式; 更新式){
  文
}

/**
 * for-in文
 */
for(変数 in オブジェクト式){
  文
}

/**
 * for-each-in文
 */
for each(変数 in オブジェクト式){
  文
}
```
##その他式

```javascript
/**
 * break文
 * ループ処理を途中で抜けます
 */
break;

/**
 * continue文
 * 途中にcontinueをかくとそれ以降は無視して最初の条件に戻ります。
 */
continue;

/**
 * ジャンプ式
 * breakは一つのループしか抜けることができません複数ある場合はこの式を使います。
 */
outer:
while () {
  while () {
    break outer; //outerに戻ることができる
  }
}


/**
 * return文
 * 戻り値を返します。
 */
continue;

```

##Javascriptの性質
Javascriptはドット記法で記述します。

```javascript
console.log('test');
```

上記のコードのように「conole」と「log」をドットでつないでいます。
この記法がJavascriptです。
コードで説明すると

```javascript
var func = function(){}

func.prototype = {
  log: function(){};
}

var console = new func;
console.log();
```

このようになっています。
ちなみに、この書き方は「プロトタイプ継承」という書き方です。
なんのこっちゃよくわからないというかたもいると思います。
文章でいうと、

<div class="em">「console」の中の「log」という関数を呼ぶ</div>

ということです。
このドットは鎖ののようにつないで行くことができます。

このドットを「チェーン」といいます。

このようにチェーンをつないでいくのがJavascriptの性質です。

##スコープチェーン

スコープチェーンとは先ほど書いたコードを元に説明します。

```javascript
var func = function(){}

func.prototype = {
  log: function(){};
}

var console = new func;
console.log();
```

このコードはなにをしているかというと、
まず「func」という**オブジェクト**を作ってその中に**プロトタイプオブジェクト**の「log」を作って、「console」という変数の中に**newオブジェクト**をつくって継承しています。

なんかややこしいですよね、
スコープチェーンは「console」のオブジェクトからみた「log」です。
「console.log();」を実行すると「console」自体には「log」というオブジェクトを持っていないので、
継承元の「func」の中をさがして「log」見つけ実行します。

これがスコープチェンです。
ようするに「自分が持っていないものを自分以外のところをさがして参照する」ことです。
