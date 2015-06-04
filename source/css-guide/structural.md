title: "CSS設計について"
description: "CSS設計の概念や考えを書いてます。OOCSS・BEM・SMACSS・ITCSSの考えを元にどう設計していくかをまとめています。"
---
CSS設計については[CSSルール](/css-guide/rule.html)にで少し触れましたが
ほんの一部にしかすぎませんCSS設計は奥深いのです。

基本はOOCSSの考えが元になっています。
さらに[CSS基礎](/css-guide/basic.html)でも触れたセレクタの強度も設計に重要に関わっています。

**CSSを書く上で設計本当に重要です。**

この設計がしっかりできているかできていないかでWeb全体がイケてるかイケてないか決まってしまいます。
いくらデザインがかっこよくても設計がダサかったら全てが台無しになるとでも言えます。
そのくらい大事なことです。

そのための方法を私はいつも考えています。
##CSS設計について
CSSの設計はHTMLの構造と深く結びついています例えばしかっりHTMLの構造が設計されルールがしっかりしたものなら
以下のような擬似セレクタを使用したスタイルも書くことができます。

```css
section - section {
  margin-top: 20px;
}

h1 + * {
  margin-top: 20px;
}
```
ですがもしパーツとして普段使用しない部分で使用する場合もあります。
そうすると崩れが起きてしまいます。
その崩れを打ち消すためのスタイルを書くのもいいですが、その分ファイルが大きくなりパフォーマンスが下がってしまいます。
こういったことも考えた上でスタイルを決め制作するのが望ましいでしょう。

##モダンCSS設計について

モダンCSS設計とはOOCSSのオブジェクト指向が元にさらに考えれたものです。
有名なものではBEMやSMACSSが有名です。

この二つを含め基本的にSASSを使用てファイルの構成から考え設計していきます。
以下のようにファイル分けます。

- 設定ファイル
- ツールファイル
- リセットファイル
- エレメントファイル
- オブジェクトファイル
- コンポネントファイル
- 調整ファイル

大きく分けるとこの７つに分けることができます。
各ファイルについて詳しく説明していきます。

###設定ファイル
configファイルです基本的な設定など（ベースの色、フォントサイズなど）の変数や設定を管理するファイルです。

###ツールファイル
sassの**mixin**や**function**のファイルです。

###リセットファイル
「reset.css」や「normalize.css」です。

###エレメントファイル
プロジェクトごとの各タグ(bodyやpなど)のCSSファイルです。

###オブジェクトファイル

レイアウトファイルです。
ページを構成するヘッダーやメインのコンテンツエリアなどの共通のレイアウトです。

###コンポネントファイル

コンポネントファイルは２種類に分けることができます。
汎用性があり再利用できる最小限のパーツファイルと、プロジェクト固有のファイルに分けることができます。
最小限のパーツファイルとプロジェクト固有のファイルは以下のように各パーツごとに分けて使用します。

- 汎用性があり再利用できる最小限のパーツファイル => parts
- プロジェクト固有のファイル => project

とファイル名をつけます。

```css
_component-parts_button.scss
...省略
_component-project_button.scss
```

読み込み順は以下の順に読み込みます。

<div class="em">parts => project</div>

複数のパーツの組み合わせも含まれるためファイルを「@import」する際には注意が必要です。

###調整ファイル

各パーツやレイアウトの調整ファイルです。
解決することが難しい・適切では無いわずかなスタイルを調整をするファイルです。
例えば状態を表したり、マージンの調整などでしようします。

###まとめ

最終的には１ファイルにまとめますが、細分化することで管理がしやすくなり、メンテナンスもしやすくなります。
ここで重要なのは各ファイルの読み込む順番です。
セレクタ強度が高いものが先に読み込まれてしまうとCSSが汚染されてしまい、
思ったように動作しなくなってしまいます。

このことがないようにセレクタの強度は常に意識して設計しましょう。

##セレクタ強度について

先ほど分割したファイルのセレクタ強度について説明します。

###設定ファイル

基本的にこのファイルはSASSの設定を書いているだけなのでセレクタとは関係無いため**0%**です。

<div class="progressBar"><div class="progressBar_none">%</div><p class="progressBar_text">0%</p></div>

###ツールファイル

「mixin」「function」の設計にもよりますが両方も基本的には戻り値を返すだけなのでセレクタとは関係ないので**0%**です。

<div class="progressBar"><div class="progressBar_none">%</div><p class="progressBar_text">0&nbsp;%</p></div>

###リセットファイル

リセットするだけなでここでは最低の強度として**10%**です。

<div class="progressBar"><div class="progressBar_low">%</div><p class="progressBar_text">10&nbsp;%</p></div>

###エレメントファイル

各タグに基本的になスタイルをあてるファイルです実際はそこまでリセットと変わりませんが少しは高いので**20%**にしました。

<div class="progressBar"><div class="progressBar_lowMid">%</div><p class="progressBar_text">20&nbsp;%</p></div>

###オブジェクトファイル

クラスやタグをにスタイルを指定するので**40%**としております。

<div class="progressBar"><div class="progressBar_middle">%</div><p class="progressBar_text">40&nbsp;%</p></div>

###コンポネントファイル

ここは**40 ~ 60%**にしました。
各ファイルは組み合わせのものとそうで無いものと、パーツファイルとプロジェクトファイルにも強度の強さが異なるので幅をもたせております。

<div class="progressBar"><div class="progressBar_heigh">%</div><p class="progressBar_text">40 ~ 60&nbsp;%</p></div>

###調整ファイル

このファイルを**100%**にした理由はどのセレクタよりも強くし無いといけないファイルだからです。
ルールでは「!important」を禁止していますがこのファイルは例外で他に勝つため使用します。
そのため100%としました。

<div class="progressBar"><div class="progressBar_max">%</div><p class="progressBar_text">100&nbsp;%</p></div>

###まとめ

CSSのコードは上から下に読み込まれるのでファイルの上に書いてあるコードはセレクタ強度が弱く下にいくほど
強くなっていきます。
「RWD」のサイトなどでよく大きい「mediascreen」で囲ったりしていますが、
セレクタの強度のことを考えると個別に指定する「mixin」で対応します。
<br>
<center>![セレクタ強度のピラミッド](/img/traiangle.png "セレクタ強度")</center>
<br>

##ファイル・ディレクトリ構成

上記のことを踏まえ基本的な構成は以下のようにしました。

```html
/*-----------------------
 設定ファイル - settings
 ------------------------ */

/**
 * global
 */

 $base-font-size: ...;


/*-----------------------
 ツールファイル - tools
 ------------------------ */

/**
 * mixin
 */

@mixin grid(arg1, arg2){...}

/*-----------------------
 リセットファイル -generic
 ------------------------ */

/**
 * reset
 */

* {...}


/*-----------------------
 エレメントファイル - element
 ------------------------ */

/**
 * page
 */

html {...}



/*-----------------------
 オブジェクトファイル - object
 ------------------------ */

/**
 * layout
 */

.o-header {...}

/*-----------------------
 コンポネントファイル　-component
 ------------------------ */

/**
 * parts
 */

/*--- ボタン ---*/

/** defaltボタン **/

 .c-button {...}


/**
 * project
 */

/** 問い合わせボタン　**/
.p-button__contact {...}


/*-----------------------
 調整ファイル - trumps
 ------------------------ */

/**
 * utility
 */

/*--- マージン ---*/

/** bottom **/

.t-mgb_s {...}

/**
 * state
 */

 /*--- メニュー ---*/

 /** active **/

 .is-active {...}
```

もしSASSなどのCSSプロセッサやビルドツールCSSを結合できるのであれば、
次のようにディレクトリ構造作るとわかりやすいです。

```html
├── setting
│   └── _config.scss
|
├── tools
│   ├── _functions.scss
│   └── _mixins.scss
|
├── generic
│   ├── _normalize.scss
│   └── _reset.scss
|
├── element
│   └── _base.scss
|
├── object
│   └── _layout.scss
|
├── component
|   ├── parts
|   │   ├── _button.scss
|   │   └── ...省略
|   |
|   └── project
|       ├── _articles.scss
|       └── ...省略
|
└── utility
        ├── _utility.scss
        └── _state.scss
```

モジュール単位でファイルを分割することによって、ページ単位またはプロジェクト単位でのモジュールの追加・削除の管理がしやすくなります。

##CSS命名規則による設計

モダンCSS設計の考えにはBEMとSMACSSといった考えかたがあります。
この二つの特徴としてはOOCSSの考えを元に独自の命名規則やパーツの考え方に特徴があります。
ここでは二つについて詳しく説明しません。

ですが両方に共通して考えられてるComponentsを意識したパーツの設計のについて説明します。
Componentsとは他のページでも何回も触れていますが**おもちゃのブロック**のような**パーツのまとまり**です。
これと文脈（コンテキスト）を細かく分けた作りなっています。
さらに私は役割がわかるように、ファイルで分割した「オブジェクト」「コンポネント」「調整」の３つで分けています。

###方法
基本的に上記の考え元にCSSを設計していきます。
基本的な記法は「[MindBEMding](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)」をベースに**Block**、**Element**、**Modifier**の考えを使用しています。
以下のように記述します。

```css
[Block]__[Element]--[Modifire]
```

そこに役割を明確にするために接頭辞(プレフィックス)つけます。
3つに加え状態を表す「is」という接頭辞(プレフィックス)を追加します。
以下のようにします。

- オブジェクト(Object) => o-
- コンポネント(Components) => c-
- 調整(Utility) => u-
- 状態 => is-

```css
[Prefix]-[Block]__[Element]--[Modifire]
```

このように記述していきます。
それでは実際どう使用するか例を見ていきます。

###記述例

以下のパーツ例に見ていきます。

![サンプルテキストの画像](/img/txt.png "サンプルテキスト")

上から順番に書いていきます。

**HTML**

```html
<!-- 通常 -->
<p class="c-text">sample</p>

<!-- 太字 -->
<p class="c-text c-text__bold">sample</p>

<!-- 太字の青 -->
<p class="c-text c-text__bold c-text__bold--blue">sample</p>

<!-- 太字の赤 -->
<p class="c-text c-text__bold c-text__bold--red">sample</p>
```

**CSS**

```css
.c-text {
  font-size: 14px;
  line-height: 1.5;
}

.c-text.c-text__bold {
  font-weight: bold;
}

.c-text.c-text__bold.c-text__bold--blue {
  color: blue;
}

.c-text.c-text__bold.c-text__bold--red {
  color: red;
}
```

このように使用します。
次のように考えて命名していきます。

<div class="em-normal">まずこのパーツは「テキスト」という「コンポネント」なので「プレフィックス」は「c-」になります。
そして任意で文脈（コンテキスト）を考えながらクラス名を付けます（ここではサンプルのため「text」にしました）。
通常のパターンとして「太字」ですなので「bold」というクラスをつけます。
太字のさらなるパターンとして「青」と「赤」があります。
なので「blue」「red」とます。</div>

しかしパーツを設計するときにどの役割なのか考えて決めるのはとても難しいです。
そこで重要なのは論理と文脈（コンテキスト）です。
この二つを考えればどう作るか簡単にわかるはずです。

##クラスが長い問題

BEMの考え方をもとに設計していくとクラス名がどんどん長くなってカオスになってしまいます。
以下のコードのように１つで完結したら美しいですよね。

```html
<p class="c-text__bold--red">sample</p>
```

そこでSASSの機能を使用します。
以下のように書くことで上記のようにできます。

```css
.c-text {
  %text {
    font-size: 14px;
    line-height: 1.5;
  }
  @extend %text;
  @at-root {
    %bold {
      @extend %text;
      font-weight: bold;
    }
    #{selector-append(&, "__bold")} {
      @extend %bold;
      @at-root {
        #{&}--red {
          @extend %bold;
          color: red;
        }
      }
    }
  }
}
```

「c-text」と「c-text__bold」は共通な部分なのでこれを「CSSクラス」として考えSASSの機能である「@extend(継承)」を利用して書いていきます。
「@at-root」を使用することで「親要素」を無視できるのでこれで囲みます。
「selector-append($selector)」を利用することでスペースなしで文字列を繋いでくれます。

このようにするとCSSでは以下のように出力されます。

```css
.c-text,
.c-text__bold,
.c-text__bold--red {
  font-size: 14px;
  line-height: 1.5;
}

.c-text__bold,
.c-text__bold--red {
  font-weight: bold;
}

.c-text__bold--red {
  color: red;
}
```

こうなることで「c-text__bold--red」のクラスだけで適応されます。
これでカオスな状態を回避できます。

##まとめ
設計するということは本当に重要で大事なことです。
これをしっかりしないとCSSもHTMLもカオスな状態になり改修できなくなります。
そうなってからでは手遅れです。
そうならないためにもしっかり設計するようにしましょう。
