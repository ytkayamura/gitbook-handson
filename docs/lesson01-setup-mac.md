# Lesson 1: 環境構築(Mac編)
まっさらな環境で試せていないので、手順漏れがあるかもしれません。  
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
`ndenv`の方がフォルダ毎にバージョンを設定できるので今から環境構築する人はこちらのほうが便利のはずですが、私が使ってないため、以下は`nodebrew`の導入方法です。  
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
`npm`の速い版です。  
`npm`はnodeのパッケージ管理ツールです。
普通にインストールするとnodeまでインストールされるので、yarnだけインストールします。
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
上のページの`install`ボタンを押し、VSCode上でインストールを完了させてください。
***
## 開発の開始
#### ハンズオンプロジェクトを作成
これから開発を開始したいディレクトリに移動します。
```
(例)
$ cd ~/work
```
ハンズオンプロジェクトをクローンして、パッケージをインストールします。
```
$ git clone git@gitlab.com:jabaoplus/typescript-webapp-handson.git typescript-webapp-handson
```
#### ハンズオン用ブランチに設定
gitのブランチをハンズオン用のブランチに変更します。
```
$ git checkout handson
Branch handson set up to track remote branch handson from origin.
Switched to a new branch 'handson'
```

#### SourceTreeの使用
`新規...`->`既存のローカルリポジトリを追加`より`git clone`で作成された`typescript-webapp-handson`ディレクトリを開きます。
#### VSCodeの使用
`Start`->`Open folder...`より`typescript-webapp-handson`ディレクトリをVisualCodeで開きます。

#### 開発の開始
`package.json`と`yarn.lock`に記載されているパッケージをインストールします。
```
$ yarn
```
ビルドします。  
`watch`モードにしてあるので、ソースが変更されたら自動的にビルドされます。  
ただし、ソースを移動した場合など、うまくいかなくなる場合があるので、その場合は`Ctrl+C`で停止して、再実行してください。
```
$ yarn build:dev:server
```
もう一枚ターミナルを開いてプロジェクトディレクトリに移動し、アプリケーションを起動します。  
```
(例)
$ cd ~/work/typescript-webapp-handson
```
```
$ yarn start:dev:server
```
こちらも再ビルド後に再起動されるようにしてありますが、うまくいかない場合は`Ctrl+C`で停止して、再実行してください。

ブラウザで下記のURLを開いてください。
```
http://localhost:8080
```
`Hello Express!`と表示されたらOKです！
