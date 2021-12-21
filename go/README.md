# Goスタイルガイド

<details><summary>目次</summary>

- [はじめに](#はじめに)
- [Linter](#linter)
- [コードの整形](#コードの整形)
- [コンテキスト](#コンテキスト)
- [構造体のコピー](#構造体のコピー)
- [乱数生成](#乱数生成)
- [空のスライス](#空のスライス)
- [docコメント](#docコメント)
- [使い方のサンプル](#使い方のサンプル)
- [goroutine](#goroutine)
- [エラーハンドリング](#エラーハンドリング)
- [import文](#import文)
- [ブランクを使用したインポート](#ブランクを使用したインポート)
- [ドットを使用したインポート](#ドットを使用したインポート)
- [インバインドエラー](#インバインドエラー)
- [エラーハンドリングの分岐](#エラーハンドリングの分岐)
- [頭字語](#頭字語)
- [インターフェース](#インターフェース)
- [行の長さ](#行の長さ)
- [名前付き戻り値](#名前付き戻り値)
- [パッケージのコメント](#パッケージのコメント)
- [パッケージ名](#パッケージ名)
- [ポインタ](#ポインタ)
- [レシーバ名](#レシーバ名)
- [レシーバの型](#レシーバの型)
- [テストの失敗例](#テストの失敗例)
- [変数名](#変数名)
- [関数名](#関数名)

</details>

## はじめに

- 本ガイドラインは、[ココネ株式会社](https://www.cocone.co.jp/)のGoのスタイル基準を示すものです。
- 本ガイドラインは、『[Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)』を参考に規定しています。
- 本ガイドラインで未定義のスタイルや、詳細を定義していない箇所の議論となった場合は、『[Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)』を参考に検討することとします。

## Linter

- 【必須】必ず、Linterの『[Staticchek](https://staticcheck.io/)』を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## コードの整形

- 【必須】コードの整形には、[`gofmt`](https://golang.org/cmd/gofmt/)コマンド（goコマンドのfmtオプション）を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## コンテキスト

- 【必須】原則として、関数では`Context`は最初のパラメータとして渡さなければなりません。

```go
func F(ctx context.Context, /* other arguments */) {}
```

- 【必須】原則として、`Context`を構造体のメンバーに含めてはいけません。かわりに、すべてのメソッドに引数として渡してください。 

例外：ライブラリのシグネチャと一致させなければならない場合は除きます。

- 【推奨】カスタムのコンテキスト型を作成や、関数の引数に取ったコンテキスト以外のインターフェースの使用は推奨しません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 構造体のコピー

- 【必須】別のパッケージから構造体をコピー場合、メソッドがポインタの値に関連付けられているなら、`T`ではなく`*T`を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 乱数生成

- 【必須】`math/rand`は、たとえ使い捨てのものであっても鍵の生成のために使用してはいけません。
- 【必須】`math/rand`のかわりに`crypto/rand`のReaderを使用しなければなりません。それを文字として取得したい場合は、16進数かbase64にエンコードしなければなりません。

```go
import (
	"crypto/rand"
	// "encoding/base64"
	// "encoding/hex"
	"fmt"
)

func Key() string {
	buf := make([]byte, 16)
	_, err := rand.Read(buf)
	if err != nil {
		panic(err)  // out of randomness, should never happen
	}
	return fmt.Sprintf("%x", buf)
	// or hex.EncodeToString(buf)
	// or base64.StdEncoding.EncodeToString(buf)
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 空のスライス

- 【必須】空のスライスを宣言する場合、`t := []string{}`よりも`var t []string`を使用しなければなりません。

`var t []string`はnilのスライスを生成します。しかし、`t := []string{}`は長さ0のスライスを宣言します。

- 【必須】インターフェースを設計する場合、nilのスライスと長さ0のスライスを区別しないようにしなければなりません。

区別してしまうと、分かりづらいミスを引き起こす場合があります。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## docコメント

- 【必須】すべてトップレベルや、外部に公開されているものは、docコメントがなければなりません。
- 【必須】外部に公開されていない重要な関数やtype宣言は、docコメントがなければなりません。

docコメントの詳細は、『[Effective Go - Commentary](https://go.dev/doc/effective_go#commentary)』をご覧ください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 使い方のサンプル

- 【推奨】新しいパッケージを追加した場合、使い方のサンプルを含めることを推奨します。

実行可能な例や、一連の流れを追えるテストなどがサンプルに該当します。

サンプルの詳細は、『[Testable Examples in Go - The Go Blog](https://go.dev/blog/examples)』をご覧ください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## goroutine

- 【必須】`goroutine`を生成する場合、終了を明確にしなければなりません。
- 【必須】並行処理は`goroutine`の生存期間が明確になるように、シンプルに書かなければなりません。
- 【必須】`goroutine`がシンプルに書けない場合、いつどんな理由で`goroutine` が終了するかをドキュメントに明示しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## エラーハンドリング

- 【必須】`_`でエラーを無視してはいけません。 

関数がエラーを返してきた場合、関数が成功したか確認してください。 エラーをハンドリングして返します（例外的な場合に限り、`panic`を使用します）。

エラーの詳細は、『[Errors - Effective Go](https://go.dev/doc/effective_go#errors)』をご覧ください。


<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## import文

- 【必須】原則として、名前の衝突を回避する目的で、package名は変更してはいけません。
- 【必須】名前が衝突した場合、package名はローカルやプロジェクト固有の名称に変更しなければなりません。
- import文はグループ化し、それぞれ空行で分離します（標準パッケージは最初のグループにします）。

[`goimports`](https://godoc.org/golang.org/x/tools/cmd/goimports)を使用すると、自動でグループ化します。

```go
package main

import (
	"fmt"
	"hash/adler32"
	"os"

	"appengine/foo"
	"appengine/user"

	"github.com/foo/bar"
	"rsc.io/goversion/version"
)
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## ブランクを使用したインポート

- 【必須】`import _ "pkg"`を使用し、パッケージをインポートした場合の副作用だけを使用する方法がありますが、この方法はプログラムのメインパッケージ、もしくはテスト以外は使用してはいけません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## ドットを使用したインポート

- 【必須】原則として、`import .`は使用してはいけません。

Quuxのような名前は、今のパッケージの識別子なのかインポートされたものなのかが非常にわかりにくく、可読性が極端に落ちるからです。

例外：

`.`を使用したインポートは、循環参照によってパッケージの一部がテストできない場合などで役立ちます。次の場合、テストファイルはfooをインポートしている`bar/testutil`を使用し、循環参照になるため、package fooに置くことができません。 なので`import .`を使用し、package fooの一部のように見せかけます。

```go
package foo_test

import (
	"bar/testutil" // also imports "foo"
	. "foo"
)
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## インバインドエラー

- 【必須】関数が、他の値が正しく取得できたか示す値を追加して返す場合、その値は戻り値の中で最後に位置していなくてはなりません。
- 【推奨】関数は、クライアントに戻り値がエラーを表現しているか調べることを求めるのではなく、他の値が正しく取得できたか示す値を追加して返すことを推奨します。この値はError型の場合がありますし、説明不要な場合はbool値でもかまいません。

```go
func Lookup(key string) (value string, ok bool)
```

この方法で、呼び出し側に正しくない値が渡るのを制限できます。

```go
Parse(Lookup(key))  // compile-time error
```

そして堅牢で、読みやすいコードを書きやすくなります。

```go
value, ok := Lookup(key)
if !ok {
	return fmt.Errorf("no value for %q", key)
}
return Parse(value)
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## エラーハンドリングの分岐

- 【必須】エラーハンドリングの分岐は、最小にしなければなりません。

分岐を最小にすると、コードを簡単に追うことができるため、可読性の向上が期待できます。

```go
// 非推奨：
if err != nil {
	// error handling
} else {
	// normal code
}

// 推奨：
if err != nil {
	// error handling
	return // or continue, etc.
}
// normal code
```

- 初期化のコードについて、変数宣言は個別の行で宣言します。

```go
x, err := f()
if err != nil {
	// error handling
	return
}
// use x
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 頭字語

- 【必須】変数名の頭字語は、プロジェクトで一貫性を持たせなければなりません。

例：

- 「URL」は「URL」か「url」であり、「Url」ではありません。「ServeHttp」ではなく、「ServeHTTP」となります。 複数の頭字語から構成される名前は、「xmlHTTPRequest」や「XMLHTTPRequest」とします。
- 「identifier」の省略である「ID」も同様で、「appId」ではなく「appID」とします。
- 非公開の定数は、「MaxLength」や「MAX_LENGTH」ではなく「maxLength」とします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## インターフェース

- 【必須】モックのために、APIの実装側にインターフェースを定義してはいけません。

かわりに、実際に実装された公開APIからテストできるAPIを設計します。

- 【必須】使用前にインターフェースを定義してはいけません。

現実的な使い方のサンプルがなければ、メソッドや、そのインターフェースが必要かどうかわかりません。

- 【推奨】パッケージを実装する場合、（ポインタや構造体のような）具体的な型を返すことを推奨します。

この方法で、使用する側は修正なしで新しいメソッドを追加できます。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 行の長さ

- 【推奨】1行の長さについて、特に制限はありませんが、長過ぎは推奨しません。

行の長さで改行するのではなく、行の意味で改行しましょう。長過ぎる行を見つけた場合は、名前や処理の流れの改善をしましょう。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 名前付き戻り値

-【必須】名前付き戻り値はGodocを配慮し、指定してはいけません。

```go
// 正しい：
func (n *Node) Parent1() *Node {}
func (n *Node) Parent2() (*Node, error) {}

// 間違い：
func (n *Node) Parent1() (node *Node) {}
func (n *Node) Parent2() (node *Node, err error) {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>


## パッケージのコメント

- 【必須】パッケージのコメントは、パッケージ節の前に、空行無しで書かなければなりません。

```go
// パッケージのmathは、基本的な定数と数学関数を提供します
package math
```

```go
/*
templateは、HTMLなどのテキスト出力を生成する
データ駆動型テンプレートになります。
....
*/
package template
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## パッケージ名

- 【必須】パッケージから公開されているすべての識別子への参照は、パッケージ名を通して行われるので、識別子にパッケージ名を使っている場合は外さなければなりません。

たとえば、`chubby`というパッケージの中で、`ChubbyFile`という名前を作成した場合、呼び出し時に`chubby.ChubbyFile`となってしまうので避けなければなりません。

かわりに`File`という名前を作成すると、`chubby.File`で使用できます。

- 【推奨】パッケージ名を検討する場合、次のルールの検討を推奨します。
  - 大文字やアンダースコアは使用せず、すべて小文字で命名する。
  - ほとんどの呼び出し側が、名前付きインポートの必要がないようにする。
  - 短く簡潔にする。すべての呼び出し側で識別されることを意識する。
  - 複数形にしない。
  - common、util、shared、libなどは、何の情報もない名前なので、使用しない。

パッケージ名の詳細は、『[Package names - go.dev](https://go.dev/doc/effective_go#package-names)』をご覧ください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## ポインタ

- 【推奨】数バイトを節約する目的で、引数にポインタを使用することは推奨しません。
- 【推奨】関数が全体をとおして引数`x`を`*x`で呼び出している場合、引数をポインタにすることは推奨しません。これは、文字列のポインタ`string`や、インターフェースのポインタ`io.Reader`も該当します。大きなStructや、今後大きくなりそうなものは例外です。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## レシーバ名

- 【必須】レシーバ名は、一貫性をもたせなければなりません（例：型名がClientの場合、`c`と`cl`が混在してはいけません）。
- レシーバ名は、可能な限り最小にします（例：型名がClientの場合、`c`または`cl`とします）。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## レシーバの型

- 【必須】レシーバがmap、func、チャネルの場合、ポインタを使用してはいけません。
- 【必須】レシーバがスライスで、メソッドがスライスを作り直さない場合、ポインタを使用してはいけません。
- 【必須】メソッドが値を変更する必要がある場合、レシーバはポインタでなければなりません。
- 【必須】レシーバがsync.Mutexか、似たような同期するフィールドをもつ構造体の場合、レシーバはポインタでなければなりません。
- 【必須】レシーバの型を混在してはいけません。すべてのメソッドのレシーバはポインタ型、値型のどちらかを選択しなければなりません。
- 【必須】上記の規定に該当しない場合、レシーバはポインタでなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## テストの失敗例

- 【推奨】テストが失敗した場合、次の項目を伝える有効なメッセージの出力を推奨します。
  - なにが悪かったのか
  - どんな入力があったか
  - 実際にどんな値が来たのか
  - どんな値が来ることを期待していたのか

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 変数名

- 【必須】変数を宣言した場所よりも、離れた場所での使用が想定される場合、より説明的な変数名しなければなりません。
- 【推奨】より珍しいものや、パッケージ外で使われるものの名前は、より説明的な名前を推奨します。
- 【推奨】同様に、パッケージ外部で使用される変数名は、より説明的な変数名を推奨します。
- 【推奨】ループの添字や、読み込みのリーダーのような一般的な変数名は、iやrのように1文字を推奨します。
- メソッドレシーバ名は、1文字から2文字とします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 関数名

- 【必須】原則として、関数名は、Goコミュニティの規則である『[MixedCaps]( https://golang.org/doc/effective_go.html#mixed-caps )』に従わなければなりません。

テストの関数は例外です。`TestMyFunction_WhatIsBeingTested`のように、テストの目的の明示に、アンダースコアで分割します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

