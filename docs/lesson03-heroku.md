# Lesson2: ハンズオンプロジェクトのセットアップ
## ハンズオンプロジェクトを作成
これから開発を開始したいディレクトリに移動します。
```
(例)
$ cd ~/work
```
ハンズオンプロジェクトをクローンして、パッケージをインストールします。
```
$ git clone https://gitlab.com/jabaoplus/webapp-hanson.git
```

## SourceTreeの使用
`新規...`->`既存のローカルリポジトリを追加`より`git clone`で作成された`webapp-handson`ディレクトリを開きます。

## VSCodeの使用
`Start`->`Open folder...`より`webapp-handson`ディレクトリをVisualCodeで開きます。

## アプリケーションの起動
npmパッケージをインストールします。
```
$ yarn
```
ビルドします。  
`watch`モードにしてあるので、ソースが変更されたら自動的にビルドされます。  
ただし、ソースを移動した場合など、うまくいかなくなることがあるので、その場合は`Ctrl+C`で停止して、再実行してください。
```
$ yarn build:dev:server
```
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
http://localhost:8080
```
`Hello Express!`と表示されたらOKです！
