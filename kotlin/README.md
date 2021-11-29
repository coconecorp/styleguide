# Kotlinスタイルガイド

<details><summary>目次</summary>

- [はじめに](#はじめに)
- [ソースファイル](#ソースファイル)
  - [命名](#命名)
  - [特殊文字](#特殊文字)
    - [空白文字](#空白文字)
    - [特殊なエスケープシーケンス](#特殊なエスケープシーケンス)
    - [非ASCII文字](#非ascii文字)
  - [構造](#構造)
    - [著作権またはライセンス](#著作権またはライセンス)
    - [ファイルレベルのアノテーション](#ファイルレベルのアノテーション)
    - [package文](#package文)
    - [import文](#import文)
    - [トップレベル宣言](#トップレベル宣言)
    - [クラスメンバーの順序](#クラスメンバーの順序)
- [形式](#形式)
  - [波括弧`{}`](#波括弧)
    - [空でないブロック](#空でないブロック)
    - [空のブロック](#空のブロック)
    - [式](#式)
    - [インデント](#インデント)
    - [1行に1つずつ](#1行に1つずつ)
    - [1行の文字数](#1行の文字数)
    - [行の折り返し](#行の折り返し)
    - [関数](#関数)
    - [プロパティ](#プロパティ)
  - [空白](#空白)
    - [垂直方向](#垂直方向)
    - [水平方向](#水平方向)
  - [特定の構造](#特定の構造)
    - [enumクラス](#enumクラス)
    - [アノテーション](#アノテーション)
    - [暗黙の戻り値/プロパティ型](#暗黙の戻り値プロパティ型)
  - [命名](#命名-1)
    - [パッケージ名](#パッケージ名)
    - [型名](#型名)
    - [関数名](#関数名)
    - [定数名](#定数名)
    - [非定数名](#非定数名)
    - [型変数名](#型変数名)
    - [Camel形式](#camel形式)
  - [ドキュメント](#ドキュメント)
    - [書式](#書式)
    - [ブロックタグ](#ブロックタグ)
    - [記述場所](#記述場所)

</details>

## はじめに

- 本ガイドラインは、[ココネ株式会社](https://www.cocone.co.jp/)のKotlinのスタイル基準を示すものです。
- 本ガイドラインは、『[Android デベロッパー Kotlin スタイルガイド](https://developer.android.com/kotlin/style-guide)』を参考に規定しています。
- 本ガイドラインで未定義のスタイルや、詳細を定義していない箇所の議論となった場合は、『[Android デベロッパー Kotlin スタイルガイド](https://developer.android.com/kotlin/style-guide)』を参考に検討することとします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## ソースファイル

- 【必須】ファイルのエンコーディングは、UTF-8でなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 命名

- 【必須】トップレベルクラスが1つしか含まれていない場合、ファイル名は大文字のCamel形式（"UpperCamelCase"）で命名し、拡張子`.kt`を付けなければなりません。
- 【必須】複数のトップレベルクラスが含まれている場合、ファイルの内容が分かる名前を大文字のCamel形式（"UpperCamelCase"）で命名し、拡張子`.kt`を付けなければなりません。

```kotlin
// MyClass.kt
class MyClass { }
```

```kotlin
// Bar.kt
class Bar { }
fun Runnable.toBar(): Bar = // …
```

```kotlin
// Map.kt
fun <T, O> Set<T>.map(func: (T) -> O): List<O> = // …
fun <T, O> List<T>.map(func: (T) -> O): List<O> = // …
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 特殊文字

#### 空白文字

- 【必須】改行以外の空白文字は、`ASCII水平スペース文字（0×20）`しか使用してはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 特殊なエスケープシーケンス

- 【推奨】特別なエスケープシーケンスをもつすべての文字（`\b` `\t` `\n` `\f` `\r` `\"` `\'` `\\`）は、8進数表記（`\012`）やUnicodeエスケープ（`\u000a`）でなく、通常のエスケープシーケンスの使用を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 非ASCII文字

非ASCII文字は、Unicode文字（例：`∞`）またはUnicodeエスケープ文字（例：`\u221e`）の両方を使用できます。コードの可読性を考慮して選択します。

- 【必須】Unicodeエスケープ文字は、印刷用文字に使用してはいけません。また、文字列リテラルおよびコメント以外では使用してはいけません。

| 例  | 考察 |
|:------------- |:---------------|
| val unitAbbrev = "μs" | 最適: コメントなしでも完全に明快にわかります |
| val unitAbbrev = "\u03bcs" // μs | 要改善: 印刷用文字にエスケープを使用する理由がありません |
| val unitAbbrev = "\u03bcs" | 要改善: これが何なのか、読者にはわかりません |
| return "\ufeff" + content | 良好: 印刷用以外の文字にエスケープを使用し、必要に応じてコメントを使用します |

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 構造

- 【必須】ソースファイルの内容は、次の順序でなければなりません。

1. 著作権またはライセンスヘッダ（オプション）
2. ファイルレベルのアノテーション
3. package文
4. import文
5. トップレベル宣言

- 【必須】ソースファイルの内容を分離する場合、複数ではなく1行の空行を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 著作権またはライセンス

- 【推奨】著作権ヘッダやライセンスヘッダは、複数行コメントのすぐ上での記述を推奨します。

```kotlin
/*
 * © cocone corporation. All rights reserved. 
 *
 * ...
 */
```

- 『[KDoc](https://kotlinlang.org/docs/reference/kotlin-doc.html)』や単一行スタイルのコメントは、使用してよいこととします。

KDoc規定は、[ドキュメント](#ドキュメント)の章をご覧ください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### ファイルレベルのアノテーション

- 【必須】『[use-site target](https://kotlinlang.org/docs/reference/annotations.html#annotation-use-site-targets)』を伴うアノテーションは、ヘッダーコメントとパッケージ宣言の間に配置しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### package文

- 【必須】package文は改行してはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### import文

- 【必須】ワイルドカードインポートは、`static`に関係なく使用してはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### トップレベル宣言

- 【推奨】ファイルの内容は1つのテーマに関する内容であることを推奨します。
- 【必須】それぞれのクラスはそのメンバーを説明がつく合理的な順序で並べ、クラスの運用担当者は、順番の理由を答えられるようにしなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### クラスメンバーの順序

- 【推奨】クラス内のメンバーの順序は、トップレベルの宣言と同じ規則で並べることを推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 形式

### 波括弧`{}`

他に`else if`や`if`分岐がなく、1行におさまる`when`分岐や`if`文の中身には、波括弧`{}`を省略してよいものとします。

```kotlin
if (string.isEmpty()) return

when (value) {
    0 -> return
    // …
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 空でないブロック

- 【必須】波括弧`{}`は空でないブロックや、ブロックの構造物ではK&Rスタイル『[エジプト人ブレース](http://www.codinghorror.com/blog/2012/07/new-programming-jargon.html)』に従わなければなりません。

つまり、

- 開始波括弧`{`の前に改行を入れてはいけません。
- 開始波括弧`{`の後に改行を入れなければなりません。
- 終了波括弧`}`の前に改行を入れなければなりません。
- 終了波括弧`}`の後に改行を入れなければなりません。これは文やメソッドの本体を終える場合になります。たとえば、終了波括弧`}`の後に`else`や、カンマ`,`が続く場合は改行しません。

```kotlin
return Runnable {
    while (condition()) {
        foo()
    }
}

return object : MyClass() {
    override fun foo() {
        if (condition()) {
            try {
                something()
            } catch (e: ProblemException) {
                recover()
            }
        } else if (otherCondition()) {
            somethingElse()
        } else {
            lastThing()
        }
    }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 空のブロック

- 【必須】空のブロックは、空ではないブロック同様、K&Rスタイル『[エジプト人ブレース](http://www.codinghorror.com/blog/2012/07/new-programming-jargon.html)』に従わなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 式

- 【推奨】`if/else`で式全体が1行におさまる場合、波括弧`{}`の省略を推奨します。

```kotlin
val value = if (string.isEmpty()) 0 else 1

val value = if (string.isEmpty()) {
    0
} else {
    1
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### インデント

- 【必須】Javaのインデントは、半角スペース**4**つとしなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 1行に1つずつ

- 【推奨】それぞれの文の後には改行を続け、セミコロンの省略を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 1行の文字数

- 【必須】コードの1行の文字数制限は**200文字**とし、制限を超えた行は改行しなければなりません。

例外：

- KDoc内の長いURLなど、文字数制限に従うのが不可能の場合
- package文やimport文
- コメント内に記載しているコマンド

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 行の折り返し

- 【必須】メソッド名やコンストラクタ名と、直後の開始丸括弧`(`の間は、改行してはいけません。
- 【必須】次の演算子に似た記号の箇所で改行する場合、シンボルの前で改行しなければなりません。
    - ドット区切り（`.`、`?.`）
    - メソッド参照で使用する2つのコロン`::`
- 【必須】カンマ`,`は、その前のトークンの直後に続いて書かなくてはなりません。改行してはいけません。
- 【必須】ラムダ式の矢印`->`の直後で改行してはいけません。
- 【推奨】演算子または`infix`関数名の箇所で改行する場合、改行は演算子または`infix`関数名の後に入れることを推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 関数

- 【推奨】関数シグネチャが1行におさまらない場合は、各引数宣言をそれぞれ1行に分割することを推奨します。
- 【推奨】関数シグネチャを分割する場合は、それぞれの引数は半角スペース4つのインデントを推奨します。終了丸括弧`)`と戻り値の型はインデントを増やさず、それぞれ別の行に配置します。

```kotlin
// 推奨
fun <T> Iterable<T>.joinToString(
    separator: CharSequence = ", ",
    prefix: CharSequence = "",
    postfix: CharSequence = ""
): String {
    // …
}
```

- 【推奨】関数に1つの式しか含まれていない場合は、[単一式関数](https://kotlinlang.org/docs/reference/functions.html#single-expression-functions)として書くことを推奨します。

```kotlin
// 推奨：
override fun toString(): String = "Hey"

// 非推奨：
override fun toString(): String {
    return "Hey"
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### プロパティ

- 【推奨】プロパティ初期化子が1行におさまらない場合は、等号`=`の後で改行し、インデントを推奨します。

```kotlin
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

- 【必須】関数`get`/`set`を宣言するプロパティは、半角スペース4つのインデントをつけて、それぞれを別々の行への配置しなければなりません。

```kotlin
var directory: File? = null
    set(value) {
        // …
    }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 空白

#### 垂直方向

- 【推奨】次の場合は、空白行を1行置くことを推奨します。

- プロパティ、コンストラクタ、関数、子クラスなどのクラス内の連続するメンバー間。
- 必要に応じて文を論理的なサブセクションに分割するため。
- 必要に応じて関数の最初の文の前、クラスの最初のメンバーの前、クラスの最後のメンバーの後（推奨ではありません）。
- この文書の他のセクション（構造に関するセクションなど）の内容に応じて。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 水平方向

- 【必須】予約語`if` `for` `catch`と、その行の開始丸括弧`(`の間は、半角スペース1つで離さなければなりません。
- 【必須】予約語 `else` `catch`と、その行の前の終了波括弧`}`の間は、半角スペース1つで離さなければなりません。
- 【必須】開始波括弧`{`の前は、半角スペース1つで離さなければなりません。
- 【必須】二項演算子や三項演算子の両側は、半角スペース1つで離さなければなりません。 
- 【必須】メソッド参照でのコロン2つ`::`の前後は、半角スペースを入れてはいけません。
- 【必須】ドット区切り文字`.`の前後は、半角スペースを入れてはいけません。
- 【必須】カンマ`,`、コロン`:`、セミコロン`;`、あるいはキャストの終了丸括弧`)`の直後は、半角スペース1つで離さなければなりません。
- 【必須】コロン`:`の前は、基本クラスまたは基本インターフェースを指定するためのクラス宣言、またはジェネリクスの`where`句内で一般的な制約使用されている場合に限り、半角スペース1つで離さなければなりません。
- 【必須】行末コメントの開始スラッシュ`//`の前後は、半角スペース1つで離さなければなりません。
- 【必須】型アノテーションと `[]` または `...` の間は、半角スペース1つで離さなければなりません。
  

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 特定の構造

#### enumクラス

enum内の定数が別々の行に配置されている場合、それらが本体を定義する場合を除いて、空白行の使用はどちらでもかまいません。

```kotlin
enum class Answer {
    YES,
    NO,
}

enum class Answer {
    YES, NO,
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### アノテーション

- 【必須】引数のないアノテーションは、単一行に配置しなければなりません。

```kotlin
@JvmField @Volatile
var disposable: Disposable? = null
```

- 【推奨】`@[...]`構文は、[use-site target](https://kotlinlang.org/docs/annotations.html#annotation-use-site-targets)を明示的に指定する場合のみ使用することを推奨します。
- 【推奨】`@[...]`構文は、1行に引数のない2つ以上のアノテーションを組み合わせる場合にのみ使用することを推奨します。

```kotlin
@field:[JvmStatic Volatile]
var disposable: Disposable? = null
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 暗黙の戻り値/プロパティ型

- 【推奨】式関数本文、またはプロパティイニシャライザがスカラである場合、値または戻り値の型は本文から明確に推定できるので、省略を推奨します。

```kotlin
// 推奨：
override fun toString() = "Hey"

// 非推奨：
override fun toString(): String = "Hey"
```

- 【推奨】ライブラリを作成するとき、それがパブリックAPIの一部である場合は型の明示的な指定を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 命名

- 【必須】原則として、識別子の名前は正規表現`\w+`にマッチした文字（ASCII文字、数字）を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### パッケージ名

- 【必須】パッケージ名は、すべて小文字で連続する単語はアンダースコア`_`なしで連結しなければなりません。

```kotlin
// 正しい：
package com.example.deepspace

// 間違い：
package com.example.deepSpace
package com.example.deep_space
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 型名

- 【必須】クラス名は、大文字のCamel形式（"UpperCamelCase"）で命名しなければなりません。
- 【必須】テストのクラス名は、テスト対象クラスの名前で始め、`Test`で終わるように命名しなければなりません（例：`HashTest` `HashIntegrationTest`）。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 関数名

- 【必須】関数名は、小文字のCamel形式（"lowerCamelCase"）で命名しなければなりません。

例外：アンダースコア`_`は、テストの関数名で名前の論理的コンポーネント名（"lowerCamelCase"）を分離する目的で使用できます。

-  `Unit`を返す`@Composable`アノテーション付きの関数名は、大文字のCamel形式（"UpperCamelCase"）で、名前と型を繋げることをお勧めします。

```kotlin
@Composable
fun NameTag(name: String) {
    // …
}
```

- 【必須】関数名にスペース含めてはいけません。環境によってはサポートされていません（特に、Androidでは完全にはサポートされていません）。

```kotlin
// 正しい：
fun testEveryPossibleCase() {}

// 間違い：
fun `test every possible case`() {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 定数名

- 【必須】定数名は、コンスタントケース（`CONSTANT_CASE`）で命名しなければなりません。すべて大文字で、各単語を1つのアンダースコアで繋げなければなりません。

```kotlin
val EMPTY_ARRAY = arrayOf()
```

- 【推奨】定数名は、`object`の内部またはトップレベルの宣言としてのみ定義することを推奨します。それ以外の場合は定数の要件を満たしていても、定数の名前は使用しません。
- 【推奨】スカラ値である定数は`const`[修飾子](https://developer.android.com/kotlin/style-guide#:~:text=%E3%81%AB%E3%81%AF%20const-,%E4%BF%AE%E9%A3%BE%E5%AD%90,-%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B)修飾子の使用を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 非定数名

- 【必須】非定数名は、小文字のCamel形式（"lowerCamelCase"）で命名しなければなりません。

インスタンスプロパティ、ローカルプロパティ、パラメータ名も同様です。

```kotlin
val variable = "var"
val nonConstScalar = "non-const"
val mutableCollection: MutableSet = HashSet()
val mutableElements = listOf(mutableInstance)
val mutableValues = mapOf("Alice" to mutableInstance, "Bob" to mutableInstance2)
val logger = Logger.getLogger(MyClass::class.java.name)
val nonEmptyArray = arrayOf("these", "can", "change")
```

- 【推奨】[バッキング プロパティ](https://kotlinlang.org/docs/reference/properties.html#backing-properties)を使用する場合は、その名前はアンダースコア`_`で始まる場合を除き、実際のプロパティ名と一致させることを推奨します。

```kotlin
private var _table: Map? = null

val table: Map
    get() {
        if (_table == null) {
            _table = HashMap()
        }
        return _table ?: throw AssertionError()
    }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 型変数名

- 【必須】型変数名は次のうちいずれかで命名しなければなりません。
  - 1つの大文字アルファベットの後に、1つの数字を続ける（例： `E` `T` `X` `T2`）。
  - クラスの命名規定の後に、大文字`T`を続ける（例： `RequestT` `FooBarT`）。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### Camel形式

<!-- 頭字語や「IPv6」「iOS」など、英語のフレーズをCamel形式に変換する方法が複数存在します。 -->

- 【推奨】予測可能性を向上させるため、次の命名方法を推奨します。

1. 単語をASCIIに変換し、アポストロフィを削除します（例：「[Müller's algorithm](https://en.wikipedia.org/wiki/Muller%27s_method)」は「Muellers algorithm」）。
2. 単語に分割し、スペースやその他の句読点（通常はハイフン）で分けます。<br>
推奨：従来のCamel形式の単語がある場合は、同様に分割します（例：「AdWords」は「ad words」）。<br>
注意：たとえば「iOS」は、本当の意味でのCamel形式ではなく、どの規則にもしたがっていないため、分割はしません。
1. 頭字語を含む、すべての文字を小文字にしてから、次のいずれかを実行します。
    - 大文字のCamel形式（"UpperCamelCase"）にする場合は、各単語の最初の文字を大文字にします。
    - 小文字のCamel形式（"lowerCamelCase"）にする場合は、最初の単語を除き、各単語の最初の文字を大文字にします。
2. 最後に、すべての単語を連結して1つの識別子にします。

| 簡潔な形式  | 正しい | 間違い |
|:------------- |:---------------|:---------------|
|「XML Http Request」（XML HTTP リクエスト）|XmlHttpRequest|XMLHTTPRequest|
|「new customer ID」（新規お客様 ID）|newCustomerId|newCustomerID|
|「inner stopwatch」（内側のストップウォッチ）|innerStopwatch|innerStopWatch|
|「supports IPv6 on iOS」（iOS で IPv6 をサポート）|supportsIpv6OnIos|supportsIPv6OnIOS|
|「YouTube importer」（YouTube インポート ツール）|YouTubeImporter	YoutubeImporter*|

単語の中には、曖昧なハイフンで連結している場合があります。たとえば、「nonempty」と「non-empty」はどちらも正しい英語です。なのでメソッド名は`checkNonempty`と`checkNonEmpty`のどちらも正しいことになります。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### ドキュメント

#### 書式

KDocブロックの基本的な書式は、次のようになります。

```kotlin
/**
 * Multiple lines of KDoc text are written here,
 * wrapped normally…
 */
fun method(arg: String) {
    // …
}
```

または次のように、1行でも書くことができます。

```kotlin
/** An especially short bit of KDoc. */
```

参考：『[Document Kotlin code: KDoc and Dokka](https://kotlinlang.org/docs/kotlin-doc.html)』

- 【推奨】KDocブロック全体（コメントマーカーを含む）が1行におさまる場合は、単一行形式に置き換えることを推奨します。

なお、単一行形式は`@return`のようなブロックタグがない場合にのみ使えることに注意してください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### ブロックタグ

- 【必須】ブロックタグは、`@constructor` `@receiver` `@param` `@property` `@return` `@throws` `@see`の順番で使用しなければなりません。
- 【必須】ブロックタグが1行のコメントに収まらない場合、2行目以降は`@`の位置から半角スペース4つ以上でインデントしなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 記述場所

- KDocは、`public`なクラスとそのクラスの`public protected`なメンバーに対し書くことをお勧めします。

例外：

- `getFoo`のような「fooを返す」以外の情報が無く、簡単で明確なメソッドの場合、記述は不要です。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>
