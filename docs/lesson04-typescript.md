# Lesson 4: TypeScript文法のポイント
TypeScriptはES6(JavaScriptの2015年に制定された新しい規格)を拡張したものとなります。  
便利ですが最初はとっつきが悪いかもしれないES6で導入された簡略記法を中心に学んでいきます。

練習用のTypeScript実行環境を別途構築するのは手間なので、Lesson01、Lesson02で作った環境を流用しましょう。  
`server/exercise`ディレクトリを作成し、その配下に練習のソースコードを書いていきます。  
下記のようなファイル構成です。
```
server
 ├ server.ts
 └ exercise
    ├ exercise01.ts
    └ exercise02.ts
```
server/server.tsの中身はいったん全部コメントアウトして練習用ソースコードをimportして呼び出し形でいろいろ試してみましょう。

`yarn buid:dev:server`と`yarn start:dev:server`をそれぞれ別のターミナルで実行しておきます。  
server.tsやそこから呼び出すソースコードで`console.log()`した内容が`yarn start:dev:server`したターミナル上で、
```
[nodemon] starting `node server/server.bundle.js`
```
と
```
[nodemon] clean exit - waiting for changes before restart
```
の間に表示されます。
