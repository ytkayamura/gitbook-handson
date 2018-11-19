# import / export
とりあえず下記を覚えておきましょう。
* `export default`
* `export default`したモジュールの`import`
* `default`なし`export`
* `default`なし`export`したモジュールの`import`
* `default`なし`export`した複数モジュールの`*`による`import`

## export default
ファイルの中でひとつだけ`export default`できます。  
またfunctionやclass、関数の戻り値などは名前なしでのexportが可能です。
```
( export default: 変数定義 )
export default const hoge: string = 'hoge';
```
```
( export default: 定義済み変数 )
const hoge: string = 'hoge';
export default hoge;
```
```
( export default: function )
export default function (): void {
  console.log('export default');
}
```
```
( expor default: 関数の戻り値 )
function fuga(): string { return 'fuga' }
export default fuga();
```

## export defaultしたモジュールのimport
ファイル名と名前を指定して行います。  
`import <名前> from '<ファイル名>'`の形式。  
ファイル名は拡張子を省略します。  
指定した名前でそのまま使用できます。
```
( export defaultしたモジュールのimport )
import hoge from 'hoge';

// 文字列なら
console.log(hoge);

// 関数なら
hoge();
```


## defaultなしexport
`default`と書かないだけで上の`export default`の場合と同様に`export`できます。
```
( defaultなしexport: 変数定義 )
export const hoge: string = 'hoge';
```

## defaultなしexportしたモジュールのimport
`import { <名前1>, <名前2>, ... from '<ファイル名>'`の形式。  
名前を{}で囲むのがポイントです。  
同じファイルの複数モジュールをカンマ区切りで一度にexportできます。  
また、名前は`as`を使って変更可能です。
```
( defaultなしexportしたモジュールのimport )
import { hoge, fuga, piyo as piyoyo } from 'hoge';
```
## defaultなしexportした複数モジュールの`*`によるimport
defaultなしexportしたモジュールは`*`で一括`import`できます。  
`import * as <名前空間> from '<ファイル名>'`の形式。  
使用時は`<名前空間>.<モジュール名>`とします。
```
( defaultなしexportした複数モジュールの`*`によるimport )
import * as hoge from 'hoge';

console.log(hoge.hoge, hoge.fuga);
hoge.piyo();
```
