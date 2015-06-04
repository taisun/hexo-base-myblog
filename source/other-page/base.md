title: "Proxy配下での環境設定について"
description: 「Proxy」配下での環境設定方法です。
---
各ファイルの環境設定について説明します。
しかし環境によっては「**Proxy**」があってインストールができないことがあります。

##基本設定

基本的な環境を構築するには「Ruby」「git」「Nodejs」とタスクランナーツールの「Grunt」と「Gulp」が必要となります。
しかし「Proxy」の影響で設定できないことがあります。

###Windowsでの設定
「Windows」の環境では「スタート」=>「コンピューター」=>「システムのプロパティ」=>「システムの詳細設定」=>「環境変数」=>「ユーザー環境変数」から「**http_proxy**」と「**https_proxy**」を設定します。
以下のように設定します。

**http_proxy**
<div class="em">http://ユーザ名:パスワード@proxy.example.com:8080

**https_proxy**
<div class="em">https://ユーザ名:パスワード@proxy.example.com:8080

###MACでの設定

```html
export http_proxy=http://ユーザ名:パスワード@example.com:8080/
export https_proxy=$http_proxy
export all_proxy=$http_proxy
```

この設定をしても通らない場合があります。
その場合は以下のように設定します。

###gem(Ruby)

```html
export http_proxy=http://ユーザ名:パスワード@proxy.example.com:8080
export https_proxy=http://ユーザ名:パスワード@proxy.example.com:8080
```

###git

```html
export http_proxy=http://ユーザ名:パスワード@proxy.example.com:8080
export https_proxy=http://ユーザ名:パスワード@proxy.example.com:8080
```

###npm(Nodejs)

```html
npm -g config set proxy http://ユーザ名:パスワード@proxy.example.com:8080
npm -g config set https-proxy http://ユーザ名:パスワード@proxy.example.com:8080
npm -g config set registry http://registry.npmjs.org/
```

以上のように設定します。

「Bower」を使用する場合は「.bowerrc」というファイルに（なかったらrootに作る）、以下を記述する。

**.bowerrc**

```html
{
  "proxy" : "http://proxy.example.co.jp:8080",
  "https-proxy" : "http://proxy.example.co.jp:8080"
}
```
