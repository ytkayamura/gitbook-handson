# アロー関数
ラムダ式など使っていれば構文については難しくはないはずです。  
ただし、`this`の扱いが変わる点は注意です。  
アロー関数は自身の`this`を持たず、中に記述された`this`は外の`this`を参照します。  
これを利用してReactコンポーネントのインスタンスメソッドをアロー関数として定義することで、`bind()`を省略するテクニックがあります。

## 型なし定義
まずはTypeScriptらしくはないですが、型なしのシンプルな定義から見てみましょう。
```
const allow1 = () => 'allow1';
assignCallBack(() => 'allow1');
```
変数の宣言には`const`と`let`を使います。  
`const`は定数、`let`は変数。  
なるべく`const`を使うことが推奨されてます。

`function`使って書くとこうなります。
```
function allow1() {
  return 'allow1';
}
assignCallBack(function () { return 'allow1' } );
```

## 戻り値の型あり定義
```
const allow2 = (): string => 'allow2';
```
`function`使って書くとこうなります。
```
function allow2_orgFunc(): string {
  return 'allow2';
}
```

## 引数あり定義
```
const allow3 = (str: string): string => str;
```
`function`使って書くとこうなります。
```
function allow3_orgFunc(str: string): string {
  return str;
}
```

## 複数行定義
```
const allow4 = (): number[] => {
  const nums = [1, 2, 3, 4];
  return nums.map((n: number): number => n * 2);
};
```

## 高階関数
関数を返す関数のことです。  
コールバック関数のように引数が決められていて呼び出し時に渡せない値を関数の作成時に動的に関数内に埋め込んでしまうなどの使い方ができます。  
ちょっとトリッキーな記述になるので練習してみましょう。  
```
const generateCallback = (s: string) => () => console.log(s);
generateCallback('hoge')();
generateCallback('fuga')();
```
これはこう書くのと同じことです。
```
function generateCallback(s: string) {
  return function () {
    console.log(s);
  };
}
generateCallback('hoge')();
generateCallback('fuga')();
```
型をしっかり書くとこうなります。  
さすがにこうなるとかえってわかりづらいですね。。
```
const generateCallback = (s: string):() => void => ():void => console.log(s);
```

## 課題
アロー関数の書き方を練習してみましょう。

## 参考
https://gitlab.com/jabaoplus/webapp-handson-lesson/commit/87d3ca30137168a7ed9e9684d92ef756b981c906
