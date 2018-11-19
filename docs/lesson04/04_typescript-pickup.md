# TypeScript機能ピックアップ
これまでは主にES6の機能を見てきましたが、TypeScriptで拡張された機能から特に抑えておきたいものを見ていきます。  
クラス、ジェネリックは重要ですが、わかる人が多いと思うのでいったん割愛します。  

## Enum
区分値の定義にはEnumを使いましょう。
```
enum Hyouka {
  VERY_GOOD: 'VERY_GOOD',
  GOOD: 'GOOD',
  FUTSU: 'FUTSU',
  BAD: 'BAD',
}
function (hyoka: Hyoka) {
  switch (hyoka) {
  case Hyoka.VERY_GOOD:
    ：
  case Hyoka.GOOD:
    ：
  }
}
```
値は省略できます。  
あんまり使わないと思うので、基本的に省略でよいでしょう。  
省略した場合は0からはじまる数値が自動的に割り当てられます。
```
enum Hyouka {
  VERY_GOOD,
  GOOD,
  FUTSU,
  BAD,
}
```

## ユニオン型
複数の型を許容する型が定義できます。  
縦棒`|`で区切っていくつでも型を列挙できます。
```
type TypeAB = TypeA | TypeB;
function (a: TypeA, b: TypeB) {
  let aa: TypeA = a;  // 当然OK
  aa = b;             // 当然NG
  let bb: TypeB = b;  // 当然OK
  bb = a;             // 当然NG
  let ab: TypaAB = a; // OK
  ab = b;             // これもOK
}
```

## オブジェクト型
[簡易記法](docs/lesson04/03_shorthand-expression.md)でさらっと登場させてしまいましたが、オブジェクトのプロパティの方を定義するものです。  
`?`付きのプロパティはオプション、つまり`?`なしのプロパティは必須項目です。
```
interface Hoge {
  a: string;
  b: number;
  c?: string;
}
const hoge: Hoge = {
  a: 'a',
  b: 2,
  c: 'c',
};
```
名前を付けず直接定義することもできます。
```
let hoge: { a: string; b?: number } = {
  a: 'a',
  b: 2,
};
hoge = { a: 'aa' };
```

## 関数型
これも[アロー関数](docs/lesson04/02_arrow-function.md)で登場済みです。  
(`引数名`: `引数の型`) => `戻り値の型`
の形で定義します。  
`引数名`: `引数の型`はもちろんカンマ区切りで列挙できます。

まずは変数定義の例。  
読みにくいし、同じ行中で型の定義が重複していて冗長な気がしますね。  
```
( 変数定義 )
const f: (s: string) => string = (s: string) => {
  console.log(s);
  return s;
}
```
こういうコールバック関数の型を定義する場合の方が有用そうです。  
読みにくいことは読みにくいですが。
ちなみに`Array.from({ length: count }, (v, k) => k)`はJavaScriptの0〜`count`までの数列作成のイディオム、\`${xxx}\`というのはES6の`テンプレートリテラル`です。  
関数の中身は無視してもよいです。
```
( 関数定義、呼び出し )
function culculate(f: (n: number) => number, count: number): number {
  const counts: number[] = Array.from({ length: count }, (v, k) => k);
  let result: number = 0;
  for (const i: number of counts) {
    console.log(`f(${i + 1})=>${f(i + 1)}`);
    result = result + f(i + 1);
  }
  return result;
}
const total: number = culculate(n: number => n * 2, 3);
console.log(`total=>${total}`);
```

## 参考
https://qiita.com/pebblip/items/f04978415929b623108c
