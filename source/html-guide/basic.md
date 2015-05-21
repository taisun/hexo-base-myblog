title: "HTML5基礎&思考"
date: 2015-05-14 19:21:07
comments: false
---
ここではHTML5の基礎について書いていきます。

##HTML5について
2014年10月28日に正式勧告されました。
2016年にはHTML5.1も勧告予定です。

ここではHTML5（一部5.1）の使い方について書いていきます。

HTML5では廃止になったタグや変更になった箇所があります。
各タグの使用には注意が必要です。

HTML5の各タグには意味があり文脈（コンテキスト）に合わせてタグを選択し使用しなければいけません。

例えば
`<strong>`タグは「強い強調」という意味があります。

HTML4のように太字にするためだけに使用するのはいけません。
場合によりますが、`小見出し`や`テーブルキャプション`に使うと良いでしょう。

各タグの意味＆使用方法などについては**[W３C](http://momdo.github.io/html5/Overview.html)**や**[Mozilla](https://developer.mozilla.org/ja/docs/Web/HTML/HTML5)**などをご覧ください。

##XHTML/HTML4の違い

HTML5とXHTMLのちがいですが大きく違うのは

- シングルタグに閉じタグをつけない
- `Docutype宣言`の記述方法
- `meta`・`style`・`script`タグの使用方法  etc...

などです。
上記に書いたものは特に注意したいものなのでコーディングする時は意識し書くようにしてください。

##基本的なマークアップ（HTML5）について

HTML5を使用した基本的なマークアップについて記述します。
HTMLは構造体です。

なので構造を崩すようなマークアップはしてはいけません。
例えば以下のような例です。

**大量な`<br>`＆スペース(`&nbsp;`)を使用してレイアウトしている**

```html
<br><br><br><br><br>
<p>見出し&nbsp;&nbsp;&nbsp;重要</p>
```

これはなぜいけないかというと、
タグの意味として使用方法が間違っていて構造体ではないからです。
`<br>`は文章の改行、`&nbsp;`は半角ではなくて「Non-breaking Space」なので自動的な改行を防ぐ物です。

このような意味を理解してマークアップをしないと構造体が崩れてしまいメンテナンスができないカオスなサイトになってしまいます。
そのためレイアウト目的では絶対に使用しないでください。

他にもHTML5のタグには意味がありHTMLは構造体なので
レイアウト目的で使用してはいけないタグがいくつかあります。

- article
- section
- heder
- nav
- footer
- aside   etc...

上記のタグは全て意味があり使用条件があるので`div`のようにレイアウト目的で使用はできません。
構造を考えて使用しなければいけません。

- 詳しくは[構造設計](/html-structural)のページで書いています。

構造体を意識してHTML5のコーディングをすることでイケてるマークアップに自然となっていくでしょう。

##HTML5基礎構造

基本的な構造＆パーツの記述例を書いていきます。

###html

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
  </head>
  <body>
  </body>
</html>
```

<br>
###Head

```html
<head>
	<meta charset="utf-8">
	<meta name="Author" content="サイト名">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<title>サイトタイトル</title>
	<meta name="description" content="サイトの説明">
	<meta name="keywords" content="検索ワード">
	<link rel="stylesheet" href="">
	<link rel="home" href="サイトURL">
	<link rel="index" href="サイトマップ">
</head>
```

- `script`タグは`body`閉じタグの直前に記述する。
- そのほか`ogp`等は`title`たぐのあとに記述する。
- ピンチをしない場合は`viewport`の`content`に`user-scalable=no`を追記する。
<br>

###Favicon

```html
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
<link rel="apple-touch-icon" href="apple-touch-icon.png">
<link rel="apple-touch-icon" sizes="57x57" href="apple-touch-icon-57x57.png">
<link rel="apple-touch-icon" sizes="72x72" href="apple-touch-icon-72x72.png">
<link rel="apple-touch-icon" sizes="76x76" href="apple-touch-icon-76x76.png">
<link rel="apple-touch-icon" sizes="114x114" href="apple-touch-icon-114x114.png">
<link rel="apple-touch-icon" sizes="120x120" href="apple-touch-icon-120x120.png">
<link rel="apple-touch-icon" sizes="144x144" href="apple-touch-icon-144x144.png">
<link rel="apple-touch-icon" sizes="152x152" href="apple-touch-icon-152x152.png">
```

- サイズなどは常に変わるので記述には注意が必要。

<br>
###Header

```html
<header class="l-header" role="banner">
		...省略
</header>
```

<br>

###Nnavigation

```html
<nav class="l-globalNav" role="navigation">
  <ul class="p-gloNav" roel="menu">
    <li class="p-gloNav__item"><a href="xxx.html">メニュー１</a></li>
    <li class="p-gloNav__item"><a href="xxx.html">メニュー２</a></li>
    ...省略
  </ul>
</nav>
```

- 入れ子のメニューになる時は`dl`を使用する。
<br>

###Main Contents

```html
<main class="l-main" role="main">
  <article class="l-contents">
    <h1 aria-level="1" class="c-heading__lvOne">見出し1</h1>
    <p>テキストテキストテキストテキスト</p>
    <section classs="l-contents">
      <h2 aria-level="2" class="c-heading__lvOne">見出し2</h2>
      ...省略
    </section>
    <section classs="l-contents">
      <h2 aria-level="2" class="c-heading__lvOne">見出し2</h2>
      ...省略
    </section>
  </article>
</main>
```

- `section`や`article`を使用する時はレイアウト目的（`div`と同じように）使用してはいけない。
- `section`&`article`を入れ子の構造にする時は見出しをつけること。
　`section` > `section`のようになると構造的にも文脈（コンテキスト）としてもおかしいので必ず、見出しをつけて区別すること。
- 同じレベルの要素が連続している時は入れ子にしてはいけない。
<br>
###Sidebar

```html
<div class="l-sidebar">
  <section class="l-contents">
    <h2 aria-level="2" class="c-heading__lvOne">関連情報</h2>
    ...省略
  </section>
  <aside class="l-contents" role="complementary">
    <a class="c-banner" href="">バナー</a>
    ...省略
  </aside>
</div>
```
- サイドバーは要素が何が入るかわからないため`aside`は使用しない。
<br>

###Footer

```html
<footer class="l-footer" role="contetinfo">
  ...省略
</footer>
```
