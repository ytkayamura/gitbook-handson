# Lesson 1: 環境構築(Mac編)
まっさらな環境で試せていないので、手順に漏れがあるかもしれません。  
上手くいかなかったら教えてください。
## 各種インストール
#### Homebrewのインストール
Macのパッケージ管理ツールです。  
インストールの確認。
```
$ brew --version
Homebrew 1.8.2
Homebrew/homebrew-core (git revision e84eb; last commit 2018-11-12)
Homebrew/homebrew-cask (git revision cfdff; last commit 2018-11-12)
```
などと表示されれば、インストールされているのでスキップしてオッケーです。  
インストールされていなければ下記などを参考にインストールしてください。
https://qiita.com/rabbit1013/items/1494cf345ff172c3b9cd

#### Git
インストールされているはずです。  
一応バージョンを確認。
```
$ git version
git version 2.19.1
```
2系なら大丈夫かと思います。

#### Source Treeのインストール
GitのGUIツールです。  
https://ja.atlassian.com/software/sourcetree  
ダウンロードして解凍し、起動が確認できたら`アプリケーション`フォルダに入れておいてください。  

OSバージョンのせいで起動できない場合は、いったん古いバージョンを使ってもよいです。
https://www.sourcetreeapp.com/download-archives  

起動後、アカウントの登録やら必要かもしれませんが、使用できる状態にしておいてください。

#### nodebrewのインストール
nodeのバージョン管理ツールです。  
複数バージョンのnodeをインストールして切り替えができます。  
同カテゴリのツール`ndenv`の方がディレクトリ毎にバージョンを設定できるので今から環境構築する人はこちらが便利のはずですが、私が使ってないため、以下は`nodebrew`の導入方法です。  
複数のプロジェクト毎に依存するnodeのバージョンがずれてきた場合に必要になるので、必ずどちらかを導入しましょう。  
インストールの確認。  
```
$ nodebrew
nodebrew 0.9.6

Usage:
　：
```
インストールされていなければ、インストールします。
```
$ brew install nodebrew
```
nodeのバージョンを指定してインストールします。
```
$ nodebrew install 10.11.0
```
使用するnodeのバージョンを設定します。
```
$ nodebrew use v10.11.0
```
.bashrcなどに下記の記述を追加します。
```
export PATH=$HOME/.nodebrew/current/bin:$PATH
```
.bashrc(など)を読み込み直します。
```
$ . ~/.bashrc
```
バージョンの確認。
```
$ node --version
v10.11.0
```

#### yarnのインストール
`yarn`はnodeのパッケージ管理ツール`npm`の高速版です。  
普通にインストールすると上でインストール済みのnodeまでインストールされてしまうので、nodeのインストールをスキップするオプションを指定します。
```
$ brew install yarn --without-node
```
バージョンの確認。
```
$ yarn --version
1.10.1
```
のように表示されたらOK。
```
java 9.0.1
Java(TM) SE Runtime Environment (build 9.0.1+11)
Java HotSpot(TM) 64-Bit Server VM (build 9.0.1+11, mixed mode)
```
などと出てきたらそれはhadoopの`yarn`です。  
`$HOME/.nodebrew/current/bin/yarn`が優先されるように`.bashrc`などで設定しましょう。

#### VSCodeのインストール
https://code.visualstudio.com/
ダウンロード、解凍して、`アプリケーション`フォルダに入れます。  
tslintのExtensionもインストールしておきましょう。
https://marketplace.visualstudio.com/items?itemName=eg2.tslint
上のページの`Install`ボタンを押し、VSCode上でインストールを完了させてください。


悲報です。  
Mac版VSCodeでは日本語をバックスペースで削除した際に制御文字が残ることがあるようです。  
とりあえず制御文字を表示するように設定を変更します。  
* `Code`->`Preferences`から、  
`Search settings`に `renderCo` と入力、  
`Editor: Render Control Charactors`にチェック。  

意図しない制御文字ができてしまった際には必ず削除するようにしましょう。  