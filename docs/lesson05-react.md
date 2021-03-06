# Lesson 5: Reactによるクライアントサイドの実装

`React`に必要なパッケージをインストールします。  
`@types/`付きのパッケージはTypeScriptの型を定義したものです。
```
$ yarn add react react-dom @types/react @types/react-dom
```
クライアントサイドの開発用に`webpack-dev-server`をインストールします。  
`-D`はローカル開発環境のみでインストールするオプションです。  
`webpack-dev-server`はソースコードの変更監視(`watch`)、再ビルド、アプリケーションの再起動をはじめとした様々な機能を持っています。
```
$ yarn add -D webpack-dev-server
```

## コミット差分
Lesson 5終了時点の[Lesson4-2 アロー関数](docs/lesson04/02_arrow-function.md)の`参考`からの差分は下記となります。

https://gitlab.com/jabaoplus/webapp-handson-lesson/commit/df6da24f56f23ec2fe90c511ca3a314188e679ef

## webpack.config.js
[コミット差分](https://gitlab.com/jabaoplus/webapp-handson-lesson/commit/df6da24f56f23ec2fe90c511ca3a314188e679ef)を参考に`webpack.config.js`を追加してください。  
クライアントサイドの`webpack`設定です。

## client/index.tsx
ビルドのエントリポイントとなるindex.tsxを作成します。  
`ReactDOM.render()`の第一引数が`JSX`で記述されたルートとなるReactコンポーネントです。 
`JSX`はHTMLライクにタグでReactコンポーネントの構造を記述でき、`{}`で囲ってTypeScriptのコードを埋め込むこともできます。  
厳密には大きく異なるものですが、PHP等のHTMLテンプレートに似た感覚で記述できるかと思います。
第２引数にはルートコンポーネントを注入するHTMLエレメントを指定しています。  
importした`React`がコード上に登場していませんが、`JSX`を使用する際に`React`のimportが必要となります。
```
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import Hello from './component/Hello';

ReactDOM.render(
  <Hello />,
  document.getElementById('app'),
);
```

## public/index.html
トップページです。index.tsxの`getElementById('app')`で選択されるエレメントが`<div id=app></div>`です。  
`script`タグにビルド結果として出力される`bundle.js`を指定しています。
```
<!doctype html public="storage">
<html>
<meta charset=utf-8/>
<meta name="viewport" content="width=device-width"/>
<title>Hands on</title>
<div id=app></div>
<script src="/bundle.js"></script>
```

## client/components/Hello.tsx
`index.tsx`で使用されていたルートコンポーネントです。  
renderの戻り値の`JSX`の型が`JSX.Element`と指定されていますね。
```
import * as React from 'react';

export default class Hello extends React.Component {
  render(): JSX.Element {
    return (
      <div>Hello React!</div>
    );
  }
}
```

## package.json
`scripts`の`start`の下に下記を追加します。  
`start:dev`はローカル開発用、`build`は本番(Herokuデプロイ)用です。
```
    "start:dev": "webpack-dev-server --mode development --open",
    "build": "webpack --mode production",
```

`heroku-postbuild`コマンドに`build`を追加しましょう。
```
-   "heroku-postbuild": "yarn build:server"
+   "heroku-postbuild": "yarn build && yarn build:server"
```

## デバッグ起動
`webpack-dev-server`を起動してみましょう。  
ターミナルを1枚、新たに立ち上げてプロジェクトディレクトリに移動します。
```
$ yarn start:dev
```
ブラウザで下記のURLが開き、`Hello React!`と表示されたらOKです！
```
http://localhost:8080
```

## サーバサイドの設定
本番(Herokuデプロイ)用にはサーバサイドのExpressから`index.html`が開くようにしておく必要があります。

### server/server.ts
コメントアウトしていた`Hello Express!`を表示していたコードを復活させ、`Lesson4`関連の記述を削除します。(`exercise`ディレクトリは残しておいてもよいです)  
`path`をimport。
```
import * as path from 'path';
```
`app.get()`を削除して、代わりに静的ファイルの配置ディレクトリとして`public`を指定します。  
```
- app.get('/', (req: Express.Request, res: Express.Response) => {
-   return res.send('Hello Express!');
- });
+ app.use(Express.static(path.join(__dirname, '../public')));
```

###  webpack.server.config.js
下記を書き加えます。  
`path`でローカルのフルパスを取得できるようにする設定です。
```
    node: {
      __dirname: false,
      __filename: false
    },
```

### クライアントサイドのビルド
`yarn build`を実行し、`public/bundle.js`を作成します。  

### サーバサイド再起動
`yarn build:dev:server`と`yarn start:dev:server`を一度停止して再実行しましょう。

ブラウザで下記のURLを開いてください。
```
http://localhost:8081
```
`Hello React!`と表示されたらOKです！
