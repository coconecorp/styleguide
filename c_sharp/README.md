# C\#コーディング規則

<details><summary>目次</summary>

- [はじめに](#はじめに)
- [名前付け規則](#名前付け規則)
  - [Pascal形式](#pascal形式)
  - [Camel形式](#camel形式)
- [レイアウト規則](#レイアウト規則)
- [コメント規則](#コメント規則)
- [言語ガイドライン](#言語ガイドライン)
  - [文字データ型](#文字データ型)
  - [暗黙的に型指定されたローカル変数](#暗黙的に型指定されたローカル変数)
  - [例外処理での`try-catch`および`using`ステートメント](#例外処理でのtry-catchおよびusingステートメント)
  - [`new`演算子](#new演算子)
  - [静的メンバー](#静的メンバー)
  - [LINQクエリ](#linqクエリ)
- [コーディングスタイル](#コーディングスタイル)

</details>

## はじめに

- 本ガイドラインは、[ココネ株式会社](https://www.cocone.co.jp/)におけるC\#のコーディング規則を示すものです。
- 本ガイドラインは、『[Microsoft C#コーディング規則](https://docs.microsoft.com/ja-jp/dotnet/csharp/fundamentals/coding-style/coding-conventions)』を参考に規定しています。
- 本ガイドラインで未定義のスタイルや、詳細を定義していない箇所の議論となった場合は、『[Microsoft C#コーディング規則](https://docs.microsoft.com/ja-jp/dotnet/csharp/fundamentals/coding-style/coding-conventions)』を参考に検討することとします。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 名前付け規則

### Pascal形式

- 【必須】`class`、`record`、`struct`の名前を付ける場合は、Pascal形式（"PascalCasing"）を使用しなければなりません。

```c#
// classの指定
public class DataService
{
}

// recordの指定
public record PhysicalAddress(
    string Street,
    string City,
    string StateOrProvince,
    string ZipCode);

// structの指定
public struct ValueCoordinate
{
}
```

- 【必須】`interface`に名前を付ける場合は、Pascal形式を使用しなければなりません。
- 【推奨】`interface`に名前を付ける場合は、名前の先頭に`I`を付けることを推奨します。

```c#
// interfaceの指定
public interface WorkerQueue
{
}

// interfaceの指定。先頭にIを付けたらなお良し
public interface IWorkerQueue
{
}
```

- 【推奨】フィールド、プロパティ、イベント、メソッド、ローカル関数などの型の`public`メンバーに名前を付ける場合は、Pascal形式の使用を推奨します。

```c#
public class ExampleEvents
{
    // 使用は控えめに
    public bool IsValid;

    // initのみのプロパティ
    public IWorkerQueue WorkerQueue { get; init; }

    // イベント
    public event Action EventProcessing;

    // メソッド
    public void StartEventProcessing()
    {
        // ローカル関数
        static int CountQueueItems() => WorkerQueue.Count;
        // ...
    }
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### Camel形式

- 【必須】`private`または`internal`のフィールドに名前を付ける場合は、Camel形式（"camelCasing"）を使用しなければなりません。

```c#
public class DataService
{
    private IWorkerQueue workerQueue;
}
```

- 【推奨】メソッドのパラメータを記述する場合は、Camel形式の使用を推奨します。

```c#
public T SomeMethod<T>(int someNumber, bool isValid)
{
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## レイアウト規則

- 【必須】次のコードに示すように、式に句を作成するときは括弧を使用しなければなりません。

```c#
if ((val1 > val2) && (val1 > val3))
{
    // 適切な処理を行う
}
```

- 【推奨】コード エディタのデフォルトの設定（スマート インデント、4文字インデント、タブを空白として保存）の使用を推奨します。
- 【推奨】1つの行には1つのステートメントのみ記述することを推奨します。
- 【推奨】1つの行には1つの宣言のみ記述することを推奨します。
- 【推奨】継続行にインデントが自動的に設定されない場合は、1タブ ストップ（4つの半角スペース）分のインデントの設定を推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## コメント規則

- 【推奨】コメントは、コード行の末尾ではなく別の行に記述することを推奨します。
- 【推奨】コメント デリミター`//`とコメント テキストの間に空白を1つ挿入することを推奨します。

```c#
// 次の宣言は、クエリを作成します。
// クエリを実行するわけではありません。
```

- 【推奨】アスタリスクを整形したブロックでコメントを囲まないことを推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## 言語ガイドライン

### 文字データ型

- 【推奨】短い文字列を連結する場合は、[文字列補間](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/tokens/interpolated)の使用を推奨します。

```c#
string displayName = $"{nameList[n].LastName}, {nameList[n].FirstName}";
```

- 【推奨】ループ内で文字列を追加する場合（特に大量のテキストを処理する場合）は、[StringBuilder](https://docs.microsoft.com/ja-jp/dotnet/api/system.text.stringbuilder)オブジェクトの使用を推奨します。

```c#
var phrase = "lalalalalalalalalalalalalalalalalalalalalalalalalalalalalala";
var manyPhrases = new StringBuilder();
for (var i = 0; i < 10000; i++)
{
    manyPhrases.Append(phrase);
}
//Console.WriteLine("tra" + manyPhrases);
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 暗黙的に型指定されたローカル変数

- 【推奨】変数の型が割り当ての右側から明らかである場合、または厳密な型が重要でない場合は、ローカル変数の暗黙の型指定の使用を推奨します。

```c#
var var1 = "This is clearly a string.";
var var2 = 27;
```

- 【推奨】割り当ての右側から型が明らかではない場合、[var](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/var)の使用を推奨しません。 メソッド名から型が明らかであると想定しないでください。 変数の型は、`new`演算子または明示的なキャストの場合に明らかであると見なされます。

```c#
int var3 = Convert.ToInt32(Console.ReadLine()); 
int var4 = ExampleClass.ResultSoFar();
```

- 【推奨】変数の型を指定する場合、変数名への依存は推奨しません。 正しくない変数名の場合があるためです。 次の例では、変数名`inputInt`は誤解を招きます。

```c#
var inputInt = Console.ReadLine();
Console.WriteLine(inputInt);
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 例外処理での`try-catch`および`using`ステートメント

- 【推奨】例外処理には、[try-catch](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/try-catch)ステートメントの使用を推奨します。

```c#
static string GetValueFromArray(string[] array, int index)
{
    try
    {
        return array[index];
    }
    catch (System.IndexOutOfRangeException ex)
    {
        Console.WriteLine("Index is out of range: {0}", index);
        throw;
    }
}
```

- 【推奨】コードを簡潔にする目的で、C#の[usingステートメント](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/using-statement)の使用を推奨します。 [try-finally](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/try-finally)ステートメントを使用するときに`finally`ブロックのコードが[Dispose](https://docs.microsoft.com/ja-jp/dotnet/api/system.idisposable.dispose)メソッドの呼び出しだけである場合は、`using`ステートメントを代わりに使用します。

次の例で、`try-finally`ステートメントは`finally`ブロックでのみ`Dispose`を呼び出します。

```c#
Font font1 = new Font("Arial", 10.0f);
try
{
    byte charset = font1.GdiCharSet;
}
finally
{
    if (font1 != null)
    {
        ((IDisposable)font1).Dispose();
    }
}
```

`using`ステートメントを使用して同じことを行うことができます。

```c#
using (Font font2 = new Font("Arial", 10.0f))
{
    byte charset2 = font2.GdiCharSet;
}
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### `new`演算子

- 【推奨】オブジェクトを作成する場合、オブジェクト初期化子の使用を推奨します。

オブジェクト初期化子を使用することで、コードを簡潔にできます。

```c#
var instance = new ExampleClass { Name = "Desktop", ID = 37414,
    Location = "Redmond", Age = 2.3 };
```

次の例は、初期化子を使用していません。

```c#
// 非推奨
var instance = new ExampleClass();
instance.Name = "Desktop";
instance.ID = 37414;
instance.Location = "Redmond";
instance.Age = 2.3;
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### 静的メンバー

- 【推奨】[静的](https://docs.microsoft.com/ja-jp/dotnet/csharp/language-reference/keywords/static)メンバーは、クラス名`ClassName.StaticMember`を使用して呼びだすことを推奨します。 静的アクセスが明確になり、コードがよりわかりやすくなります。
- 【推奨】派生クラスの名前をもつ基本クラスに定義された静的メンバーの指定は推奨しません。 コンパイルすると、コードが読みやすくなくなり、派生クラスに同じ名前の静的メンバーを追加すると、将来的にコードを中断する場合があります。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

### LINQクエリ

- 【推奨】クエリ変数にはCamel形式（"camelCasing"）の使用を推奨します。

```c#
var seattleCustomers = from customer in customers
                       where customer.City == "Seattle"
                       select customer.Name;
```

- 【推奨】エイリアスは、Pascal形式（"PascalCasing"）の使用を推奨します。

```c#
var localDistributors =
    from customer in customers
    join distributor in distributors on customer.City equals distributor.City
    select new { Customer = customer, Distributor = distributor };
```

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>

## コーディングスタイル

- 【必須】インデントは4つの半角スペースを使用しなければなりません。タブは使用してはいけません。
- 【必須】単一ステートメントの`if`を使用する場合、一行形式は絶対に使用してはなりません（例：`if (source == null) throw new ArgumentNullException("source");`）。
- 【必須】単一ステートメントの`if`を使用する場合、`if/else if/.../else`の複合文のいずれかのブロックに波括弧`{}`が使用されている場合や、1つの文の本文が複数行にわたる場合は、波括弧`{}`を使用しなければなりません。
- 【推奨】内部およびプライベートフィールドには、可能な限り`readonly`の使用を推奨します。
- 【推奨】静的なフィールドに使用する場合は、`static`の後に`readonly`の付与を推奨します（`static readonly`よりは`readonly static`を推奨します）。
- 【推奨】原則として、パブリックフィールドを使用してはいけません。パブリックフィールドを使用する場合はPascal形式（"PascalCasing"）の使用を推奨します。プレフィックスの付与は推奨しません。
- 【推奨】`this.`の使用は推奨しません。
- 【推奨】アクセス修飾子は最初の修飾子に使用することを推奨します（`abstract public`よりは`public abstract`を推奨します）。
- 【推奨】名前空間のインポートは、名前空間の前に宣言することを推奨します。

<div align="right">
<a href="#">⬆️ 先頭に戻る</a>
</div>