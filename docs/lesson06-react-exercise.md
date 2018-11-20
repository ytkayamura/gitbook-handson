# Lesson 6: React練習

Reactの`props`と`state`の使い方について学んでいきます。  
`props`はReactコンポーネントの引数です。  
コンポーネント作成時に外から渡され、値は不変です。  
一方で`state`の値は可変です。  
名前の通り、変化するコンポーネントの内部`状態`を保持するものと理解してよいでしょう。

## propsの追加
Helloコンポーネントにpropsを追加してみましょう。
### client.component.Hello.tsx
まずはpropsのinterfaceを定義します。
```
interface Props {
  initialName: string;
}
```
PropsをReact.Componentのジェネリックに指定。
```
- export default class Hello extends React.Component {
+ sexport default class Hello extends React.Component<Props> {
```
propsはReactコンポーネントの`this`に格納されます。  
`render()`の中で取り出して、値を使ってみます。  
JSXの中で`{}`を囲んだ中はTypeScriptのコードになり、スコープ内で定義された変数やコンポーネントのthis等が使用可能です。
```
  render(): JSX.Element {
    const { initialName } : Props = this.props;
    return (
      <div>Hello {initialName}!</div>
    );
  }
```

### client/index.tsx
Helloコンポーネントのpropsを定義したので、呼び出し(作成)側でそれを渡してやらなければいけません。
```
-  <Hello />,
+  <Hello initialName="React" />,
```
これでコンポーネントの追加は完了です。
index.tsxから渡す`initialName`の値を変えてやれば、`Hello xxx!`というように画面表示が変わります。  
確認してみましょう。

## stateの追加
画面表示される`Hello `の後の名前をstateにして変化できるようにしてみましょう。
### client.component.Hello.tsx
stateのinterfaceを定義します。
```
interface State {
  name: string;
}
```
StateをReact.Componentのジェネリックに指定。
```
- export default class Hello extends React.Component<Props> {
+ sexport default class Hello extends React.Component<Props, State> {
```
class定義の中でstateを定義、初期化します。
```
export default class Hello extends React.Component<Props, State> {
  state: State = {
    name: this.props.initialName,
  };
  ：
```
`render()`の中の`props.initialName`を`state.name`に変えます。
```
  render(): JSX.Element {
    const { name } : State = this.state;
    return (
      <div>Hello {name}!</div>
    );
  }
```
これでstateの追加ができましたが、まだ変化はしません。

## stateの変更
stateを変更できるボタンを追加します。

### client.component.Hello.tsx
state.nameを`太郎`と`花子`に変更するメソッドを追加します。
```
  setNameTaro: () => void = (): void => {
    this.setState({ name: '太郎' });
  }
  setNameHanako: () => void = (): void => {
    this.setState({ name: '花子' });
  }
```
`太郎`ボタンと`花子`ボタンを追加します。
```
  render(): JSX.Element {
    const { name } : State = this.state;
    return (
      <div>
        <button type="button" onClick={this.setNameTaro}>太郎</button>
        <button type="button" onClick={this.setNameHanako}>花子</button>
        <div>Hello {name}!</div>
      </div>
    );
  }
```
`太郎`ボタンを押すと`Hello 太郎!`に、`花子`ボタンを押すと`Hello 花子!`に表示が変わればOKです！

## コミット差分
前回からの差分は下記となります。  
https://gitlab.com/jabaoplus/webapp-handson-lesson/commit/1a73fddbdfd57894a29134f1330ddb699cbb7875

## 演習
ボタンのラベルが可変のコンポーネントを作り、そのコンポーネントからHelloのstate.nameを変更するようにしてみてください。  
下層のコンポーネントから上層のコンポーネントに値を渡してやるには上層からそのstateを変更するメソッド下層のコンポーネントのpropsとして渡してやるのが定石です。  
ただし、この方法はReduxを導入したらあまり使わないはずなので、飛ばして下の解答例を見てしまっても構いません。

### 解答例
https://gitlab.com/jabaoplus/webapp-handson-lesson/commit/17b70b73ffd963a35f8b7bbe4fe0dcbf3a3b68ee
