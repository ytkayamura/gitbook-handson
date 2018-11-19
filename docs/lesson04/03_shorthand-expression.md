# 簡略記法
これらは知らないとコード上で見かけた際にキーワードがわからないので検索もできないのがつらいところです。  
使えるようになると便利なので覚えてしまいましょう。  

## Object Shorthand
オブジェクトを作成する際に、代入する変数名と同じプロパティ名は左側の`<プロパティ名>: `を省略して書くことができます。
```
const hoge = 'abc';
const fuga = { hoge };
```
省略しないで書くとこうなります。
```
const hoge = 'abc';
const fuga = { fuga: fuga };
```
型がないですね。
```
const hoge: string = 'abc';
const fuga: { hoge: string } = { hoge };
```
もしくは
```
const hoge: string = 'abc';
interface Fuga {
  hoge: string;
}
const fuga: Fuga = { hoge };
```

## スプレッド構文
Reduxの公式ドキュメントで推奨されているように、Reduxの処理で多用します。
https://redux.js.org/recipes/usingobjectspreadoperator
```
const srcHoge = {
  a: 'a',
  b: 'b',
  c: 3,
  d: 4,
};
const destHoge {
  ...srcHoge,
  a: 'c',
};
```
これはこう書くのと同じことになります。
```
const destHoge {
  a: 'c',
  b: srcHoge.b,
  c: srcHoge.c,
  d: srcHoge.d,
};
```
型を入れて書いてみます。
```
interface Hoge {
  a: string;
  b: string;
  c: number;
  d: number;
}
const srcHoge: Hoge = {
  a: 'a',
  b: 'b',
  c: 3,
  d: 4,
};
const destHoge: Hoge = {
  ...srcHoge,
  a: 'c',
};
```

配列もスプレッド構文の使用が可能です。
https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Spread_syntax

## 分割代入
```
const hoge = {
  a: 'a',
  b: 2,
};
const { a, b } = hoge;
```
これはこう書くのと同じことになります。
```
const a = hoge.a;
const b = hoge.b;
```
型を入れて書いてみます。
```
interface Hoge {
  a: string;
  b: number;
}
const hoge: Hoge = {
  a: 'a',
  b: 2,
};
const { a, b }: Hoge = hoge;
```
指定した型のプロパティのうち一部だけを取得することも可能です。
```
const { a }: Hoge = hoge;
```
関数の定義と呼び出しにも使用できます。
```
function fuga({ a, b }: Hoge) {
  console.log(a, b);
}
export default function () {
  fuga(hoge);
}
```

## 課題
各種簡略記法を練習してみましょう。
