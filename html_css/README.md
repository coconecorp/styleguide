# HTML/CSSスタイルガイド

  
<details><summary>目次</summary>

- [はじめに](#はじめに)
- [全般](#全般)
  - [一般的なスタイルルール](#一般的なスタイルルール)
    - [プロトコル](#プロトコル)
  - [全般的なフォーマッティングルール](#全般的なフォーマッティングルール)
    - [インデント](#インデント)
    - [末尾の空白](#末尾の空白)
  - [一般的なメタルール](#一般的なメタルール)
    - [エンコーディング](#エンコーディング)
    - [コメント](#コメント)
- [HTML](#html)
  - [HTMLスタイルのルール](#htmlスタイルのルール)
    - [ドキュメントのタイプ](#ドキュメントのタイプ)
    - [HTMLの妥当性](#htmlの妥当性)
    - [セマンティクス](#セマンティクス)
    - [関心の分離](#関心の分離)
    - [実体参照](#実体参照)
  - [HTMLフォーマット規則](#htmlフォーマット規則)
    - [一般的なフォーマット](#一般的なフォーマット)
    - [HTMLの引用符](#htmlの引用符)
  - [タグのルール](#タグのルール)
    - [img要素のwidth属性、height属性](#img要素のwidth属性height属性)
- [CSS](#css)
  - [CSSスタイルルール](#cssスタイルルール)
    - [CSSの妥当性](#cssの妥当性)
    - [IDとクラスの命名](#idとクラスの命名)
    - [要素型セレクタ](#要素型セレクタ)
    - [0と単位](#0と単位)
    - [先頭の 0](#先頭の-0)
    - [16進表記](#16進表記)
    - [IDとクラス名の命名規則](#idとクラス名の命名規則)
    - [CSSハック](#cssハック)
  - [CSSフォーマット規則](#cssフォーマット規則)
    - [ブロックコンテンツのインデント](#ブロックコンテンツのインデント)
    - [インデント](#インデント-1)
    - [改行](#改行)
    - [宣言の終了](#宣言の終了)
    - [プロパティ名の終了](#プロパティ名の終了)
    - [セレクタおよび宣言の分離](#セレクタおよび宣言の分離)
    - [ルールの分離](#ルールの分離)
    - [CSSの引用符](#cssの引用符)
  - [パフォーマンス](#パフォーマンス)
    - [全称セレクタ`*`](#全称セレクタ)
    - [子孫セレクタ](#子孫セレクタ)
    - [複雑なセレクタ](#複雑なセレクタ)
    - [!important](#important)

</details>

## はじめに

- 本ガイドラインは、[ココネ株式会社](https://www.cocone.co.jp/)のHTML/CSSのスタイル基準を示すものです。
- 本ガイドラインは、『[Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)』を参考に規定しています。
- 本ガイドラインで未定義のスタイルや、詳細を定義していない箇所の議論となった場合は、『[Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)』を参考に検討することとします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 全般

### 一般的なスタイルルール

#### プロトコル

- 【必須】画像やその他のメディアファイル、スタイルシート、スクリプトには、HTTPS経由で使用できない場合を除き、常にHTTPS「https:」を使用しなければなりません。

HTTPS通信をするサイトで、HTTPで読み込んでいるリソース（画像、スクリプトファイルなど）が存在している（いわゆる『[Mixed content(混在コンテンツ)](https://developer.mozilla.org/ja/docs/Web/Security/Mixed_content)』）場合、ブラウザ側で安全性の理由から読み込みをブロックしてしまう場合があるため、デザインが崩れた状態で表示されたり、機能上の不具合がある状態で表示される可能性があります。<br>
セキュリティの観点からも暗号化通信を導入している意味が無くなるため、安全なサイトといえなくなります。

HTMLの場合：

```html
<!-- 間違い：プロトコルを省略 --><script src="//ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
<!-- 間違い：HTTPを使用 --><script src="http://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
<!-- 正しい --><script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.0/jquery.min.js"></script>
```

CSSの場合：
```css
/* 間違い：プロトコルを省略 */@import '//fonts.googleapis.com/css?family=Open+Sans';
/* 間違い：HTTPを使用 */@import 'http://fonts.googleapis.com/css?family=Open+Sans';
/* 正しい */@import 'https://fonts.googleapis.com/css?family=Open+Sans';
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 全般的なフォーマッティングルール

#### インデント

- 【必須】HTMLのインデントは、半角スペース4つとしなければなりません。

```html
<h2 class="title info">おしらせ</h2>
<ul class="infoList">
    <li class="item banner">
        <a href="##
htmlcssスタイルガイド" class="banner"><img src="/assets/img/banner_254x49.png" /></a>
        <p>アイテム追加のお知らせ</p>
    </li>
    <li class="item banner">
        <a href="##
htmlcssスタイルガイド" class="banner"><img src="/assets/img/banner_254x49.png" /></a>
        <p>アイテム追加のお知らせ</p>
    </li>
</ul>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 末尾の空白

- 【必須】末尾の空白は削除しなければなりません。

差分を複雑にする可能性があるため、末尾の空白は不要です。

```html
<!-- 間違い：</p>の後ろに5つの半角スペースが存在 -->
<p>What?</p>     

<!-- 正しい： -->
<p>Yes please.</p>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 一般的なメタルール

#### エンコーディング

- 【必須】エンコーディングはHTML、CSS共にUTF-8（BOMなし）でなければなりません。

HTMLは `<meta charset="utf-8">` で文書のエンコーディングを指定します。

```html
<meta charset="utf-8" />
```

スタイルシートはデフォルトでUTF-8を想定しているため、エンコーディングの指定は不要です。

```css
/* 間違い：以下の指定は不要です */
@charset "utf-8";
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### コメント

- 【推奨】必要に応じてコメントを使用し、コードの目的等の明示を推奨します。

何をカバーしているか、どんな目的を果たしているか、なぜそれぞれの解決策が使用されるか、または望ましいか等の文書化にコメントを使用してください。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## HTML

### HTMLスタイルのルール

#### ドキュメントのタイプ

- 【必須】HTML5(HTML構文：&lt;!DOCTYPE html&gt;)を使用しなければなりません。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### HTMLの妥当性

- 【必須】妥当性のあるHTMLを使用しなければなりません。

妥当性のあるHTMLとは『[The W3C Markup Validation Service](https://validator.w3.org/)』などのHTMLバリデートツールでValidな状態を指します。

独自の構文を使用する場合以外は、ValidなHTMLを使用します。

```html
<!-- 間違い： -->
<title>Test</title>
<article>This is only a test.
 
<!-- 正しい： -->
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Test</title>
    </head>
    <body>
        <article>This is only a test.</article>
    </body>
</html>
```

例： p要素やli要素など、終了タグが省略可能な場合でも省略してはなりません。

``` html
<!-- 間違い：終了タグの省略 -->
<p>新製品のご案内です。
<ul>
    <li>製品1
    <li>製品2
</ul>
 
<!-- 正しい： -->
<p>新製品のご紹介です。</p>
<ul>
    <li>製品1</li>
    <li>製品2</li>
</ul>
```

例：void要素（終了タグが存在せず常に開始タグのみで記述される要素）は閉じることを推奨します。

```html
<!-- 非推奨： -->
<br>
 
<!-- 推奨： -->
<br />
<hr />
<img />
<input />
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### セマンティクス

- 【推奨】原則として、目的に応じた要素の使用を推奨します。

例：見出しにh1要素、リストにli要素、リンクにa要素を使用します。

```html
<h1>お知らせ</h1>
<ul>
    <li>
        <a href="xx.html">
            <h2>秋の新色のご案内</h2>
            <p>秋に向け、新色を追加しました。</p>
        </a>
    </li>
</ul>
```

目的に応じた要素の指定は、アクセシビリティ、再使用、コード効率の観点からも重要です。

```html
<!-- 間違い： アクセシビリティが劣る -->
<div onclick="goToRecommendations();">全てのおすすめ商品</div>
 
<!-- 正しい： -->
<a href="/recommendations/">全てのおすすめ商品</a>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 関心の分離

- 【必須】HTML（構造）、CSS（プレゼンテーション）、およびスクリプト（振舞い）を厳密に区別し、3つの間の相互作用を最小限に抑えなければなりません。

ドキュメントとテンプレートはHTMLのみを含み、HTMLは構造上の目的でのみ使用します。そしてプレゼンテーションをスタイルシートに、振舞いをスクリプトにまとめます。<br>
また、ドキュメントやテンプレートからのCSSファイルやJSファイルの読み込みを可能な限り少なくし、参照範囲を最小限にします。<br>
構造のプレゼンテーションと振舞いの分離は、メンテナンスの観点からも重要です。HTML文書やテンプレートの変更作業は、スタイルシートやスクリプトの更新作業よりも、コストが常にかかります。

```html
<!-- 間違い：構造とプレゼンテーションが分離できておらず、参照範囲も広い -->
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>お知らせ</title>
        <link rel="stylesheet" href="default.css" />
        <link rel="stylesheet" href="base.css" media="screen">
        <link rel="stylesheet" href="grid.css" media="screen">
        <link rel="stylesheet" href="print.css" media="print">
    </head>
    <body>
        <h1  style="font-size: 1.5em;">お知らせ</h1>
        <h2 style="margin: 12px; color:#c00">ご注意</h2>
        <p style="text-align:center;">夏季休暇は8月11日からになります。</p>
    </body>
</html>
 
 
<!-- 正しい： -->
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>お知らせ</title>
        <link rel="stylesheet" href="default.css" />
    </head>
    <body>
        <h1 class="title">お知らせ</h1>
        <div class="note">
            <h2>ご注意</h2>
            <p>夏季休暇は8月11日からになります。</p>
        </div>
    </body>
</html>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 実体参照

- 【推奨】原則として、実体参照の使用は推奨しません。

エンコーディングにUTF-8を使用している場合、`\&mdash;`（`—`）、`\&rdquo;`（`”`）、 `\&#x263a;`（☺）などの実体参照の使用は不要です（特別な意味をもつ文字`\&lt;`（`<`）`\&amp;`（`&`）、制御文字、または見えない文字`\&nbsp;`（半角スペース）は例外です）。

```html
<!-- 非推奨： -->
ユーロの通貨記号は &ldquo;&euro;&ldquo; です
見出し要素 <h1>
 
<!-- 推奨： -->
ユーロの通貨記号は “€” です
見出し要素　&lt;h1&gt;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### HTMLフォーマット規則

#### 一般的なフォーマット

- 【推奨】対象の要素がブロック、リスト、またはテーブル要素の子要素はインデントの指定を推奨します。
- 【推奨】すべてのブロック、リスト、またはテーブル要素は新しい行での指定を推奨します。

```html
<ul class="list">
    <li>
        <a href="##
htmlcssスタイルガイド" class="wrap">
            <p class="img"><img src="./img/thumbnail_48x48.png"></p>
            <div class="info">
                <p class="date">6月8日（金）</p>
                <p class="detail">記事の内容</p>
            </div>
        </a>
    </li>
</ul>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### HTMLの引用符

- 【必須】属性値を引用符で囲む場合は、シングルクォート`'`ではなく、ダブルクォート`"`を使用しなければなりません。

```html
<!-- 間違い：シングルクォート -->
<a class='maia-button maia-button-secondary'>Sign in</a>
 
<!-- 正しい： -->
<a class="maia-button maia-button-secondary">Sign in</a>
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### タグのルール

#### img要素のwidth属性、height属性

- 【推奨】img要素にサイズ指定が必要な場合、width属性、height属性の指定を推奨します。

画像の領域が一瞬、崩れたように表示されるレイアウトシフト（Layout Shift）が発生する場合、width属性、height属性を指定します。

```html
<p class="thumb"><img src="..." width="123" height="123"></p>
```

参考：『[Optimize Cumulative Layout Shift](https://web.dev/optimize-cls/)』

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## CSS

### CSSスタイルルール

#### CSSの妥当性

- 【必須】妥当性のあるCSSを使用しなければなりません。

妥当性のあるCSSとは『[CSS Validation Service](https://jigsaw.w3.org/css-validator/)』などのHTMLバリデートツールでValidな状態を指します。<br>
CSSバリデーターのバグに対応する場合や、独自の構文を要求する場合以外は、ValidなCSSを使用します。

```css
/* 間違い：妥当性のないCSS */
_:-ms-lang(x)::-ms-backdrop, .css-hack {
    color: gray;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### IDとクラスの命名

- 【推奨】原則として、意味があるIDとクラス名を使用を推奨します。


『[Tailwind CSS](https://tailwindcss.com/)』のような見た目の指定をclass属性に直接指定するようなフレームワークを使用する場合を除き、要素の目的を反映したID名またはクラス名の使用を推奨します。<br>
具体的で要素の目的を反映した名前は、理解しやすく変更される可能性が低くなります。

```css
/* 推奨： */
#gallery {}
.video {}
```

単語の省略で、意味が伝わりにくくなる場合がるので注意しましょう。

```css
/* 非推奨：意味が理解できない ​*/
.cr{} /* current */
.ttl {} /* title */
 
/* 推奨： */
#nav {}
.author {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 要素型セレクタ

- 【必須】要素型セレクタでIDやクラス名を修飾してはいけません。
- 【必須】（ヘルパークラスなどで）必要な場合以外は、IDやクラスと一緒に要素名を使用してはいけません。

不要な先祖セレクタの指定は、パフォーマンスの低下につながります。

```css
/* 間違い：要素型セレクターの使用 */
ul#example {}
div.error {}
 
/* 正しい： */
#example {}
.error {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 0と単位

- 【必須】必要でない限り、0の値の後の単位指定は省略しなければなりません。

```css
flex: 0px; /* flexは単位が必要 */
flex: 1 1 0px; /* IE11で単位が必要 */
margin: 0;
padding: 0;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 先頭の 0

- 【必須】小数点の先頭の0を省略してはいけません。

```css
/* 間違い： */
font-size: .8em;
transition: color .3s linear;
 
/* 正しい： */
font-size: 0.8em;
transition: color 0.3s linear;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 16進表記

- 【必須】16進数表記で指定する場合、可能な限り3文字にしなければなりません。

カラー表記は、6文字よりも3文字の方がより短く、より簡潔です。

```css
/* 間違い：6文字で省略可能 */
color: #cc0000;
 
/* 正しい： */
color: #c00;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### IDとクラス名の命名規則

- 【必須】IDとクラスの命名はケバブケースを採用しなければなりません。

ローワーキャメルケースや、スネークケースは採用しないでください。

```css
/* 間違い： */
.missiontype {}
.missionType {} /* ローワーキャメルケース */
.mission_type {} /* スネークケース */
 
/* 正しい */
.mission-type {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### CSSハック

- 【推奨】ユーザエージェントの検出やCSSハックの使用は推奨しません。

CSSハックの使用はまず避けなくてはなりません。そして最後の手段と考えるべきです。<br>
CSSハックは可読性が悪く、CSSが妥当ではない場合があります。またブラウザ依存の短期的な対応になるため、長期的には負債を生む原因になります。

```css
/* 非推奨：IE11のみ対応 */
_:not(_)::-ms-backdrop, .selector {
    property: value;
}
 
/* 非推奨：ChromeとOperaのみ対応 */
_::content, _:future, p.text:not(*:root) {
    color: gray;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### CSSフォーマット規則

#### ブロックコンテンツのインデント

- 【必須】すべてのブロックコンテンツをインデントしなければなりません。

すべての『[ブロックコンテンツ](https://www.w3.org/TR/CSS21/syndata.html#block)』をインデントすることで、可読性が向上します。

```css
/* 間違い： */
@media screen, projection {
html {
    background: #fff;
    color: #444;
}
}
 
/* 正しい： */
@media screen, projection {
    html {
        background: #fff;
        color: #444;
    }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### インデント

- 【必須】CSSのインデントは、半角スペース4つとしなければなりません。
- 【必須】セレクタ名直後の波括弧`{`の直前は、半角スペース1つで離さなければなりません。
- 【必須】各プロパティごとのセミコロン`;`の前に半角スペースを指定してはいけません。

```css
/* 間違い： */
b.icon{
  　　　　margin: 0 4px ;
  　　　　width: 25px ;
  　　　　height: 19px ;
}
 
/* 正しい： */
b.icon {
    margin: 0 4px;
    width: 25px;
    height: 19px;
    background: url('../assets/img/icon/icon_sprite.png') no-repeat;
    -webkit-background-size: auto 41px;
    background-position: left top;
}
```

可読性向上のため指定を1行にまとめている場合、

- 【必須】波括弧`{`の直後は、半角スペース1つで離さなければなりません。
- 【必須】波括弧`}`の直前は、半角スペース1つで離さなければなりません。

```css
/* 間違い： */
.avatar {width: 30px;}
.thumbnail {width: 150px;}
 
/* 正しい： */
.avatar { width: 30px; }
.thumbnail  { width: 150px; }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 改行

- 【必須】原則として、指定の始まりの波括弧`{`の直後は、改行を指定しなければなりません。
- 【必須】指定の終わりの波括弧`}`の直後は、改行を指定しなければなりません。
- 【必須】原則として、各プロパティごとのセミコロン`;`の直後は、改行を指定しなければなりません。

``` css
/* 間違い： */
.title > strong
{
    display: block; font-size: 12px;
    color: #666;}
 
/* 正しい： */
.title > strong { /*　指定の始まり */
    display: block; /* 各プロパティ毎 */
    font-size: 12px; /* 各プロパティ毎 */
    color: #666; /* 各プロパティ毎 */
} /*　指定の終わり */
```

- 【推奨】同種類のプロパティを複数指定する場合は可読性向上を目的に、指定の始まりと各プロパティごとの改行指定の省略を推奨します。

以下では改行の基本ルールに準拠した場合、行数が3倍に増加し可読性が低下します。

```css
/* 推奨： */
.sample1 { width: 100px; }
.sample2 { width: 110px; }
.sample3 { width: 120px; }
.sample4 { width: 130px; }
.sample5 { width: 140px; }
 
/* 非推奨：基本ルールに準拠 */
.sample1 {
    width: 100px;
}
.sample2 {
    width: 110px;
}
.sample3 {
    width: 120px;
}
.sample4 {
    width: 130px;
}
.sample5 {
    width: 140px;
}
```

- 【推奨】backgroundプロパティがマルチバックグラウンドの場合、カンマ`,`の直後に改行の指定を推奨します。

マルチバックグラウンドの場合、改行の指定で可読性の向上が期待できます。

```css
/* 非推奨： */
.sample1 {
    background: url('../assets/img/bg/sky.png') 50% 100% no-repeat,  url('../assets/img/bg/water.png') 0　0 no-repeat;
}
.sample2 {
    background: linear-gradient( 8deg,blue 13%,yellow,red ), linear-gradient( red, yellow, blue 130px, yellow ),　linear-gradient( yellow, blue 22%, red, yellow );
}
 
/* 推奨： */
.sample1 {
    background: url('../assets/img/bg/sky.png') 50% 100% no-repeat,  /* カンマ`,`の後に改行 */
    url('../assets/img/bg/water.png') 0　0 no-repeat;
}
.sample2 {
    background: linear-gradient( 8deg,blue 13%,yellow,red ), /* カンマ`,`の後に改行 */
    linear-gradient( red, yellow, blue 130px, yellow ), /* カンマ`,`の後に改行 */
    linear-gradient( yellow, blue 22%, red, yellow );
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 宣言の終了

- 【必須】各プロパティの宣言の直後は、セミコロン`;`を指定しなければなりません。

一貫性と拡張性の理由から、すべての宣言をセミコロンで終了してください。

```css
/* 間違い： */
.test {
    display: block;
    height: 100px
}
 
/* 正しい： */
.test {
    display: block;
    height: 100px;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### プロパティ名の終了

- 【必須】コロン`:`の直後は、半角スペース1つで離さなければなりません。

```css
/* 間違い： */
h3 {
    font-weight:bold;
}
 
/* 正しい： */
h3 {
    font-weight: bold;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### セレクタおよび宣言の分離

- 【必須】セレクタと宣言は改行で区切らなければなりません。

それぞれのセレクタと宣言に対は、必ず新しい行から開始してください。

```css
/* 間違い： */
a:focus, a:active {
    position: relative; top: 1px;
}
 
/* 正しい： */
h1,
h2,
h3 {
    font-weight: normal;
    line-height: 1.2;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### ルールの分離

- 【必須】改行でルールを区切らなければなりません。
- 【推奨】ルールの間隔は空行の追加を推奨します。

```css
/* 非推奨： */
html {
    background: #fff;
}
body {
    margin: auto;
    width: 50%;
}
 
/* 推奨： */
html {
    background: #fff;
}
 
body {
    margin: auto;
    width: 50%;
}
```

ルールの間隔で空行を追加しないほうが読みやすい場合、1行分の改行を指定します。

```css
/* 非推奨： */
.sample1 { width: 100px; height: 100px; }
 
.sample2 { width: 110px; height: 110px; }
 
.sample3 { width: 120px; height: 120px; }

/* 推奨： */
.sample1 { width: 100px; height: 100px; }
.sample2 { width: 110px; height: 110px; }
.sample3 { width: 120px; height: 120px; }
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### CSSの引用符

- 【推奨】属性セレクタとプロパティ値には、ダブルクォート`"`ではなくシングルクォート`'`の使用を推奨します。
- 【推奨】URI値`url()`に引用符はシングルクォート`'`を推奨します。

```css
/* 非推奨： */
@import url("https://www.google.com/css/maia.css");
 
html {
    font-family: "open sans", arial, sans-serif;
}
 
/* 推奨： */
@import url('https://www.google.com/css/maia.css');
 
html {
    font-family: 'open sans', arial, sans-serif;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### パフォーマンス

#### 全称セレクタ`*`

- 【必須】原則として、全称セレクタ`*`の使用は避けなければなりません。

セレクタの参照は、右から左の方向で行われます。<br>
全称セレクタ`*`を使用すると、すべてのDOM要素を列挙した後、対象のセレクタを絞っていく流れとなるため、コストが高くパフォーマンス低下する結果となります。

```css
.main > ul > * {
    color: red;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 子孫セレクタ

- 【必須】不要な子孫セレクタの使用は避けなければなりません。

子孫セレクタが少ない程、パフォーマンスの向上に繋がります。

```css
/* 間違い： */
.list li ul li {
    color: red;
}
 
/* 正しい： */
.list li li {
    color: red;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### 複雑なセレクタ

- 【推奨】一般兄弟結合子`~`、隣接兄弟結合子`+`の使用はコストが高くなるため、推奨しません。

```css
/* 非推奨：任意の画像の兄弟で、
   その画像より後方にある段落 */
img ~ p {
    color: red;
}
 
/* 非推奨：画像の直後に来る段落 */
img + p {
    font-style: bold;
}
```

- 【推奨】属性セレクタで、複雑な正規表現の使用はコストが高くなるため、推奨しません。

```css
/* 非推奨： */
li[class^="a"] {}
li[class^="a" i] {}
li[class$="-box"] {}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

#### !important

- 【必須】原則として、`!important`の使用は避けなければなりません。

優先順位が最上位になり、自然のカスケードを破壊するためデバッグが難しくなるので、極力避けるべきです。またパフォーマンスの低下にも繋がります。<br>
例外として、外部のCSSライブラリを上書きする場合のみ、!importantを使用します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>