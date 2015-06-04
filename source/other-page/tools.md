title: "タスクランナーツールの設定について"
description: タスクランナーツール「Gulp」「Grunt」の設定方法です。
---
各タスクランナーについての設定について説明します。
「Proxy」の設定が完了しているうえで書いていきます。

##基本設定
基本的に「Sass」や「CSSのプレフィックス」などはタスクランナーツールをしようして制作します。
個人的には「Gulp」がお勧めです。

##Gruntの設定

「Grunt」のをインストールします。

```Javascript
npm -g install grunt-cli
```
- 「-g」を付けるとグローバルにインストールするということです。

コマンドツールでプロジェクトに移動します。

```Javascript
cd /user/project/...
```

移動したら以下のコマンドで

```Javascript
npm init
```

このコマンドを実行すると色々聞かれますがとりあえずは「Enter」で進めてください。
そうすると「package.json」と「gruntfile.js」というファイルができます。

「package.json」ファイルは「npm（node package maneger）」の情報や各種設定が記述されるファイルです。
「gruntfile.js」ファイルは「grunt」のタスクを記述するファイルです。

次に「Grunt」本体をインストールします。

```Javascript
npm install --save-dev grunt
```

「--save-dev」を付けると「package.json」に記述されます。
記述されることで、他のプロジェクトでも同じ設定を使用したい場合でも「package.json」をコピペして以下のコマンドを実行するだけで同じ「npm」が使用できます。

```Javascript
npm install
```

なので新しい「npm」をインストールするときは「--save-dev」をつけましょう。
インストールが完了したらプロジェクトに応じたファイルをインストールします。

私は以下のファイルをお勧めします

- [grunt-contrib-sass](https://github.com/gruntjs/grunt-contrib-sass) //sass3.4に対応しています。
- [grunt-contrib-cssmin](https://github.com/gruntjs/grunt-contrib-cssmin) //cssをmin化してくれます。
- [grunt-contrib-concat](https://github.com/gruntjs/grunt-contrib-concat) //ファイルを結合します。
- [grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer) //ベンダープレフィックススをつけてくれます。
- [grunt-contrib-lint](https://github.com/gruntjs/grunt-contrib-csslint) //CSSをベストにしてくれます。
- [grunt-csscomb](https://github.com/csscomb/grunt-csscomb) //CSSをバラバラに書いたものの順番を綺麗にしてくれます。
- [grunt-stylestats](https://github.com/tvooo/grunt-stylestats) //cssを分析してくれます。
- [grunt-contrib-watch](https://github.com/gruntjs/grunt-contrib-watch) //gruntのタスクツールを監視してくれます。
- etc...

です。

この他にもパーフォーマンスを考えたりしてプラグインを選んでいきましょう。

###gruntfile.jsの基本

基本的に以下のように記述していきます。

```Javascript
'use strict';

module.export = function(grunt){

  grunt.registerTask('task', 'description', function() {
    grunt.log.writeln('HelloWorld!);
  });

  grunt.registerTask('default', [ 'task' ]);
}

```

分解して解説します。

```Javascript
'use strict';
```
必ず厳格モードを使用します。

```Javascript
module.export = functio(grunt){...}
```
外側で囲んでいる`module.export`は、Node.js特有の書き方です。これに登録されたオブジェクトを、Gruntが処理します。
この中に各タスクを記述していきます。

###タスクの記述
各タスクは以下のように`grunt.initConfig`の中に`リテラル`で記述していきます。

```Javascript
grunt.initConfig({
  タスク名称1: {
    ...省略
  },
  タスク名称2: {
    ...省略
  },...
});
```
###gruntプラグイン読み込み

以下のようにして必要なプラグインを読み込みます。

```Javascript
grunt.loadNpmTask('npmプラグイン名');
```

###タスクの実行

```Javascript
grunt.registerTask('task', 'description', function(){...});
```

`grunt.regsterTask`を呼び出し「タスク」（任意）を登録しています。
`registerTask`に渡す引数は順に、「タスク名称」、「簡単な説明」、「タスク実行内容」です。

これを元にコードを書くと以下のようになります。

```Javascript
grunt.registerTask('タスク名称', '簡単な説明', タスク実行内容);
```

です。
「簡単な説明」は省略できます。

タスクは配列でまとめて登録することもできます。

```Javascript
grunt.registerTask('default', [ 'task1', 'task2' ]);
```

この設定が完了したら、以下のコマンドを実行します。
```Javascript
grunt
```

そうすると設定通りに実行されます。

##Gulpの設定

私は以下の理由でこちらを推奨します。

- Gruntより設定ファイルが記述しやすい
- StreamAPI（簡潔に書ける）を利用することでファイルを毎回書き出すGruntより高速

「Gulp」をインストールします。

```Javascript
npm install -g gulp
```

グローバルにインストールしたら
プロジェクト用フォルダを作りローカルに移動しインストールします

```Javascript
mkdir test
cd /test
npm install gulp --save-dev
```
インストールが完了したら他のnpmファイルもインストールしていきます

- [grunt-browserify](https://github.com/jmreidy/grunt-browserify) //仮想サーバを立ち上げて自動的にブラウザを立ち上げ更新します。
- [gulp-autoprefixer](https://github.com/sindresorhus/gulp-autoprefixer) //ベンダープレフィックスをつけてくれます。
- [gulp-concat](https://github.com/wearefractal/gulp-concat) //ファイルを結合します
- [gulp-specificity-graph](https://github.com/ishotfirst/gulp-specificity-graph) //CSSのセレクタ強度をグラフ化してくれます。
- [gulp-csslint-report](https://github.com/thirus/gulp-csslint-report) //CSSのテストをしてレポートをだしてくれます。
- [gulp-plato](https://github.com/sindresorhus/gulp-plato) //Javascriptのテストをしてレポートをだしてくれます。
- [gulp-hologram](https://github.com/rejahrehim/gulp-hologram) //スタイルガイド生成します
- [gulp-load-plugins](https://github.com/jackfranklin/gulp-load-plugins) // 毎回requireする必要がなくなります
- [gulp-minify-css](https://github.com/murphydanger/gulp-minify-css) // cssをmin化してくれます
- [gulp-notify](https://github.com/mikaelbr/gulp-notify) //デスクトップに処理が完了すると表示してくれます
- [gulp-plumber](https://github.com/floatdrop/gulp-plumber) //エラーが出てもwatchタスクが止まらない
- [gulp-ruby-sass](https://github.com/sindresorhus/gulp-ruby-sass) //RubyのSassを使用してビルドします。
- etc...

こんな感じで必要なものをインストールしていきます。
インストール完了したら`gulpfile.js`を作りタスクを書いていきます。

```Javascript
echo > gulpfile.js
```

###gulpプラグイン読み込み

gulpファイルに以下を記述してプラグインを読み込みます。

```Javascript
var gulp = require("gulp");
```
`require`を使用して読み込みます。
`gulp-load-plugins`を使用すると読み込みが簡単になります。

```Javascript
var $ = require("gulp-load-plugins");
```

このように読み込むと以下のように記述をするだけで読み込むことができます。

```Javascript
$.rubySass('path',...省略
```

###gulpのタスク記述

各タスクは以下のように記述していきます。

```Javascript
gulp.task('タスク名', タスク実行内容)
```

「タスク名」は任意で命名してください。
「タスク実行内容」は基本的に`function(){}`の記述`{}`の中にで書いていきます。
戻り値としてタスクの処理を記述します。
例として`grunt-ruby-sass`を記述していきます。

```Javascript
gulp.task('sass', function () {
    return $.rubySass('_src/sass/style.scss', オプション) //コンパイルするscssファイル「*」で指定するとエラー
            .pipe(gulp.dest('_dest/css/'));　//出力先
});
```

このように記述していきます。

###gulpのタスク実行&監視

`gulp-watch`を使用しタスクを実行＆監視していきます。

```Javascript
gulp.task('defalut', ['sass'], function () {
    gulp.watch('_src/sass/**/*.scss', ['sass']);
});
```

基本的な記述方法です。
実際は以下のコマンドで実行します。

```Javascript
gulp
```
