# Lesson 2: ハンズオンプロジェクトのセットアップ
## ハンズオンプロジェクトを作成
これから開発を開始したいディレクトリに移動します。
```
(例)
$ cd ~/work
```
ハンズオンプロジェクトをクローンして、パッケージをインストールします。
```
$ git clone https://gitlab.com/jabaoplus/webapp-handson.git
```

## SourceTreeの使用(Mac)
`新規...`->`既存のローカルリポジトリを追加`よりLesson1で`git clone`した`webapp-handson`ディレクトリを開きます。

## SourceTreeの使用(Windows)
`Add`->`参照`よりLesson1で`git clone`した`webapp-handson`ディレクトリを開き、`追加`を押します。

## VSCodeの使用
`Start`->`Open folder...`より`webapp-handson`ディレクトリをVisualCodeで開きます。

## アプリケーションの起動
npmパッケージをインストールします。
```
$ yarn
```
ビルドします。  
```
$ yarn build:dev:server
```
`watch`モードにしてあるので、ソースが変更されたら自動的にビルドされます。  
ただし、ソースを移動した場合など、うまくいかなくなることがあるので、その場合は`Ctrl+C`で停止して、再実行してください。

もう一枚ターミナルを開いてプロジェクトディレクトリに移動し、アプリケーションを起動します。  
```
(例)
$ cd ~/work/webapp-handson
```
```
$ yarn start:dev:server
```
こちらも再ビルド後に再起動されるようにしてありますが、うまくいかない場合は`Ctrl+C`で停止して、再実行してください。

ブラウザで下記のURLを開いてください。
```
http://localhost:8081
```
`Hello Express!`と表示されたらOKです！

## 画面分割
`build:dev:server`と`start:dev:server`のウィンドウを同時に見るために、画面分割できるターミナルソフトの利用を推奨します。  
クライアント側が加わるともう一枚増えるので。  

Macなら`iTerm`が超定番。  
https://www.iterm2.com/  

Windowsなら`ConEmu`あたりがよさそうです。
https://conemu.github.io/
