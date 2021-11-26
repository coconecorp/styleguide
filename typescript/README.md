# TypeScript/JavaScriptスタイルガイド

<details><summary>目次</summary>

- [はじめに](../typescript_javascript/README.md#はじめに)
- [言語対応レベル](../typescript_javascript/README.md#言語対応レベル)
- [TypeScript/JavaScript共通](../typescript_javascript/README.md#typescriptjavascript共通)
  - [構文](../typescript_javascript/README.md#構文)
    - [識別子](../typescript_javascript/README.md#識別子)
      - [命名スタイル](../typescript_javascript/README.md#命名スタイル)
      - [説明的な名前](../typescript_javascript/README.md#説明的な名前)
    - [ファイルエンコーディング](../typescript_javascript/README.md#ファイルエンコーディング)
    - [コメント](../typescript_javascript/README.md#コメント)
      - [JSDocと通常のコメント](../typescript_javascript/README.md#jsdocと通常のコメント)
      - [HTMLタグのサポート](../typescript_javascript/README.md#htmlタグのサポート)
      - [冗長化の回避](../typescript_javascript/README.md#冗長化の回避)
      - [@paramと@return](../typescript_javascript/README.md#paramとreturn)
  - [言語ルール](../typescript_javascript/README.md#言語ルール)
    - [コンストラクタ](../typescript_javascript/README.md#コンストラクタ)
    - [クラスメンバー](../typescript_javascript/README.md#クラスメンバー)
      - [フィールドの初期化](../typescript_javascript/README.md#フィールドの初期化)
      - [クラスの静的スコープ外で使用するプロパティ](../typescript_javascript/README.md#クラスの静的スコープ外で使用するプロパティ)
    - [プリミティブ型とラッパークラス](../typescript_javascript/README.md#プリミティブ型とラッパークラス)
    - [配列コンストラクタ](../typescript_javascript/README.md#配列コンストラクタ)
    - [変数](../typescript_javascript/README.md#変数)
    - [例外](../typescript_javascript/README.md#例外)
    - [オブジェクトの反復](../typescript_javascript/README.md#オブジェクトの反復)
    - [配列の反復](../typescript_javascript/README.md#配列の反復)
    - [スプレッド構文](../typescript_javascript/README.md#スプレッド構文)
    - [Switch文](../typescript_javascript/README.md#switch文)
    - [等価のチェック](../typescript_javascript/README.md#等価のチェック)
    - [関数式](../typescript_javascript/README.md#関数式)
      - [アロー関数](../typescript_javascript/README.md#アロー関数)
      - [式とブロック](../typescript_javascript/README.md#式とブロック)
      - [thisの再バインド](../typescript_javascript/README.md#thisの再バインド)
      - [イベントハンドラ](../typescript_javascript/README.md#イベントハンドラ)
    - [プロパティアクセサの最適化](../typescript_javascript/README.md#プロパティアクセサの最適化)
    - [デバッグ文](../typescript_javascript/README.md#デバッグ文)
  - [ソースの構成](../typescript_javascript/README.md#ソースの構成)
    - [モジュール](../typescript_javascript/README.md#モジュール)
      - [パス](../typescript_javascript/README.md#パス)
      - [名前空間とモジュール](../typescript_javascript/README.md#名前空間とモジュール)
    - [export文](../typescript_javascript/README.md#export文)
      - [コンテナクラス](../typescript_javascript/README.md#コンテナクラス)
    - [import文](../typescript_javascript/README.md#import文)
      - [インポート名の変更](../typescript_javascript/README.md#インポート名の変更)
    - [機能別の整理](../typescript_javascript/README.md#機能別の整理)
  - [コードのフォーマット](../typescript_javascript/README.md#コードのフォーマット)
    - [インデント](../typescript_javascript/README.md#インデント)
    - [空白](../typescript_javascript/README.md#空白)
    - [改行](../typescript_javascript/README.md#改行)
    - [空行](../typescript_javascript/README.md#空行)
    - [1行の文字数](../typescript_javascript/README.md#1行の文字数)
    - [セミコロン`;`](../typescript_javascript/README.md#セミコロン)
    - [波括弧`{}`](../typescript_javascript/README.md#波括弧)
    - [二項または三項の演算子](../typescript_javascript/README.md#二項または三項の演算子)
    - [クォート](../typescript_javascript/README.md#クォート)
- [TypeScript](#typescript)
  - [言語ルール](#言語ルール)
    - [識別子](#識別子)
      - [エイリアス](#エイリアス)
    - [コメント](#コメント)
      - [@override](#override)
      - [デコレーター](#デコレーター)
    - [可視性](#可視性)
    - [クラスメンバー](#クラスメンバー)
      - [readonly修飾子](#readonly修飾子)
      - [パラメータプロパティ](#パラメータプロパティ)
    - [関数宣言](#関数宣言)
    - [@ts-ignore](#ts-ignore)
    - [型アサーションと非nullアサーション演算子](#型アサーションと非nullアサーション演算子)
    - [型アサーションのシンタックス](#型アサーションのシンタックス)
    - [型アサーションとオブジェクトリテラル](#型アサーションとオブジェクトリテラル)
    - [メンバープロパティ宣言](#メンバープロパティ宣言)
    - [デコレーター](#デコレーター)
  - [型システム](#型システム)
    - [型表現](#型表現)
    - [return文の型](#return文の型)
    - [nullとundefined](#nullとundefined)
    - [オプションと`| undefined`の型](#オプションと-undefinedの型)
    - [構造的型付けと記名的型付け](#構造的型付けと記名的型付け)
    - [any型](#any型)
      - [より具体的な型の使用](#より具体的な型の使用)
    - [unknown型の使用](#unknown型の使用)
      - [lintの警告の抑制](#lintの警告の抑制)
    - [ラッパー型](#ラッパー型)

</details>

## TypeScript

### 言語ルール

#### 識別子

##### エイリアス

既存のシンボルのローカルスコープのエイリアスを作成する場合は、既存の識別子のフォーマットを使用してください。

- 【必須】ローカルエイリアスは、ソースの既存のネーミングやフォーマットと一致していなければなりません。

変数のローカルエイリアスには`const`文を使用し、クラスフィールドには`readonly`修飾子を使用します。

```typescript
// ローカルエイリアス
const {Foo} = SomeType; 
const CAPACITY = 5;
  
class Teapot {
    // クラスフィールド
    readonly BrewStateEnum = BrewStateEnum;
    readonly CAPACITY = CAPACITY;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### コメント

##### @override

- 【必須】`@override`は使用してはなりません。

`@override`はコンパイラによって強制されないため、注釈と実装が同期しなくなる場合があります。ドキュメント作成の使用は混乱を招きます。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### デコレーター

- 【必須】クラスやメソッド、プロパティに`@Component`などのデコレーターとJSDocが存在する場合、必ずデコレーターの前にJSDocを記述しなければなりません。

```typescript
// 間違い：デコレーターとdecoratedクラスの間にJSDocを記述
@Component({
  selector: 'foo',
  template: 'bar',
})
/**
 * Component that prints "bar".
 */
export class FooComponent {}
```

```typescript
// 正しい：デコレーターの前にJsDocを記述
/**
 * Component that prints "bar".
 */
@Component({
  selector: 'foo',
  template: 'bar',
})
export class FooComponent {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>


#### 可視性

プロパティ、メソッド、および型全体の可視性を制限することで、コードの分離を維持できます。

- 【必須】アクセス修飾子を使用して、メンバーのアクセス範囲をでるだけ制限しなければなりません。シンボルの視認性を可能な限り制限しなければなりません。
- 【必須】TypeScriptのシンボルのデフォルトのアクセス修飾子は`public`です。`public`修飾子はコンストラクタ内において、非読み取り専用の`public`パラメータプロパティを宣言する場合を除き使用してはいけません。


```typescript
// 間違い：
class Foo {
    public bar = new Bar(); // public装飾子は不要です

    constructor(public readonly baz: Baz) {} // readonlyはデフォルトでpublicのプロパティを意味します
}

// 正しい：
class Foo {
    bar = new Bar();

    constructor(public baz: Baz) {} // publicは許可されています
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### クラスメンバー

##### readonly修飾子

- 【必須】コンストラクタの外で再度割り当てられることのないプロパティは、`readonly`修飾子を使用しなければなりません（完全にイミュータブルである必要はありません）。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### パラメータプロパティ

- 【推奨】初期化が明らかな場合、クラスメンバーにするのではなく、パラメータプロパティの使用を推奨します。

```typescript
// 非推奨：
class Foo {
    private readonly barService: BarService;
 
    constructor(barService: BarService) {
        this.barService = barService;
    }
}

// 推奨：
class Foo {
    constructor(private readonly barService: BarService) {}
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 関数宣言

`function foo() { ... }`を使って、名前付きの関数を宣言します。これには、別の関数の中など、入れ子になったスコープの関数も含まれます。

```typescript
function foo() { ... }
```

- 【推奨】関数式はローカル変数への代入ではなく、関数宣言の使用を推奨します。

TypeScriptはあらかじめ関数の再バインドを許可していないため、`const`文を使用して関数宣言を上書きしないようにする必要はありません。

```typescript
// 間違い：上記の宣言を考えると、これはコンパイルされません
foo = () => 3; // ERROR: 代入式の左辺が無効です

// このような宣言は不要です
const foo = function() { ... }
```

ここで説明する関数宣言`function foo() { ... }`と、アロー関数の違いに注意してください。

トップレベルのアロー関数は、対象の関数がインターフェースを実装していることを明示的に宣言するために使用してよいこととします。

```typescript
interface SearchFunction {
    (source: string, subString: string): boolean;
}

const fooSearch: SearchFunction = (source, subString) => { ... };
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### @ts-ignore

- 【推奨】次の行の型チェックをスキップする`@ts-ignore`の使用は推奨しません。

`@ts-ignore`の使用はコンパイルエラーの原因の解決ではなく、あくまで表面的な解決になります。コンパイラエラーは修正可能な問題が原因の場合が多く、原因の究明と問題の解決を考えるべきです。<br>
たとえば`@ts-ignore`を使用して型エラーを抑制する場合、周囲のコードがどの型を参照するか予測するのは困難です。

```typescript
// 非推奨：
if (false) {
    // @ts-ignore: 到達不可能なコードエラー
    console.log('hello');
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 型アサーションと非nullアサーション演算子

- 【推奨】明確な理由がない限り、型アサーション`x as SomeType`と非nullアサーション演算子`y!`の使用は推奨しません。

型アサーション`x as SomeType`と非nullアサーション演算子`y!`は安全とはいえません。TypeScriptコンパイラは、これらのアサーションにマッチしたランタイムチェックは挿入しないため、ランタイムにプログラムがクラッシュする原因となります。

```typescript
// 非推奨：
(x as Foo).foo();
y!.bar();
```

代わりに、ランタイムチェックを明示的に作成します。

```typescript
// 推奨：
if (x instanceof Foo) {
    x.foo();
}
if (y) {
    y.bar();
}
```

- 【推奨】コードのローカルな特性により、アサーション形式が安全であると確信できる場合があります。そのような場合には、安全でない動作でも問題がない理由をコメントとともに使用することを推奨します。

```typescript
// xはFooです。なぜなら....
(x as Foo).foo();

// yはnullにはなりません。なぜなら....
y!.bar();
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 型アサーションのシンタックス

- 【必須】型アサーションは、山括弧`<>`ではなく、`as`構文を使用しなければなりません。

```typescript
// 間違い：
const x = (<Foo>z).length;
const y = <Foo>z.length;
```

`as`構文を使用することで、メンバーへのアクセス時にアサーションを丸括弧`()`で囲むことが強制されます。

```typescript
// 正しい：
const x = (z as Foo).length;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 型アサーションとオブジェクトリテラル

- 【推奨】オブジェクトリテラルの型を指定する場合、型アサーション`as Foo`ではなく、型アノテーション`:Foo`の使用を推奨します。

型アノテーション`:Foo`の使用で、インターフェースのフィールドが変更した場合のリファクタリングのバグを検出できます。

```typescript
// 非推奨：型アサーションの使用
interface Foo {
    bar: number;
    baz?: string; // は元々bamで後にbazに改名
}

const foo = {
    bar: 123,
    bam: 'abc', // エラーとして検知されない
} as Foo; // 型アサーション

function func() {
    return {
        bar: 123,
        bam: 'abc', // エラーとして検知されない
    } as Foo; // 型アサーション
}
```

```typescript
// 推奨：型アノテーション
interface Foo {
    bar: number;
    baz?: string;
}

const foo: Foo = { // 型アノテーション
    bar: 123,
    bam: 'abc', // エラーとして検知
};

function func(): Foo { // 型アノテーション
    return {
        bar: 123,
        bam: 'abc', // エラーとして検知
    };
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### メンバープロパティ宣言

- 【必須】インターフェースとクラスの宣言では、個々のメンバーの宣言を分離するためにセミコロン`;`を使用しなければなりません。

```typescript
// 正しい：
interface Foo {
  memberA: string;
  memberB: number;
}
```

- 【必須】インターフェースでは特に、クラス宣言との対称性を考慮して、フィールドを区切るためにカンマ`,`を使用してはいけません。

```typescript
// 間違い：
interface Foo {
  memberA: string,
  memberB: number,
}
```

- 【必須】型エイリアスと、インラインオブジェクトタイプ宣言では区切り文字としてカンマ`,`を使用しなければなりません。

```typescript
// 型エイリアス
type SomeTypeAlias = {
  memberA: string,
  memberB: number,
};
 
// インラインオブジェクトタイプ宣言
let someProperty: {memberC: string, memberD: number};
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### デコレーター

- 【必須】新しいデコレーターを定義してはいけません。フレームワークで定義されているデコレーターのみを使用すべきです。

デコレーターは実験的な機能であり、TC39の提案から乖離しており、修正されない既知のバグがあるため、一般的には避けたほうが無難です。

- 【必須】デコレーターを使用する場合、デコレーターはデコレーションするシンボルの直前に置かなけれななりません。空行も入れません。

```typescript
@Component({...}) // デコレーターの後には空行も入れません
class MyComp {
    @Input() myField: string; // フィールド上のデコレーターは、同じ行にあるかもしれません
 
    @Input()
    myOtherField: string; // もしくはラップします
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 型システム

#### 型表現

コードは、すべての型表現（変数、フィールド、戻り値の型など）について、TypeScriptコンパイラが実装する型推論に依存してよいこととします。

```typescript
const x = 15; // 型の推測が容易
```

文字列、数値、ブール値、`RegExp`リテラル、新しい式で初期化された変数やパラメータなど、些細なことから推測できる型については、型アノテーションを省略します。

```typescript
// 間違い：
const x: boolean = true; // booleanが読みやすさに欠ける
const x: Set<string> = new Set(); // 初期化によってSetがstring型と推測できるので型アノテーションを省略可能

// 正しい：
const x = new Set<string>();
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### return文の型

- 【推奨】関数やメソッドの戻り値について、型アノテーションの使用を推奨します。

```typescript
// 非推奨：型アノテーション無し
function identity(num: number) {
    return num;
}
 
// 推奨：型アノテーションの使用
function identity(num: number): number {
    return num;
}
```

関数やメソッドの戻り値の明示は、2つのメリットがあります。

- コードの読者に役立つ、より正確なドキュメントになります。
- コードを変更して関数の戻り値の型が変わった場合、型が原因のエラーをより早く発見できます。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### nullとundefined

- 【必須】型エイリアスについて、ユニオン型に`| null`または`| undefined`を含めるべきではありません。

`null`値のエイリアスは通常、アプリケーションの多くの層で`null`値が受け渡されていることを示しており、`null`値になった元々の問題の原因を不明にしています。また、クラスやインターフェースの特定の値が存在しない場合も不明瞭になります。

- 【必須】代わりに、エイリアスが実際に使用する場合だけ`| null`または`| undefined`を追加すべきです。コードは、`null`値が発生する場所の近くで`null`値を処理すべきです。

```typescript
// 間違い：
type CoffeeResponse = Latte | Americano | undefined;

class CoffeeService {
    getLatte(): CoffeeResponse { ... };
}

// 正しい：
type CoffeeResponse = Latte | Americano;

class CoffeeService {
    getLatte(): CoffeeResponse | undefined { ... };
}

// より正しい：
type CoffeeResponse = Latte | Americano;

class CoffeeService {
    getLatte(): CoffeeResponse {
        return assert(fetchResponse(), 'Coffee maker is broken, file a ticket');
    };
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### オプションと`| undefined`の型

TypeScriptは、プロパティや引数に`?`を付与する特別な構文があります。

```typescript
interface CoffeeOrder {
  sugarCubes: number;
  milk?: Whole | LowFat | HalfHalf;
}
 
function pourCoffee(volume?: Milliliter) { ... }
```

`?`を付与したパラメータは、暗黙的に型に`| undefined`を含みます。ただし、値を作成したりメソッドを呼び出したりする場合に省略できるという点が異なります。<br>
たとえば上記について、`{sugarCubes: 1}`は`milk`プロパティがオプションなので、有効な`CoffeeOrder`です。

- 【必須】インターフェースやクラスのオプションのフィールドやパラメータでは、`| undefined`ではなく、`?`を使用しなければなりません。

なお、クラスの場合はこのパターンよりも、できるだけ多くのフィールドを初期化したほうがのぞましいです。

```typescript
class MyClass {
    field = '';
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 構造的型付けと記名的型付け

コード内の適切な場所で型付けを指定してください。テストコード以外では、インターフェイスを使って構造的な型を定義してください。テストコードでは、余分なインターフェイスを追加せず、モック実装をテスト対象のコードと構造的に一致させると便利です。

構造ベースの実装をする場合は、シンボルの宣言時に型を明示します。これにより、より正確な型チェックとエラー報告が可能になります。

```typescript
// 正しい：
const foo: Foo = {
  a: 123,
  b: 'abc',
}
```

```typescript
// 間違い：
const badFoo = {
  a: 123,
  b: 'abc',
}
```

`badFoo`オブジェクトは、型推論に依存しています。`badFoo`には新たにフィールドを追加できますが、型はオブジェクトに基づいて推論されます。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### any型

- 【必須】`any`型の使用禁止を検討すべきです。

TypeScriptの`any`型は、他のすべての型のスーパータイプとサブタイプであり、すべてのプロパティを参照できます。重大なプログラミングエラーを隠してしまう可能性があり、そもそも静的型をもつことの価値を損なうため、使用には検討が必要です。

`any`型を使用する場合、次のいずれかを検討します。

- より具体的な型を使用できないか
- `unknown`型を使用できないか
- lintの警告を抑制し、理由をコメントで文書化できないか

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### より具体的な型の使用

インターフェース、インラインのオブジェクトタイプ、またはタイプエイリアスを使用します。

```typescript
// 宣言されたインタフェースを使って、サーバーサイドのJSONを表現します
declare interface MyUserJson {
    name: string;
    email: string;
}

// 頻繁に使用る型には、型エイリアスを使用します
type MyType = number | string;

// または、複雑な返しにはインラインのオブジェクトタイプを使用します
function getTwoThings(): {something: number, other: string} {
    // ...
    return {something, other};
}

// ジェネリクス型を使用します。そうでなければ、ライブラリは any型と表現します
// ユーザーがどのような型で操作しているかは気にしません（ただし、『戻り値の
// ジェネリック型のみ』に注意してください）。
function nicestElement<T>(items: T[]): T {
    // コードはTに制約を加えることもできます。例えば、<T extends HTMLElement>などです。
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### unknown型の使用

`any`型は他の任意の型への代入とその型から任意のプロパティを参照できます。多くの場合、このような動作は不必要で望ましくなく、型が不明であることを明示する必要があります。このような場合に`unknown`型を使用してください。`unknown`型は概念を表現し、任意のプロパティの参照解除を許容しないためより安全です。

```typescript
// 間違い：
const danger: any = value /* 任意の式の結果 */;
danger.whoops(); // このアクセスは全くチェックされていません

// 正しい：
// nullやundefinedを含む任意の値を割り当てることができますが、
// 型の絞り込みやキャストなしには使用できません
const val: unknown = value;　
```

型が不明な値を安全に使用するために、『[型ガード](https://typescript-jp.gitbook.io/deep-dive/type-system/typeguard)』を使用してタイプを絞り込みます。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### lintの警告の抑制

たとえばモックオブジェクトを構築するテストでの`any`型の使用は正当な場合があります。そのような場合には、lintの警告を抑制するコメントを追加し、なぜそれが正当なのかを文書化します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### ラッパー型

JavaScriptのプリミティブに関連して、Typescriptでは絶対に使用してはいけない型がいくつか存在します。

- 【必須】`String`、`Boolean`、`Number`オブジェクトではなく、プリミティブ型の`string`、`boolean`、`number`を使用しなければなりません。

`String`、`Boolean`、`Number`オブジェクトと、対応するプリミティブ型の`string`、`boolean`、`number`は若干意味が異なります。

```typescript
let str1: string = 'test';
let str2 = new String('test');

console.log(`str1: ${str1}`); // str1: test
console.log(`str2: ${str2}`); // str2: test
console.log(`typeof str1: ${typeof(str1)}`); // typeof str1: string
console.log(`typeof str2: ${typeof(str2)}`); // typeof str2: object
console.log(`str1 == str2: ${str1 == str2}`); // str1 == str2: true
console.log(`str1 === str2: ${str1 === str2}`); // str1 === str2: false
```

常に小文字のバージョンを使用してください。

```typescript
// 間違い：
const bool: Boolean = false;
const num: Number = 0;
const str: String = '';
const sym: Symbol = Symbol();
const big: BigInt = 10n;
```

- 【必須】`null`値と`undefined`以外のすべてを含む型には波括弧`{}`を、他のプリミティブ型（前述の3つに加え、`symbol`と`bigint`）をさらに除外したい場合、小文字の`object`を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>
