﻿---
title: 関数 (C++)
ms.date: 11/19/2018
helpviewer_keywords:
- defaults, arguments
- function definitions
- function definitions, about function definitions
- default arguments
- declarators, functions
ms.assetid: 33ba01d5-75b5-48d2-8eab-5483ac7d2274
ms.openlocfilehash: 1425ddebffc150158e88e44b1d2c22e3f85e5a31
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81375738"
---
# <a name="functions-c"></a>関数 (C++)

関数とは、何らかの操作を実行するコードのブロックです。 関数には、呼び出し元が関数に引数を渡すのに使用する入力パラメーターを必要に応じて定義できます。 関数は、必要に応じて値を出力として返すことができます。 関数は、一般的な操作を 1 つの再利用可能なブロックでカプセル化するのに役立ちます。関数には、その動作を明確に説明する名前を付けることが理想的です。 次の関数は、呼び出し元から 2 つの整数を受け取り、その合計を返します。*a*と*b*は**int**型の*パラメータ*です。

```cpp
int sum(int a, int b)
{
    return a + b;
}
```

この関数は、プログラム内の任意の数の場所から*呼び出したり、呼び出*すことができます。 関数に渡される値は*引数で、* その型は関数定義のパラメーター型と互換性がある必要があります。

```cpp
int main()
{
    int i = sum(10, 32);
    int j = sum(i, 66);
    cout << "The value of j is" << j << endl; // 108
}
```

関数の長さに事実上制限はありませんが、優れた設計では、適切に定義された 1 つのタスクを実行する関数を目標にします。 複雑なアルゴリズムは、可能な場合は常に、理解しやすい簡潔な関数に分割することをお勧めします。

クラス スコープで定義されている関数はメンバー関数と呼ばれます。 C++ では、他の言語とは異なり、名前空間スコープ (暗黙的なグローバル名前空間を含む) でも関数を定義できます。 このような関数は *、フリー関数*または*非メンバー関数*と呼ばれます。これらは標準ライブラリで広く使用されています。

関数は*オーバーロード*される可能性があるため、関数の異なるバージョンが仮パラメータの数や型によって異なる場合、同じ名前を共有できます。 詳細については、「[関数のオーバーロード](../cpp/function-overloading.md)」を参照してください。

## <a name="parts-of-a-function-declaration"></a>関数宣言部分

最小限の関数*宣言*は、戻り値の型、関数名、およびパラメーター リスト (空の場合があります) と、コンパイラに追加の命令を提供するオプションのキーワードで構成されます。 次の例は関数宣言です。

```cpp
int sum(int a, int b);
```

関数定義は、宣言と*body*で構成され、中かっこの間のすべてのコードです。

```cpp
int sum(int a, int b)
{
    return a + b;
}
```

関数宣言の後にはセミコロンが続きます。1 つのプログラムの複数個所で、関数宣言がなされる場合があります。 関数宣言は、翻訳単位ごとに関数に対する呼び出しの前に記述される必要があります。 関数定義は、単一定義規則 (ODR) に従い、プログラム内で 1 回だけ記述する必要があります。

関数宣言に必要な部分は次のとおりです。

1. 関数が返す値の型を指定する戻り値の**型。** C++11 では **、auto**は、コンパイラに戻りステートメントから型を推論するように指示する有効な戻り値の型です。 C++14 では、"decltype(auto)" も使用できます。 詳細については、以下の「戻り値の型の型推論」を参照してください。

1. 関数名は文字かアンダースコアで始まる必要があり、スペースを含めることはできません。 一般に、標準ライブラリ関数名で先頭にアンダースコアがあるものは、プライベート メンバー関数であるか、コードでの使用が意図されていない非メンバー関数であることを意味しています。

1. パラメーター リストとは、中かっこに挟まれ、コンマで区切られた 0 個以上のパラメーターのセットです。パラメーターで、型を指定し、関数本体内で値にアクセスする際に使用するローカル名も必要に応じて指定できます。

関数宣言の省略可能な部分は次のとおりです。

1. `constexpr`。関数の戻り値がコンパイル時に計算できる定数値であることを示します。

    ```cpp
    constexpr float exp(float x, int n)
    {
        return n == 0 ? 1 :
            n % 2 == 0 ? exp(x * x, n / 2) :
            exp(x * x, (n - 1) / 2) * x;
    };
    ```

1. そのリンケージ仕様、**エクスタン**または**静的**.

    ```cpp
    //Declare printf with C linkage.
    extern "C" int printf( const char *fmt, ... );

    ```

   詳細については、「[変換単位とリンケージ](../cpp/program-and-linkage-cpp.md)」を参照してください。

1. **inline**は、関数への呼び出しを関数コード自体に置き換えるコンパイラに指示します。 パフォーマンスが重要なコード セクションで関数が迅速に実行され、繰り返し呼び出されるシナリオでは、インライン展開を使用すると、パフォーマンスが向上します。

    ```cpp
    inline double Account::GetBalance()
    {
        return balance;
    }
    ```

   詳細については、「[インライン関数](../cpp/inline-functions-cpp.md)」を参照してください。

1. 関数`noexcept`が例外をスローできるかどうかを指定する式。 次の例では、式が**true**と評価された場合`is_pod`、関数は例外をスローしません。

    ```cpp
    #include <type_traits>

    template <typename T>
    T copy_object(T& obj) noexcept(std::is_pod<T>) {...}
    ```

   詳細については[、「noexcept」](../cpp/noexcept-cpp.md)を参照してください。

1. (メンバー関数のみ)関数が**const**であるか**volatile**であるかを指定する cv 修飾子。

1. (メンバー関数のみ)**仮想** `override`、 `final`、 、 、 、 の各 仮想の構成を行います。 **virtual**は、関数を派生クラスでオーバーライドできることを指定します。 `override` は、派生クラス内の関数が仮想関数をオーバーライドすることを意味します。 `final` は、いかなる派生クラス内でも関数がオーバーライドされないことを意味します。 詳細については、「[仮想関数](../cpp/virtual-functions.md)」を参照してください。

1. (メンバー関数のみ)**メンバー**関数に適用される static は、その関数がクラスのオブジェクト インスタンスに関連付けられていないことを意味します。

1. (非静的メンバー関数のみ)ref 修飾子は、暗黙的なオブジェクト パラメーター (this)\*が右辺値参照と左辺値参照の場合に選択する関数のオーバーロードをコンパイラに指定します。 詳細については、「[関数のオーバーロード](function-overloading.md#ref-qualifiers)」を参照してください。

次の図では、関数定義の一部を示しています。 網かけされた部分は関数本体です。

![関数定義部分](../cpp/media/vc38ru1.gif "関数定義部分") <br/>
関数定義部分

## <a name="function-definitions"></a>関数定義

*関数定義*は、変数宣言、ステートメント、および式を含む中かっこで囲まれた宣言と関数本体で構成されます。 次の例は、完全な関数定義を示しています。

```cpp
    int foo(int i, std::string s)
    {
       int value {i};
       MyClass mc;
       if(strcmp(s, "default") != 0)
       {
            value = mc.do_something(i);
       }
       return value;
    }
```

本体内で宣言された変数は、ローカル変数またはローカルと呼ばれます。 これらは関数の終了時にスコープ外に出るため、関数がローカルに参照を返すことはありません。

```cpp
    MyClass& boom(int i, std::string s)
    {
       int value {i};
       MyClass mc;
       mc.Initialize(i,s);
       return mc;
    }
```

## <a name="const-and-constexpr-functions"></a>const 関数と定数関数

メンバー関数を**const**として宣言すると、クラス内のデータ メンバーの値を変更することを許可されていない関数を指定できます。 const**としてメンバー**関数を宣言すると、コンパイラが const*の正確性*を強制するのに役立ちます。 **const**として宣言された関数を使用して、誤ってオブジェクトを変更しようとした場合、コンパイラ エラーが発生します。 詳細については、「 [const](const-cpp.md)」を参照してください。

コンパイル時に生成`constexpr`される値を決定できる場合に関数を宣言します。 constexpr 関数は、通常の関数よりも高速に実行されます。 詳細については、 [constexpr](constexpr-cpp.md)を参照してください。

## <a name="function-templates"></a>関数テンプレート

関数テンプレートはクラス テンプレートに似ており、テンプレート引数に基づく具体的な関数を生成します。 多くの場合、テンプレートは型引数を推測できるので、型引数を明示的に指定する必要はありません。

```cpp
template<typename Lhs, typename Rhs>
auto Add2(const Lhs& lhs, const Rhs& rhs)
{
    return lhs + rhs;
}

auto a = Add2(3.13, 2.895); // a is a double
auto b = Add2(string{ "Hello" }, string{ " World" }); // b is a std::string
```

詳細については、「[関数テンプレート」を参照してください。](../cpp/function-templates.md)

## <a name="function-parameters-and-arguments"></a>関数のパラメーターと引数

関数にはコンマで区切られた 0 個以上の型のパラメーター リストがあり、それぞれに関数本体内でアクセスする際に使用する名前があります。 関数テンプレートで、追加の型や値のパラメーターを指定できます。 呼び出し元は引数を渡します。引数は、パラメーター リストと互換性のある型を持つ具体的な値です。

既定では、引数は関数に値渡しで渡されます。このことは、関数が渡されるオブジェクトのコピーを受け取ることを意味します。 大きなオブジェクトの場合、コピーの作成は負荷が高く、必ずしも必要ではありません。 引数を参照 (特に左辺値参照) で渡す場合は、パラメータに参照量指定子を追加します。

```cpp
void DoSomething(std::string& input){...}
```

関数が参照によって渡される引数を変更すると、ローカル コピーではなく元のオブジェクトが変更されます。 関数がこのような引数を変更しないようにするには、パラメーターを const&として修飾します。

```cpp
void DoSomething(const std::string& input){...}
```

**C++ 11:** 右辺値参照または左辺値参照によって渡される引数を明示的に処理するには、汎用参照を示すためにパラメーターにダブルアンパサンドを使用します。

```cpp
void DoSomething(const std::string&& input){...}
```

パラメーター宣言リストで単一のキーワード**void**を使用して宣言された関数は、キーワード**void**が引数宣言リストの最初の唯一のメンバーである限り、引数を受け取りません。 リスト内の他の場所で**void**型の引数を指定すると、エラーが発生します。 次に例を示します。

```cpp

// OK same as GetTickCount()
long GetTickCount( void );
```

ここで説明した場合を除いて**void**引数を指定することは無効ですが **、void**型から派生した型 ( **void**へのポインターや**void**の配列など ) は、引数宣言リストの任意の場所に配置できます。

### <a name="default-arguments"></a>既定の引数

関数のシグネチャの最後のパラメーターに既定の引数を割り当てることができます。このことは、他の値を指定する必要がない場合は、関数を呼び出すときに呼び出し元が引数を省略できることを意味します。

```cpp
int DoSomething(int num,
    string str,
    Allocator& alloc = defaultAllocator)
{ ... }

// OK both parameters are at end
int DoSomethingElse(int num,
    string str = string{ "Working" },
    Allocator& alloc = defaultAllocator)
{ ... }

// C2548: 'DoMore': missing default parameter for parameter 2
int DoMore(int num = 5, // Not a trailing parameter!
    string str,
    Allocator& = defaultAllocator)
{...}
```

詳細については、「[既定の引数](../cpp/default-arguments.md)」を参照してください。

## <a name="function-return-types"></a>関数の戻り値の型

関数は別の関数や組み込みの配列を返さないかもしれません。ただし、これらの型へのポインター、または関数オブジェクトを生成する*ラムダ*を返すことができます。 これらの場合を除き、関数はスコープ内の任意の型の値を返す場合や、戻り値の型が**void**である場合は値を返さない場合があります。

### <a name="trailing-return-types"></a>後続の戻り値の型

"通常" の戻り値の型は、関数のシグネチャの左側にあります。 *末尾の戻り値の型*は、シグネチャの右端にあり、その前に -> 演算子が付きます。 後続の戻り値の型は、関数テンプレートにおいて、戻り値の種類がテンプレート パラメーターに依存する場合、特に便利です。

```cpp
template<typename Lhs, typename Rhs>
auto Add(const Lhs& lhs, const Rhs& rhs) -> decltype(lhs + rhs)
{
    return lhs + rhs;
}
```

**auto**を末尾の戻り値の型と組み合わせて使用する場合は、decltype 式が生成するもののプレースホルダーとして機能し、それ自体は型の推論を実行しません。

## <a name="function-local-variables"></a>関数のローカル変数

関数本体内で宣言される変数は、ローカル変数または単に*ローカル変数*と呼*ばれます*。 非静的ローカルは関数本体内でのみ認識され、スタックで宣言されている場合は、関数の終了時にスコープ外に出ます。 ローカル変数を構築して値で返す場合、コンパイラは通常、*名前付きの戻り値の最適化*を実行して不要なコピー操作を回避できます。 ローカル変数を参照渡しで返す場合、呼び出し元がその参照を使用するために実行する試行がローカルの破棄後に発生するため、コンパイラは警告を発行します。

C++ では、ローカル変数を "静的" として宣言することがあります。 変数は関数本体内でのみ認識されますが、関数のすべてのインスタンスに対して変数の 1 つのコピーが存在します。 ローカルな静的オブジェクトは、`atexit` によって指定された終了時に破棄されます。 プログラムの制御フローが宣言をバイパスしたために静的オブジェクトが構築されなかった場合、そのオブジェクトの破棄は試みられません。

## <a name="type-deduction-in-return-types-c14"></a><a name="type_deduction"></a>戻り値の型の型の推論 (C++14)

C++ 14 では **、auto**を使用して、末尾の戻り値の型を指定せずに、関数本体から戻り値の型を推論するようにコンパイラに指示できます。 **auto**は常に値による戻り値に変換されることに注意してください。 `auto&&` を使用すると、参照を推測するようにコンパイラに指示できます。

この例では **、auto**は、lhs と rhs の合計の非 const 値コピーとして推定されます。

```cpp
template<typename Lhs, typename Rhs>
auto Add2(const Lhs& lhs, const Rhs& rhs)
{
    return lhs + rhs; //returns a non-const object by value
}
```

**auto**は、それが導く型の定数を保持しないことに注意してください。 戻り値が引数の定数性または参照性を保持する必要がある関数を転送する場合は **、decltype(auto)** キーワードを使用できます。 **decltype** **decltype(auto) は**、左側の通常の戻り値として、または末尾の戻り値として使用できます。

次の例[(N3493](https://wg21.link/n3493)のコードに基づく) は、テンプレートがインスタンス化されるまで分からない戻り値の型で関数引数を完全に転送できるようにするために使用されている**decltype(auto)** を示しています。

```cpp
template<typename F, typename Tuple = tuple<T...>, int... I>
decltype(auto) apply_(F&& f, Tuple&& args, index_sequence<I...>)
{
    return std::forward<F>(f)(std::get<I>(std::forward<Tuple>(args))...);
}

template<typename F, typename Tuple = tuple<T...>,
    typename Indices = make_index_sequence<tuple_size<Tuple>::value >>
   decltype( auto)
    apply(F&& f, Tuple&& args)
{
    return apply_(std::forward<F>(f), std::forward<Tuple>(args), Indices());
}
```

## <a name="returning-multiple-values-from-a-function"></a><a name="multi_val"></a>関数から複数の値を返す

関数から複数の値を返す方法は、次のとおりです。

1. 名前付きクラスまたは構造体オブジェクトの値をカプセル化します。 クラスまたは構造体の定義を呼び出し元から参照できる必要があります。

    ```cpp
    #include <string>
    #include <iostream>

    using namespace std;

    struct S
    {
        string name;
        int num;
    };

    S g()
    {
        string t{ "hello" };
        int u{ 42 };
        return { t, u };
    }

    int main()
    {
        S s = g();
        cout << s.name << " " << s.num << endl;
        return 0;
    }
    ```

1. std::タプルまたは std::pair オブジェクトを返します。

    ```cpp
    #include <tuple>
    #include <string>
    #include <iostream>

    using namespace std;

    tuple<int, string, double> f()
    {
        int i{ 108 };
        string s{ "Some text" };
        double d{ .01 };
        return { i,s,d };
    }

    int main()
    {
        auto t = f();
        cout << get<0>(t) << " " << get<1>(t) << " " << get<2>(t) << endl;

        // --or--

        int myval;
        string myname;
        double mydecimal;
        tie(myval, myname, mydecimal) = f();
        cout << myval << " " << myname << " " << mydecimal << endl;

        return 0;
    }
    ```

1. **Visual Studio 2017 バージョン 15.3 以降** [(/std:c++17](../build/reference/std-specify-language-standard-version.md)で利用可能): 構造化バインディングを使用します。 構造化バインディングの利点は、戻り値を格納する変数が宣言されると同時に初期化されるため、場合によってはかなり効率的になる場合があります。 このステートメント --`auto[x, y, z] = f();`括弧は、関数ブロック全体のスコープ内にある名前を導入し、初期化します。

    ```cpp
    #include <tuple>
    #include <string>
    #include <iostream>

    using namespace std;

    tuple<int, string, double> f()
    {
        int i{ 108 };
        string s{ "Some text" };
        double d{ .01 };
        return { i,s,d };
    }
    struct S
    {
        string name;
        int num;
    };

    S g()
    {
        string t{ "hello" };
        int u{ 42 };
        return { t, u };
    }

    int main()
    {
        auto[x, y, z] = f(); // init from tuple
        cout << x << " " << y << " " << z << endl;

        auto[a, b] = g(); // init from POD struct
        cout << a << " " << b << endl;
        return 0;
    }
    ```

1. 戻り値自体を使用するだけでなく、関数が呼び出し元が提供するオブジェクトの値を変更または初期化できるように、参照渡しを使用するパラメーターをいくつでも定義することで、値を "戻す" ことができます。 詳細については、「[参照型関数の引数](reference-type-function-arguments.md)」を参照してください。

## <a name="function-pointers"></a>関数ポインター

C++ では、C 言語と同じ方法で、関数ポインターをサポートします。 ただし、通常、よりタイプ セーフな代替手段で関数オブジェクトが使用されます。

関数ポインター型を返す関数を宣言する場合は **、typedef**を使用して関数ポインター型の別名を宣言することをお勧めします。  次に例を示します。

```cpp
typedef int (*fp)(int);
fp myFunction(char* s); // function returning function pointer
```

このように記述していない場合でも、識別子 (上の例では `fp`) を関数名と引数リストで置き換えることで、関数ポインターの宣言構文から関数宣言の正しい構文を次のように導き出すことはできます。

```cpp
int (*myFunction(char* s))(int);
```

この宣言は、上記の typedef を使用した宣言と同等です。

## <a name="see-also"></a>関連項目

[関数のオーバーロード](../cpp/function-overloading.md)<br/>
[可変引数リストを持つ関数](../cpp/functions-with-variable-argument-lists-cpp.md)<br/>
[明示的に既定された関数および削除された関数](../cpp/explicitly-defaulted-and-deleted-functions.md)<br/>
[関数の引数依存名の参照 (Koenig 参照)](../cpp/argument-dependent-name-koenig-lookup-on-functions.md)<br/>
[既定の引数](../cpp/default-arguments.md)<br/>
[インライン関数](../cpp/inline-functions-cpp.md)
