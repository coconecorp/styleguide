# TypeScript/JavaScriptスタイルガイド

<details><summary>目次</summary>


- [はじめに](#はじめに)
- [言語対応レベル](#言語対応レベル)
- [TypeScript/JavaScript共通](#typescriptjavascript共通)
  - [構文](#構文)
    - [識別子](#識別子)
      - [命名スタイル](#命名スタイル)
      - [説明的な名前](#説明的な名前)
    - [ファイルエンコーディング](#ファイルエンコーディング)
    - [コメント](#コメント)
      - [JSDocと通常のコメント](#jsdocと通常のコメント)
      - [HTMLタグのサポート](#htmlタグのサポート)
      - [冗長化の回避](#冗長化の回避)
      - [@paramと@return](#paramとreturn)
  - [言語ルール](#言語ルール)
    - [コンストラクタ](#コンストラクタ)
    - [クラスメンバー](#クラスメンバー)
      - [フィールドの初期化](#フィールドの初期化)
      - [クラスの静的スコープ外で使用するプロパティ](#クラスの静的スコープ外で使用するプロパティ)
    - [プリミティブ型とラッパークラス](#プリミティブ型とラッパークラス)
    - [配列コンストラクタ](#配列コンストラクタ)
    - [変数](#変数)
    - [例外](#例外)
    - [オブジェクトの反復](#オブジェクトの反復)
    - [配列の反復](#配列の反復)
    - [スプレッド構文](#スプレッド構文)
    - [Switch文](#switch文)
    - [等価のチェック](#等価のチェック)
    - [関数式](#関数式)
      - [アロー関数](#アロー関数)
      - [式とブロック](#式とブロック)
      - [thisの再バインド](#thisの再バインド)
      - [イベントハンドラ](#イベントハンドラ)
    - [プロパティアクセサの最適化](#プロパティアクセサの最適化)
    - [デバッグ文](#デバッグ文)
  - [ソースの構成](#ソースの構成)
    - [モジュール](#モジュール)
      - [パス](#パス)
      - [名前空間とモジュール](#名前空間とモジュール)
    - [export文](#export文)
      - [コンテナクラス](#コンテナクラス)
    - [import文](#import文)
      - [インポート名の変更](#インポート名の変更)
    - [機能別の整理](#機能別の整理)
  - [コードのフォーマット](#コードのフォーマット)
    - [インデント](#インデント)
    - [空白](#空白)
    - [改行](#改行)
    - [空行](#空行)
    - [1行の文字数](#1行の文字数)
    - [セミコロン`;`](#セミコロン)
    - [波括弧`{}`](#波括弧)
    - [二項または三項の演算子](#二項または三項の演算子)
    - [クォート](#クォート)
- [TypeScript](../typescript/README.md#typescript)
  - [言語ルール](../typescript/README.md#言語ルール)
    - [識別子](../typescript/README.md#識別子)
      - [エイリアス](../typescript/README.md#エイリアス)
    - [コメント](../typescript/README.md#コメント)
      - [@override](../typescript/README.md#override)
      - [デコレーター](../typescript/README.md#デコレーター)
    - [可視性](../typescript/README.md#可視性)
    - [クラスメンバー](../typescript/README.md#クラスメンバー)
      - [readonly修飾子](../typescript/README.md#readonly修飾子)
      - [パラメータプロパティ](../typescript/README.md#パラメータプロパティ)
    - [関数宣言](../typescript/README.md#関数宣言)
    - [@ts-ignore](../typescript/README.md#ts-ignore)
    - [型アサーションと非nullアサーション演算子](../typescript/README.md#型アサーションと非nullアサーション演算子)
    - [型アサーションのシンタックス](../typescript/README.md#型アサーションのシンタックス)
    - [型アサーションとオブジェクトリテラル](../typescript/README.md#型アサーションとオブジェクトリテラル)
    - [メンバープロパティ宣言](../typescript/README.md#メンバープロパティ宣言)
    - [デコレーター](../typescript/README.md#デコレーター)
  - [型システム](../typescript/README.md#型システム)
    - [型表現](../typescript/README.md#型表現)
    - [return文の型](../typescript/README.md#return文の型)
    - [nullとundefined](../typescript/README.md#nullとundefined)
    - [オプションと`| undefined`の型](../typescript/README.md#オプションと-undefinedの型)
    - [構造的型付けと記名的型付け](../typescript/README.md#構造的型付けと記名的型付け)
    - [any型](../typescript/README.md#any型)
      - [より具体的な型の使用](../typescript/README.md#より具体的な型の使用)
    - [unknown型の使用](../typescript/README.md#unknown型の使用)
      - [lintの警告の抑制](../typescript/README.md#lintの警告の抑制)
    - [ラッパー型](../typescript/README.md#ラッパー型)

</details>

## はじめに

- 本ガイドラインは、[ココネ株式会社](https://www.cocone.co.jp/)のTypeScriptとJavaScriptのスタイル基準を示すものです。
- 本ガイドラインについて、TypeScriptは『[Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)』、JavaScriptは『[Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)』を参考に規定しています。
- 本ガイドラインで未定義のスタイルや、詳細を定義していない箇所の議論となった場合は、『[Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)』と『[Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)』を参考に議論することとします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## TypeScript/JavaScript共通

注意：本セクションの各規定は、原則としてTypeScript/JavaScript共通の規定になります。TypeScriptもしくはJavaScriptを対象とした規定は、次のラベルを先頭に付け、言語対応レベルを明示しています。

- **（TS）** TypeScriptのみ対象の規定です
- **（JS）** JavaScriptのみ対象の規定です

### 構文

#### 識別子

- 【必須】識別子は、ASCII文字、数字、アンダースコア（定数および構造化されたテストメソッド名の場合）を使用しなければなりません。

スタイル  | カテゴリ
------------- | -------------
UpperCamelCase  | クラス、インターフェース、型、列挙型、デコレーター、型パラメータ
lowerCamelCase  | 変数、パラメータ、関数、メソッド、プロパティ、モジュールエイリアス
CONSTANT_CASE | 列挙型の値を含むグローバルな定数

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### 命名スタイル

TypeScript：

- 【推奨】（TS）TypeScriptは情報を型で表現するので、名前に型情報を含むことは推奨しません。

具体的な例は次になります。

- プライベートなプロパティやメソッドの先頭にアンダースコア`_`を付与しない。
- オプションのパラメータに`opt_`というような接頭辞を付与しない。

JavaScript：

型が存在しないため、名前に型情報を含め認識しやすくします。<br>
具体的な例は次になります。

- 【推奨】（JS）プライベートなプロパティやメソッドは先頭にアンダースコア`_` の付与を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### 説明的な名前

- 【必須】名前は説明的で、初めて読む人にとっても分かりやすいものでなければなりません。曖昧で馴染みのない略語を使用したり、単語を省略したりしてはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### ファイルエンコーディング

- 【必須】エンコーディングはHTML、CSS同様、UTF-8（BOMなし）でなければなりません。
- 【推奨】原則として、実体参照の使用は推奨しません。

非ASCII文字については、Unicode文字（例：`∞`）を使用してください。印刷不可能な文字は、同等の16進数またはUnicodeのエスケープを説明したコメントとともに使用できます（例： `'\u221e' // ∞です`）。

```javascript
// 正しい：コメントがなくてもわかります
const units = 'μs';
 
// 正しい：印刷できない文字にはコメントを追記します
const output = '\ufeff' + content; // BOM

// 間違い：コメントがあっても読みづらく、ミスが起こりやすい
const units = '\u03bcs'; // ギリシャ文字のμs
 
// 間違い：コメントが付与されていないため、何の意味なのかわかりません
const output = '\ufeff' + content;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### コメント

##### JSDocと通常のコメント

コメントには、JSDocのコメント`/** ... */`と、通常のコメント`// `、`/* ... */`の2種類があります。

- 【推奨】プログラムの説明をドキュメントで残す場合、JSDocのコメント`/** ... */`の使用を推奨します。
- 【推奨】ドキュメントで残さない場合、通常のコメント`//`の使用を推奨します。

```javascript
// JSDocのコメント
/**
 * JSDocコメントはスラッシュ`/`と2つのアスタリスク`*`から始めます
 * インラインタグは {@code this} のように波括弧`{}`で囲みます
 * @desc ブロックタグは必ず行の先頭から開始します
 */
```

JSDocのコメントは、JSDocをサポートするエディタやドキュメント作成ツールなど、ツールが解析できるコメントです。<br>
次のような場面で使用します。

- `export`文を使用した、関数や変数、オブジェクト、クラスの`public`の各メンバー
- （TS）`export`文を使用した、列挙型`enum`の各定数

```typescript
// 例：列挙型の各定数の解説をツールで表示する場合
// 推奨：JSDocのコメントを使用。エディタ上で列挙型AgeTypeにマウスオーバーすると、各定数がコードヒントで表示される
export enum AgeType {
    /** 15歳以下 */
    Child = 1,
    /** 16歳～19歳 */
    Teen = 2,
    /** 20歳以上 */
    Adult = 3,
}

// 非推奨：通常のコメントを使用。対象のファイルを開かないと、各定数を確認できない
export enum AgeType {
    Child = 1, // 15歳以下
    Teen = 2, // 16歳～19歳
    Adult = 3, //20歳以上
}
```

通常のコメントは、書式のルールはありません。

```typescript
// 最後にupdateを実行した時間
protected lastUpdateTime = 0;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### HTMLタグのサポート

JSDocは`<code>` `<pre>` `<tt>` `<strong>` `<ul>` `<ol>` `<li>` `<a>` などHTMLタグをサポートしています。<br>
これは、プレーンテキストに書式を設定しても無視することを意味します。このため、スペースによってJSDocを整形しようとせず、HTMLタグを使用します。

```javascript
/**
 * 以下の3つの要因に基づいて重さを計算します：
 *    - 送った項目
 *    - 受け取った項目
 *    - タイムスタンプ
 */
```

上のコメントはツールで次のように表示されます。

```javascript
以下の3つの要因に基づいて重さを計算します：    - 送った項目   - 受け取った項目   - タイムスタンプ
```

代わりにHTMLタグを使用します。

```javascript
/**
 * 以下の3つの要因に基づいて重さを計算します：
 * <ul>
 * <li>送った項目
 * <li>受け取った項目
 * <li>タイムスタンプ
 * </ul>
 */
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### 冗長化の回避

JSDocのコメントは冗長化を避けるため、規定しているすべてのブロックタグを使用する必要はありません。たとえば、`implements` `enum` `private`などのキーワードを使用しているコードに対し、`@implements` `@enum` `@private`のブロックタグを使用した文書化は不要です。

詳しくはJSDocの『[Block Tags](https://jsdoc.app/#block-tags)』をご覧ください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### @paramと@return

- 【推奨】（JS）パラメータと戻り値が存在する場合、`@param`と`@return`の記述を推奨します。
- 【必須】（JS）可読性向上のため、`@param`や`@return`を記述する場合、型宣言をしなければなりません。

```javascript
/**
 * 進行ベクトルの取得
 * @param {number} elapsedTime // 前フレームからの経過時間
 * @return {{x: number, y:number}}
 */
getVector(elapsedTime: number): { x: number; y: number } {
    return {
        x: (this.vector.x / 1000) * elapsedTime,
        y: (this.vector.y / 1000) * elapsedTime,
    };
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 言語ルール

#### コンストラクタ

- 【必須】引数を渡さない場合でも、コンストラクタ呼び出し時は丸括弧`()`を使用しなければなりません。

```javascript
// 間違い：
const x = new Foo;
 
// 正しい：
const x = new Foo();
```

- 【推奨】ES2015ではコンストラクタを指定していない場合、デフォルトのクラスコンストラクタが提供されるため空のコンストラクタの指定は不要です。ただし空の場合でもパラメータプロパティ、修飾子、またはパラメータデコレーターをもつコンストラクタは省略しないことを推奨します。

```typescript
// 間違い：
class UnnecessaryConstructor {
    constructor() {}
}
 
class UnnecessaryConstructorOverride extends Base {
    constructor(value: number) {
        super(value);
    }
}
```

```typescript
// 例：TypeScriptの場合
// 正しい：
class DefaultConstructor {
}
 
// パラメータプロパティ
class ParameterProperties {
    constructor(private myService) {}
}
 
// パラメータデコレーター
class ParameterDecorators {
    constructor(@SideEffectDecorator myService) {}
}
 
// 修飾子
class NoInstantiation {
    private constructor() {}
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### クラスメンバー

##### フィールドの初期化

- 【推奨】クラスのメンバーがパラメータでない場合は、宣言場所での初期化を推奨します。

```typescript
// 間違い：
class Foo {
    private readonly userList: string[];
 
    constructor() {
      this.userList = [];
    }
}
 
// 正しい：
class Foo {
    private readonly userList: string[] = [];
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### クラスの静的スコープ外で使用するプロパティ

ゲッターとセッター

- 【必須】ゲッターは結果が一貫しており、副作用がない純粋な関数（つまり結果が一貫しており、副作用がない）でなければなりません。


ゲッターとセッターは、内部的な実装の詳細や冗長な実装の可視性を制限する手段としても有用です。

```typescript
// TypeScriptのゲッタとセッタの例
class Foo {
  constructor(private readonly someService: SomeService) {}
 
  get someMember(): string {
    return this.someService.someVariable;
  }
 
  set someMember(newValue: string) {
    this.someService.someVariable = newValue;
  }
}
```

アクセサを使用してクラスのプロパティを非表示にする場合、非表示にするプロパティの前に`internal`や`wrapped`などの任意の単語を付けることができます。<br>
このようなプライベートなプロパティを使用する場合は、可能な限りアクセサを通して値にアクセスしてください。


- 【必須】プロパティを隠すためだけにアクセサを使用してはいけません。ゲッターとセッターのいずれかはロジックをもつものにすべきです。

ゲッタとセッターがロジックを持たない場合、プロパティを`public`にします。セッターが存在せず、ゲッターがロジックを持たない場合、プロパティを`readonly`にします。

```typescript
// 例：TypeScriptの場合
// 正しい：
class Foo {
  private wrappedBar = '';
 
  get bar() {
    return this.wrappedBar || 'bar';
  }
 
  set bar(wrapped: string) {
    this.wrappedBar = wrapped.trim();
  }
}
```

```typescript
// 例：TypeScriptの場合
// 間違い：プロパティを隠すためだけにパススルーのアクセサを定義
class Bar {
  private barInternal = '';
 
  // どちらのアクセサもロジックを持っていないので、barをpublicにするだけです
  get bar() {
    return this.barInternal;
  }
 
  set bar(value: string) {
    this.barInternal = value;
  }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### プリミティブ型とラッパークラス

- 【必須】プリミティブ型である`String`、`Boolean`、`Number`のラッパークラスをインスタンス化してはいけません。


ラッパークラスは、`new Boolean(false)`が`true`に評価されるなど、予想外の動作をします。

```javascript
// 間違い：
const s = new String('hello');
const b = new Boolean(false);
const n = new Number(5);
 
// 正しい：
const s = 'hello';
const b = false;
const n = 5;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 配列コンストラクタ

- 【必須】`Array()`コンストラクタは、混乱を招くおそれがあるため、`new`の有無にかかわらず、使用してはいけません。

```javascript
// 間違い：
const a = new Array(2); // [undefined, undefined];
const b = new Array(2, 3); // [2, 3];
```

代わりに、配列の初期化には常にブラケット表記（角括弧`[]`）を使用します。

```javascript
// 正しい：
const a = [2];
const b = [2, 3];
 
// Array(2)と同じ
const c = [];
c.length = 2;
```

サイズのある配列の初期化は`Array.from()`メソッドを使用する方法があります。

```typescript
Array.from<number>({length: 5}).fill(0); // [0, 0, 0, 0, 0]
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 変数

- 【必須】変数を宣言する場合は、`var`文は使用せず、必ず`const`文または`let`文を使用しなければなりません。

```javascript
const foo = otherValue; // 絶対に変更されない場合、const文を使用
let bar = someValue; // 再割当てがある場合、let文を使用
```

`const`文と`let`文は、他の多くの言語の変数と同様に、ブロックにスコープされています。JavaScriptの`var`文は関数にスコープされており、理解しにくいバグの原因となります。使わないようにしましょう。

```javascript
var foo = someValue; // var文は複雑でバグの原因となるので、使用しない
```

- 【必須】変数は、その宣言前に使用してはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 例外

- 【必須】例外をインスタンス化する場合、`Error()`ではなく、`new Error()`を使用しなければなりません。

どちらの形式も新しい`Error`インスタンスを生成しますが、`new`を使用したほうが他のオブジェクトのインスタンス化の方法と一貫性があります。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### オブジェクトの反復

- 【必須】フィルタリングされていない`for...in`文は使用してはいけません。

`for...in`文でオブジェクトを反復すると、プロトタイプチェインから列挙可能なプロパティが含まれてしまい、エラーが発生しやすくなります。

```javascript
// 間違い：
for (const x in someObj) {
    // xは、プロトタイプチェインから列挙可能なプロパティが含まれる可能性があります
}
```

代わりに`if`文で明示的に値をフィルタリングするか、`for (... of Object.keys(...))`を使用してください。

```javascript
// 正しい：
for (const x in someObj) {
    if (!someObj.hasOwnProperty(x)) continue;
    // xは someObjで確実に定義されている
}

for (const x of Object.keys(someObj)) { // note: for _of_!
    // 上記同様、xはsomeObjで確実に定義されている
}

for (const [key, value] of Object.entries(someObj)) { // note: for _of_!
    // keyは someObjで確実に定義されている
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 配列の反復

- 【必須】配列の反復処理に`for...in`文を使用してはいけません。

`for...in`文は配列の値ではなく、配列のインデックスを文字列として提供します。

```javascript
// 間違い：
const someArray = [5, 4, 3, 2, 1];
for (const x in someArray) {
    // xはindex
    console.log(x); // 0, 1, 2....
}
```

代わりに、`for...of`文またはインデックス付きの`for`文を使用してください。

```javascript
// 正しい：
for (const x of someArray) {
    // x はsomeArrayの値
}

for (let i = 0; i < someArray.length; i++) {
    // インデックスが必要な場合は明示的にカウントし、そうでない場合はfor-ofを使用
    const x = someArray[i];
    // ...
}

for (const [i, x] of someArray.entries()) {
    // 上記の代替バージョン
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### スプレッド構文

-【必須】スプレッド構文を使用する場合、スプレッドされる値は、生成されるものと一致していなければなりません。つまり、オブジェクトを作成する場合スプレッドできるのはオブジェクトのみであり、配列を作成する場合スプレッドできるのは配列のみです。`null`値や`undefined`などのプリミティブにスプレッド構文を使用してはいけません。

```javascript
// 間違い：
const foo = {num: 7};
const bar = {num: 5, ...(shouldUseFoo && foo)}; // undefinedの可能性があります

const fooStrings = ['a', 'b', 'c'];
const ids = {...fooStrings}; // {0： 'a'、1： 'b'、2： 'c'}を作成しますが、長さはありません

// 正しい：
const foo = shouldUseFoo ? {num: 7} : {};
const bar = {num: 5, ...foo};

const fooStrings = ['a', 'b', 'c'];
const ids = [...fooStrings, 'd', 'e'];
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### Switch文

- 【必須】`switch`文はコードが含まれていない場合でも、すべての文に`default`節を含めなければなりません。

```javascript
// 間違い：
switch (x) {
    case X:
        doSomething();
        // 許可されていません
    case Y:
        // ...
}

// 正しい：
switch (x) {
    case X:
    case Y:
        doSomething();
        break;
    default: // 何もしません
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 等価のチェック

- 【必須】原則として、厳密等価`===`と厳密不等価演算子`!==`を使用しなければなりません。

等価演算子`==`や不等価演算子`!=`は型強制が発生するため、エラーが発生しやすくなります。

参考：[JS Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)

```javascript
// 間違い：
if (foo == 'bar' || baz != bam) {
    // 型強制のため、動作の理解が困難
}

// 正しい：
if (foo === 'bar' || baz !== bam) {
    // ....
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 関数式

##### アロー関数

- 【必須】関数がコールバックなど値として使用している場合、`function`キーワードで定義されたES6以前の関数式ではなく、常にアロー関数を使用しなければなりません。

```javascript
// 間違い：
bar(function() { ... })

// 正しい：
bar(() => { this.doSomething(); })
```

- 【推奨】関数式（`function`キーワードで定義）は、コードが動的に`this`を再バインドする必要がある場合にのみ使用できますが、一般的には`this`の再バインドは推奨しません。
- 【推奨】通常の関数（アロー関数やメソッドではなく）の`this`へのアクセスは推奨しません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### 式とブロック

必要に応じて、式や波括弧`{}`を本体とするアロー関数を使用します。

```typescript
// トップレベルの関数は関数宣言を使用
function someFunction() {
    // アロー関数： 本文に処理の行があるので、波括弧`{}`とreturn文を使用
    const receipts = books.map((b: Book) => {
        const receipt = payMoney(b.price);
        recordTransaction(receipt);
        return receipt;
    });
    
    // アロー関数：
    // 本体の中括弧を削除と "return" 文を省略　- return文が含まれる
    // 引数が1つの場合、丸括弧`()`は省略が可能
    const longThings = myValues.filter(v => v.length > 1000).map(v => String(v));
    
    function payMoney(amount: number) {
        // 関数の宣言は問題ありませんが、この中で `this` にアクセスしてはいけません
    }
}
```

- 【必須】引数が1つの場合でも、引数の周りに丸括弧`()`を指定しなければなりません。

一貫性を保つため、引数が複数の場合や無い場合はもちろん、引数が1つの場合でも、引数の周りに丸括弧`()`を指定します。

```javascript
// 正しい：引数あり
const sample1 = (a, b) => a + b + 100;
console.log(sample1(1,3));

// 正しい：引数なし
let c = 4;
let d = 2;
const sample2 = () => c + d + 100;
console.log(sample2());

// 間違い：引数が1つ（丸括弧`()`を省略）
let g = 3;
const sample3 = e => e + g + 100;
console.log(sample3(1));

// 正しい：引数が1つ
let h = 3;
const sample4 = (e) => e + h + 100;
console.log(sample4(1));
```

本文に処理の追加の行が必要な場合は、波括弧`{}`と`return`文を指定します。

```javascript
// 正しい：
const transformed = [1, 2, 3].map(v => {
    const intermediate = someComplicatedExpr(v);
    const more = acrossManyLines(intermediate);
    return worthWrapping(more);
});
```

```javascript
// 間違い：関数の戻り値を利用しない場合は、波括弧`{}`の指定が必要です。
myPromise.then(v => console.log(v));
 
// 正しい： 
myPromise.then(v => {
  console.log(v);
});
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### thisの再バインド

- 【必須】関数内では、 `this`を再バインドする目的で特別に存在する場合を除き、`this`を使用してはいけません。

ほとんどの場合、アロー関数や明示的なパラメータを使用することで、`this`の再バインドを回避できます。

```javascript
// 間違い：
function clickHandler() {
    // この文脈でのthisは何ですか？
    this.textContent = 'Hello';
}
// thisは暗黙的にdocument.bodyに設定されてしまいます
document.body.onclick = clickHandler;
```

```javascript
// 正しい：
// アロー関数でオブジェクトを明示的に参照
document.body.onclick = () => {
    document.body.textContent = 'hello';
 }
// 別の方法として、明示的にパラメータを取る
const setTextFn = (e: HTMLElement) => { 
    e.textContent = 'hello';
}
// bindの使用
document.body.onclick = setTextFn.bind(null, document.body);
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### イベントハンドラ

イベントハンドラは、ハンドラをアンインストールする必要がない場合（たとえば、イベントがクラス自身によって発せられている場合）には、アロー関数を使用をお勧めします。ハンドラをアンインストールする必要がある場合は、アロー関数のプロパティを使用するのが正しい方法です。

```javascript
// イベントハンドラーは、無名関数やアロー関数のプロパティでもよい
class Component {
    onAttached() {
        // イベントはこのクラスから発せられるので、アンインストールは不要
        this.addEventListener('click', () => {
            this.listener();
        });
        // this.listenerはステーブルな参照なので、後でアンインストールできます
        window.addEventListener('onbeforeunload', this.listener);
    }
    
    onDetached() {
        // このイベントはwindowのイベントす。アンインストールしない場合、
        // this.listenerはthisへの参照を保持することになり、メモリリークが発生します
        window.removeEventListener('onbeforeunload', this.listener);
    }
    // プロパティに格納されたアロー関数は、自動的に `this` にバインドされます
    private listener = () => {
        confirm('Do you want to exit the page?');
    }
}
```

- 【必須】イベントハンドラを指定する式の中で`bind`メソッドを使用してはいけません。

```javascript
// 間違い：リスナーをバインドすることで、一時的な参照が作成され、アンインストールを防ぐことができます
class Component {
    onAttached() {
        // これにより、アンインストールできない一時的な参照が作成されます
        window.addEventListener('onbeforeunload', this.listener.bind(this));
    }
    
    onDetached() {
        // このバインドでは別の参照が作成されるので、この行は何もしません
        window.removeEventListener('onbeforeunload', this.listener.bind(this));
    }
    
    private listener() {
        confirm('Do you want to exit the page?');
    }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### プロパティアクセサの最適化

- 【必須】プロパティにアクセスする場合、ドット表記法と、ブラケット表記法を混在すべきではありません。

```javascript
// 間違い：ドット表記法とブラケット表記法の混在。アプリケーション全体で一貫して使用する必要があります
console.log(x['someField']);
console.log(x.someField);
```

- 【必須】（TS）コードは名前の変更を防ぐために、アプリケーションの外部にあるすべてのプロパティを宣言しなければなりません。

TypeScriptはアプリケーションの外部にあるすべてのプロパティを宣言し、名前の変更を防ぎます。

```typescript
// 正しい：interfaceを用いて、外部にある全てのプロパティを宣言
declare interface ServerInfoJson {
    appVersion: string;
    user: UserJson;
}
 
const data = JSON.parse(serverResponse) as ServerInfoJson;
console.log(data.appVersion);
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### デバッグ文

- 【必須】デバッグ文を本番コードに含めるべきではありません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### ソースの構成

#### モジュール

##### パス

- 【必須】他のファイルをインポートする場合、パスを指定しなければなりません。
- 【推奨】同じ（論理的な）プロジェクト内のファイルを参照する場合、原則として絶対パスの`/to/foo`ではなく`./foo`のような相対パスのインポートの使用を推奨します。

パス数の制限を検討してください。`../../../`のようにパスが深いと、モジュールやパスの構造がわかりにくくなります。

```javascript
import {Symbol1} from 'google3/path/from/root';
import {Symbol2} from '../parent/file';
import {Symbol3} from './sibling';
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### 名前空間とモジュール

- 【必須】インポートに`import x = require('...');`のように`require`構文は使用してはいけません。ES6のモジュール構文を使用します。
- 【必須】（TS）`namespace Foo{...}`は使用してはいけません。ただし、外部のサードパーティのコードとのインターフェースに必要な場合にのみ使用してよいこととします。

```typescript
//間違い：名前空間を使用しない
namespace Rocket {
    function launch() { ... }
}
  
//間違い：<reference>を使用しない
/// <reference path="..."/>
  
//間違い：require()を使用しない
import x = require('mydep');
```

注意：TypeScriptの名前空間は、かつては内部モジュールと呼ばれ、`module Foo { ....}`の形で`module`キーワードが使われていました。 これも使ってはいけません。常にES6の`import`文を使用してください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### export文

すべてのコードで名前付きエクスポートを使用します。

```javascript
// 正しい：
export class Foo { ... }
```

- 【必須】使用するフレームワークが使用を許可している場合を除き、`default exports`は使用してはいけません。

```javascript
// 間違い：
export default class Foo { ... }
```

`default export`は正規の名前が提供されていないため、コードの所有者にとっては可読性の低下などの比較的少ないメリットしかなく、管理が難しくなるためです。

```javascript
// 間違い：どちらも正しいため、管理が難しくなります
import Foo from './bar';
import Bar from './bar';
```

これは`named export`で解決できます。`named export`は`import`文が宣言されていないものをインポートしようとするとエラーになるメリットがあります。

たとえばfoo.tsでは

```javascript
// export defaultの使用
const foo = 'blah';
export default foo;
```

そしてbar.tsでは

```javascript
import { fizz } from './foo';
```

結果として、TS2614のエラー`Module '"./foo"' has no exported member 'fizz'`が発生します。

一方、bar.tsを次に変更すると

```javascript
import fizz from './foo';
```

fizz === fooという結果になりますが、これはおそらく予想外のことで、デバッグが困難です。

さらに、デフォルトのエクスポートでは、すべてのものを1つの大きなオブジェクトにまとめて名前空間にすることが推奨されています。

```typescript
// TypeScriptの例
export default class Foo {
  static SOME_CONSTANT = ...
  static someHelpfulFunction() { ... }
  ...
}
```

上記のパターンでは、名前空間として使用できるファイルスコープがあります。また、おそらく不要な第2のスコープ（Fooクラス）があり、他のファイルで型や値としても使用できてしまいます。

代わりに、名前付きのエクスポートと同様に、名前付きのファイルスコープの使用をお勧めします。

```typescript
export const SOME_CONSTANT = ...
 
export function someHelpfulFunction()
 
export class Foo {
  // ここにはクラスのものだけ
}
```

例外：使用するフレームワークで使用を許可している場合は、`default exports`は使用してよいものとします。

```typescript
// 例外：Vue.jsのexport defaultの使用
import { Vue, Component, Prop } from "vue-property-decorator";
import Item from "@/assets/js/store/Item";
 
@Component
export default class ItemList extends Vue {
    @Prop() item!: Item;
 
    get thumbnail(): string {
        return require(`@/assets/${this.item.thumbUrl}`);
    }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### コンテナクラス

- 【必須】名前空間のために、静的メソッドまたはプロパティを使用してコンテナクラスを作成すべきではありません。

代わりに、個々の定数と関数をエクスポートします。

``` javascript
// 間違い：
export class Container {
  static FOO = 1;
  static bar() { return 1; }
}
 
// 正しい：
export const FOO = 1;
export function bar() { return 1; }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### import文

ES6とTypeScriptの`import`文は、4つのバリエーションがあります。

タイプ | 例 | 使用 
------------- | ------------- | ------------
モジュール  | `import * as foo from '...';` |
分割  | `import {SomeThing} from '...';` |
デフォルト  | `import SomeThing from '...';` | 必要な他の外部コードの場合のみ
副作用  | `import '...';` | ロード時の副作用（カスタム要素など）のためだけにインポート

```javascript
import * as ng from '@angular/core';
import { Foo } from './foo';

import Button from 'Button';

import 'jasmine';
import '@polymer/paper-button';
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

##### インポート名の変更

- 【推奨】モジュールのインポートを使用するか、エクスポート自体の名前を変更することで、名前の衝突回避を推奨します。

名称変更が有効な3つの例：

1. 他のインポートされたシンボルとの衝突を回避する必要がある場合。
2. インポートされたシンボル名が生成された場合。
3. 名前が不明確なシンボルをインポートする場合、名前の変更でコードの明確さが期待できる場合（たとえば『[RxJS](https://rxjs.dev/)』の場合、`from`メソッドは`observableFrom`に名前を変更すると可読性が向上します）。

```typescript
// 推奨：
import { Foo as SomeOtherThing } from './foo';
import { from as observableFrom } from 'rxjs';
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 機能別の整理

- 【推奨】パッケージはタイプ別ではなく、機能別の整理を推奨します。たとえばオンラインショップの場合、ビュー、モデル、コントローラではなく、プロダクト、チェックアウト、バックエンドというパッケージの用意を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### コードのフォーマット

#### インデント

- 【必須】TypeScript/JavaScriptのインデントは、半角スペース4つとしなければなりません。

```typescript
// 正しい：
const hoge = {
    width: 100,
    height: '300px',
}
 
export default class AlphaTimewarp implements Timewarp {
    private readonly STORAGE_KEY = 'alpha_datetime';
 
    constructor(private storage: Storage) {}
     
    setDatetime(datetime: string): void {
        const unixtime = this.datetimeToUnixtime(datetime);
        this.storage.setItem(this.STORAGE_KEY, unixtime);
    }
 
    getDatetime(): string {
        const unixtime = this.getUnixtime();
        return this.unixtimeToDatetime(unixtime);
    }
}
```

- 【必須】初期化リストの中で長い識別子や値の位置は揃えてはいけません。

```javascript
// 間違い：
const sample1 = {
  a          : 0,
  b          : 1,
  lengthyName: 2
};
 
// 正しい：
const sample2 = {
    a: 0,
    b: 1,
    lengthyName: 2
};
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 空白

- 【必須】行末に空白を指定してはいけません。
- 【必須】演算子の前後には半角スペース1つで離さなければなりません。
- 【必須】カンマ`,`は行末を除き、後ろに半角スペース1つで離さなければなりません。
- 【必須】セミコロン`;`は行末を除き、後ろに半角スペース1つで離さなければなりません。

```javascript
// 正しい：
const j = k + 3;
const list = [1, 2, 3, 4];
for (let i = 0; i < 10; i++) { … }
```

- 【必須】文が1行の場合、波括弧`{}`の前後は行末を除き半角スペース1つで離さなければなりません。

```javascript
// 正しい：
if (ns < 10) { ns = `0${ns}`; }
const object = { foo: 'bar'; }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 改行

- 【推奨】原則として、カンマ`,`、セミコロン`;`、波括弧`{}`の後、関数ブロックの終わりに改行の指定を推奨します。

```javascript
const app = new Vue({
    components: {
        Header,
        Footer,
    },
    created() {
        imgPreloading();
    },
    mounted() {
        htmlScale();
    }
});
```

可読性が向上する場合、改行の省略はしてよいものとします。おもに関数内にメソッドが1つの場合や、カンマ`,`で改行すると可読性が落ちる場合、これに該当します。

```javascript
const arr = [1, 2, 3]; 
const obj = {a: 1, b: 2, c: 3}; 
const x = a ? b : c; 

const hoge = (arg) => { return { name: value }; }

if (ns < 10) { ns = `0${ns}`; }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 空行

- 【推奨】可読性向上のため、コンテキスト（論理的に関連する部分）でグループになりそうな箇所は空行の使用を推奨します。

```javascript
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);
 
nowDoSomethingWith(y);
 
andNowWith(z);
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 1行の文字数

- 【必須】可読性向上のため、1行の文字数は120文字以内におさめなくてはなりません 。

注意：全角文字は2文字でカウントします。

```javascript
// 半角スペース4つでインデントし、120文字で折り返します
// 関数名が変わった場合、インデントを修正する必要がなく、場所もあまりとりません
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function( 
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo, 
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) { 
    ... 
};

// 関数名が長い場合：
// 半角スペース4つでインデントし、各行に1つずつ引数を書きます
// 関数名の変更の影響を受けず、また個々の引数を目立たせることができます
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function( 
    veryDescriptiveArgumentNumberOne, 
    veryDescriptiveArgumentTwo, 
    tableModelEventHandlerProxy, 
    artichokeDescriptorAdapterIterator) { 
    ... 
};

// 丸括弧に揃えてインデントし、120文字で折り返します
// 視覚的に引数をグループ化でき、 かつスペースも少なくてすみます
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo, 
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) { 
    ... 
}

// 丸括弧に揃えてインデントし、各行に1つずつ引数を書きます
// 個々の引数を目立たせることができます
function bar(veryDescriptiveArgumentNumberOne, 
             veryDescriptiveArgumentTwo, 
             tableModelEventHandlerProxy, 
             artichokeDescriptorAdapterIterator) { 
    ... 
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### セミコロン`;`

- 【必須】文と宣言は、セミコロン`;`で終了しなくてはなりません。

『[自動セミコロン挿入（Automatic Semicolon Insertion）](https://tc39.es/ecma262/#sec-rules-of-automatic-semicolon-insertion)』に依存しないでください。状況によってはエラーの原因になります。セミコロン`;`を使用して、すべての文を明示的に終了します。


``` javascript
// 間違い：
const text1 = 'a'
const text2 = 'b'
const text3 = 'c' // Error: Uncaught TypeError: "c" is not a function
 
(() => {
    console.log(text1, text2, text3)
})()
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 波括弧`{}`

- 【必須】波括弧`{}`はセミコロンの暗黙の挿入を考慮し、波括弧が開く箇所と同じ行から始めなくてはなりません。

```javascript
if (something) {
    ...
} else {
    ...
}
```

1行に収まる`if`文の場合は、波括弧`{}`を省略可能です。

```javascript
// 例外：波括弧`{}`の省略
if (x) x.doFoo();
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 二項または三項の演算子

- 【必須】演算子は先頭の行で指定しなくてはなりません。ドット演算子も同様です。

```typescript
// 正しい：
const x = a ? b : c; 

const y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

const x = foo.bar().
    doSomething().
    doSomethingElse();

// 間違い：
const x = a 
    ? b : c;

const x = foo
    .bar().
    doSomething().
    doSomethingElse();
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### クォート

- 【必須】一貫性の面でダブルクォート`"`よりもシングルクォート`'`の方が好ましいといえるため、ダブルクォート`"`ではなく、シングルクォート`'`の使用しなければなりません。
- 【推奨】文字列が複数行にわたる場合や、式を含む場合、バッククォート`` ` ``の使用を推奨します。

普通の文字列はシングルクォート`'`を使用します。

```javascript
let message = 'This is some HTML';
```

複数行にわたる場合や式を含む場合、バッククォート`` ` ``を使用します。

```javascript
// テンプレートリテラル
let greeting = `${name.toUpperCase()}さんこんにちは`; 
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>