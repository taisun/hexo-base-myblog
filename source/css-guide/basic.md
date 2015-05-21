title: "CSS基礎"
description: "CSS&CSS3を使用した。CSSの書き方の基礎・CSSの優先順位・CSSの概念をまとめております。"
---

CSSとはCascading Style Sheetsの略でWebページのスタイルを指定するための言語です。

基本的に以下のように記述します。

```css
セレクタ {
  プロパティ: 値;
}
```

複数のセレクタを指定する場合は「,」で区切って記述します。

```html
セレクタ, セレクタ
```

記述方法はとても簡単だとおもいます。
ですがCSSは他の言語と同様にコードの上から下へ向かってブラウザが読み込みます。

その為後に書かれたコードが優先されます。
<br>
##セレクタ強度について

セレクタの指定方法でCSS優先度が違います。

<div class="em">セレクタ強度　＝　CSS優先度</div>

以下のコードで文字色を指定する場合の上からセレクタ強度が高い順にかいていきます

**HTML**

```html
<div id="changeBox">
  <p class="text">テキスト</div>
</div>
```

**CSS**

```css
#changeBox .text {
  color: red;
}

div .text {
  color: blue;
}

.text {
  color: yellow;
}

div p {
  color: green;
}

p {
  color: black;
}
```

このような順番で強度が決まってきます。

強い強度にするとパーツの汎用性が低くなりCSSが膨大になります。
逆に低くしすぎるとCSSが他のCSSによって汚染されてしまいます。
じゃあどうするのか？

- IDセレクタは使用しない。
- CSS汚染を防ぐために全てにクラスを着ける。

それでもCSS汚染することがあるので、
CSSの設計は念入りにする。

<br>
###CSSのプロパティの順番＆論理

セレクタ強度の重要性は分かったと思います。
それではプロパティはどうでしょうか？
プロパティは表示に関係しています。
そのため書く順番を意識することで、表示に影響します。

CSSのコードは上から下に読まれます。
そのとき以下のようなコードだと論理上どう表示されるでしょう。

```css
a {
  background-image: url(hoge.png);
  color: red;
  margin: 10px;
  display: block;
}
```

このコードはまず最初に「bacground-image」が指定され、
次に「color」「margin」「display」という順に設定されています。

回線速度が遅い環境では表示が一瞬でも崩れる可能性があります。
なぜな実際ブラウザ側では以下のように設定しているからです。


<div class="em">背景の画像取得 => 背景の画像表示 => テキストの色を設定 => 要素のマージン設定 => 要素をblockに設定</div>


そのことを考え、私は以下のような順番でプロパティを書いています。

- 1.表示に関するプロパティ
- 2.配置に関するプロパティ
- 3.ボックスモデルに関するプロパティ
- 4.背景に関するプロパティ
- 5.テキストに関するプロパティ
- 6.内容に関するプロパティ
- 7.ユーザーインターフェイスに関するプロパティ
- 8.アニメーションに関するプロパティ

最低限表示が崩れないように考えこのような順番にしています。

各詳しいプロパティは以下にを参照ください。

###表示に関するプロパティ
 * display
 * list-style
  - type
  - image
  - position
 * overflow
 * clip
 * visbilty
 * opacity

###配置に関するプロパティ
 * position
 * top
 * right
 * bottom
 * left
 * float
 * clear
 * z-index
 * transform

###ボックスモデルに関するプロパティ
 * width
 * height
 * margin
 * padding
 * border
  - width
  - style
  - color
 * border-radius
 * border-image
 * box-sizing
 * box-shadow

###背景に関するプロパティ
 * background
  - color
  - image
  - repeat
  - attachment
  - position
 * background-clip
 * background-origin
 * background-size

###テキストに関するプロパティ
 * color
 * font
  - family
  - style
  - variant
  - weight
  - size
 * line-height
 * text-decoration
 * text-align
 * vertical-align
 * leter-spacing
 * word-spacing
 * text-transform
 * white-space
  * text-shadow

###内容に関するプロパティ
 * content
 * quputes
 * counter-reset
 * counter-increment

###ユーザーインターフェイスに関するプロパティ
 * cursor
 * resize
 * appearance

###アニメーションに関するプロパティ
 * transition
  - property
  - duration
  - timing-function
  - delay
 * animation
  - name
  - duration
  - timing-function
  - iteration-count
  - direction
  - play-state
  - delay
  - fill-mode

私たちにとって表示崩れやホワイトバック（白い状態が続くこと）は致命的な**バグ**です。
完全に起こさないことは難しいため**バグ**を減らすためにこの順番で書くことを私は推奨します。

ちなみに自分の任意の順番を意識したり人に伝えたりするには少し時間がかかります。
そこでCSScombというツールを使用すると自動的に自分が決めたルールにしたがい整形してくれます。
しかもタスクランナーにプラグインとしてあるのでSASS等をビルドする時組み込むと便利です。
<br>
