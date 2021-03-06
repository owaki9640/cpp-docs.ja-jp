---
title: auto_handle クラス
ms.date: 01/16/2019
ms.topic: reference
f1_keywords:
- msclr::auto_handle::auto_handle
- msclr::auto_handle::get
- msclr::auto_handle::release
- msclr::auto_handle::reset
- msclr::auto_handle::swap
- msclr::auto_handle::operator->
- msclr::auto_handle::operator=
- msclr::auto_handle::operator auto_handle
- msclr::auto_handle::operator!
helpviewer_keywords:
- msclr::auto_handle class
ms.assetid: a65604d1-ecbb-44fd-ae2f-696ddeeed9d6
ms.openlocfilehash: 701669d1dbc6f3363f76c113dc98e38db04681a7
ms.sourcegitcommit: c123cc76bb2b6c5cde6f4c425ece420ac733bf70
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81372545"
---
# <a name="auto_handle-class"></a>auto_handle クラス

自動リソース管理を使用して、仮想ハンドルをマネージ型に埋め込むことができます。

## <a name="syntax"></a>構文

```cpp
template<typename _element_type>
ref class auto_handle;
```

### <a name="parameters"></a>パラメーター

*_element_type*<br/>
埋め込まれるマネージ型。

## <a name="members"></a><a name="members"></a>メンバー

### <a name="public-constructors"></a>パブリック コンストラクター  

|名前|説明|  
|---------|-----------|  
|[auto_handle::auto_handle](#auto-handle)|`auto_handle`コンストラクター。|  
|[auto_handle::~auto_handle](#tilde-auto-handle)|デス`auto_handle`トラクター。|  

### <a name="public-methods"></a>パブリック メソッド  

|名前|説明|  
|---------|-----------|  
|[auto_handle::get](#get)|格納されているオブジェクトを取得します。|  
|[auto_handle::release](#release)|オブジェクトを管理から`auto_handle`解放します。|
|[auto_handle::reset](#reset)|現在所有しているオブジェクトを破棄し、必要に応じて新しいオブジェクトを所有します。|
|[auto_handle::swap](#swap)|オブジェクトを別`auto_handle`の .|  

### <a name="public-operators"></a>公共事業者

|名前|説明|  
|---------|-----------|
|[auto_handle::オペレーター-&gt;](#operator-arrow)|メンバー アクセス演算子。|
|[auto_handle::operator=](#operator-assign)|代入演算子。|
|[auto_handle::operator auto_handle](#operator-auto-handle)|互換性のある型との`auto_handle`間の型キャスト演算子。|  
|[auto_handle::operator bool](#operator-bool)|条件式で`auto_handle`使用する演算子。|
|[auto_handle::オペレーター!](#operator-logical-not)|条件式で`auto_handle`使用する演算子。|  

## <a name="requirements"></a>必要条件

**ヘッダー ファイル**\<msclr\auto_handle.h>

**名前空間**msclr

## <a name="auto_handleauto_handle"></a><a name="auto-handle"></a>auto_handle::auto_handle

`auto_handle`コンストラクター。

```cpp
auto_handle();
auto_handle(
   _element_type ^ _ptr
);
auto_handle(
   auto_handle<_element_type> % _right
);
template<typename _other_type>
auto_handle(
   auto_handle<_other_type> % _right
);
```

### <a name="parameters"></a>パラメーター

*_ptr*<br/>
所有するオブジェクト。

*_right*<br/>
既存の `auto_handle`。

### <a name="example"></a>例

```cpp
// msl_auto_handle_auto_handle.cpp
// compile with: /clr
#include "msclr\auto_handle.h"

using namespace System;
using namespace msclr;
ref class RefClassA {
protected:
   String^ m_s;
public:
   RefClassA(String^ s) : m_s(s) {
      Console::WriteLine( "in RefClassA constructor: " + m_s );
   }
   ~RefClassA() {
      Console::WriteLine( "in RefClassA destructor: " + m_s );
   }

   virtual void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

ref class RefClassB : RefClassA {
public:
   RefClassB( String^ s ) : RefClassA( s ) {}
   virtual void PrintHello() new {
      Console::WriteLine( "Hello from {0} B!", m_s );
   }
};

int main()
{
   {
      auto_handle<RefClassA> a(gcnew RefClassA( "first" ) );
      a->PrintHello();
   }

   {
      auto_handle<RefClassB> b(gcnew RefClassB( "second" ) );
      b->PrintHello();
      auto_handle<RefClassA> a(b); //construct from derived type
      a->PrintHello();
      auto_handle<RefClassA> a2(a); //construct from same type
      a2->PrintHello();
   }

   Console::WriteLine("done");
}
```

```Output
in RefClassA constructor: first
Hello from first A!
in RefClassA destructor: first
in RefClassA constructor: second
Hello from second B!
Hello from second A!
Hello from second A!
in RefClassA destructor: second
done
```

## <a name="auto_handleauto_handle"></a><a name="tilde-auto-handle"></a>auto_handle::~auto_handle

デス`auto_handle`トラクター。

```cpp
~auto_handle();
```

### <a name="remarks"></a>解説

デストラクターも所有オブジェクトを破棄します。

### <a name="example"></a>例

```cpp
// msl_auto_handle_dtor.cpp
// compile with: /clr
#include "msclr\auto_handle.h"

using namespace System;
using namespace msclr;

ref class ClassA {
public:
   ClassA() { Console::WriteLine( "ClassA constructor" ); }
   ~ClassA() { Console::WriteLine( "ClassA destructor" ); }
};

int main()
{
   // create a new scope for a:
   {
      auto_handle<ClassA> a = gcnew ClassA;
   }
   // a goes out of scope here, invoking its destructor
   // which in turns destructs the ClassA object.

   Console::WriteLine( "done" );
}
```

```Output
ClassA constructor
ClassA destructor
done
```

## <a name="auto_handleget"></a><a name="get"></a>auto_handle::ゲット

格納されているオブジェクトを取得します。

```cpp
_element_type ^ get();
```

### <a name="return-value"></a>戻り値

格納されるオブジェクトです。

### <a name="example"></a>例

```cpp
// msl_auto_handle_get.cpp
// compile with: /clr
#include "msclr\auto_handle.h"

using namespace System;
using namespace msclr;

ref class ClassA {
   String^ m_s;
public:
   ClassA( String^ s ) : m_s( s ){
      Console::WriteLine( "in ClassA constructor:" + m_s );
   }
   ~ClassA() {
      Console::WriteLine( "in ClassA destructor:" + m_s );
   }

   void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

void PrintA( ClassA^ a ) {
   a->PrintHello();
}

int main() {
   auto_handle<ClassA> a = gcnew ClassA( "first" );
   a->PrintHello();

   ClassA^ a2 = a.get();
   a2->PrintHello();

   PrintA( a.get() );
}
```

```Output
in ClassA constructor:first
Hello from first A!
Hello from first A!
Hello from first A!
in ClassA destructor:first
```

## <a name="auto_handlerelease"></a><a name="release"></a>auto_handle::リリース

オブジェクトを管理から`auto_handle`解放します。

```cpp
_element_type ^ release();
```

### <a name="return-value"></a>戻り値

リリースされたオブジェクト。

### <a name="example"></a>例

```cpp
// msl_auto_handle_release.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

ref class ClassA {
   String^ m_s;
public:
   ClassA( String^ s ) : m_s( s ) {
      Console::WriteLine( "ClassA constructor: " + m_s );
   }
   ~ClassA() {
      Console::WriteLine( "ClassA destructor: " + m_s );
   }

   void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

int main()
{
   ClassA^ a;

   // create a new scope:
   {
      auto_handle<ClassA> agc1 = gcnew ClassA( "first" );
      auto_handle<ClassA> agc2 = gcnew ClassA( "second" );
      a = agc1.release();
   }
   // agc1 and agc2 go out of scope here

   a->PrintHello();

   Console::WriteLine( "done" );
}
```

```Output
ClassA constructor: first
ClassA constructor: second
ClassA destructor: second
Hello from first A!
done
```

## <a name="auto_handlereset"></a><a name="reset"></a>auto_handle::リセット

現在所有しているオブジェクトを破棄し、必要に応じて新しいオブジェクトを所有します。

```cpp
void reset(
   _element_type ^ _new_ptr
);
void reset();
```

### <a name="parameters"></a>パラメーター

*_new_ptr*<br/>
(オプション)新しいオブジェクト。

### <a name="example"></a>例

```cpp
// msl_auto_handle_reset.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

ref class ClassA {
   String^ m_s;
public:
   ClassA( String^ s ) : m_s( s ) {
      Console::WriteLine( "ClassA constructor: " + m_s );
   }
   ~ClassA() {
      Console::WriteLine( "ClassA destructor: " + m_s );
   }

   void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

int main()
{
   auto_handle<ClassA> agc1 = gcnew ClassA( "first" );
   agc1->PrintHello();

   ClassA^ ha = gcnew ClassA( "second" );
   agc1.reset( ha ); // release first object, reference second
   agc1->PrintHello();

   agc1.reset(); // release second object, set to nullptr

   Console::WriteLine( "done" );
}
```

```Output
ClassA constructor: first
Hello from first A!
ClassA constructor: second
ClassA destructor: first
Hello from second A!
ClassA destructor: second
done
```

## <a name="auto_handleswap"></a><a name="swap"></a>auto_handle::スワップ

オブジェクトを別`auto_handle`の .

```cpp
void swap(
   auto_handle<_element_type> % _right
);
```

### <a name="parameters"></a>パラメーター

*_right*<br/>
オブジェクト`auto_handle`を交換する対象。

### <a name="example"></a>例

```cpp
// msl_auto_handle_swap.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

int main() {
   auto_handle<String> s1 = "string one";
   auto_handle<String> s2 = "string two";

   Console::WriteLine( "s1 = '{0}', s2 = '{1}'",
      s1->ToString(), s2->ToString() );
   s1.swap( s2 );
   Console::WriteLine( "s1 = '{0}', s2 = '{1}'",
      s1->ToString(), s2->ToString() );
}
```

```Output
s1 = 'string one', s2 = 'string two'
s1 = 'string two', s2 = 'string one'
```

## <a name="auto_handleoperator-gt"></a><a name="operator-arrow"></a>auto_handle::オペレーター-&gt;

メンバー アクセス演算子。

```cpp
_element_type ^ operator->();
```

### <a name="return-value"></a>戻り値

で`auto_handle`ラップされるオブジェクト。

### <a name="example"></a>例

```cpp
// msl_auto_handle_op_arrow.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

ref class ClassA {
protected:
   String^ m_s;
public:
   ClassA( String^ s ) : m_s( s ) {}

   virtual void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }

   int m_i;
};

int main() {
   auto_handle<ClassA> a( gcnew ClassA( "first" ) );
   a->PrintHello();

   a->m_i = 5;
   Console::WriteLine( "a->m_i = {0}", a->m_i );
}
```

```Output
Hello from first A!
a->m_i = 5
```

## <a name="auto_handleoperator"></a><a name="operator-assign"></a>auto_handle:演算子=

代入演算子。

```cpp
auto_handle<_element_type> % operator=(
   auto_handle<_element_type> % _right
);
template<typename _other_type>
auto_handle<_element_type> % operator=(
   auto_handle<_other_type> % _right
);
```

### <a name="parameters"></a>パラメーター

*_right*<br/>
現在`auto_handle``auto_handle`の に割り当てられる 。

### <a name="return-value"></a>戻り値

現在`auto_handle`の 、 を`_right`所有しています。

### <a name="example"></a>例

```cpp
// msl_auto_handle_op_assign.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

ref class ClassA {
protected:
   String^ m_s;
public:
   ClassA(String^ s) : m_s(s) {
      Console::WriteLine( "in ClassA constructor: " + m_s );
   }
   ~ClassA() {
      Console::WriteLine( "in ClassA destructor: " + m_s );
   }

   virtual void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

ref class ClassB : ClassA {
public:
   ClassB( String^ s ) : ClassA( s ) {}
   virtual void PrintHello() new {
      Console::WriteLine( "Hello from {0} B!", m_s );
   }
};

int main()
{
   auto_handle<ClassA> a;
   auto_handle<ClassA> a2(gcnew ClassA( "first" ) );
   a = a2; // assign from same type
   a->PrintHello();

   auto_handle<ClassB> b(gcnew ClassB( "second" ) );
   b->PrintHello();
   a = b; // assign from derived type
   a->PrintHello();

   Console::WriteLine("done");
}
```

```Output
in ClassA constructor: first
Hello from first A!
in ClassA constructor: second
Hello from second B!
in ClassA destructor: first
Hello from second A!
done
in ClassA destructor: second
```

## <a name="auto_handleoperator-auto_handle"></a><a name="operator-auto-handle"></a>auto_handle::オペレーターauto_handle

互換性のある型との`auto_handle`間の型キャスト演算子。

```cpp
template<typename _other_type>
operator auto_handle<_other_type>();
```

### <a name="return-value"></a>戻り値

現在`auto_handle`のキャストは`auto_handle<_other_type>`にキャストされます。

### <a name="example"></a>例

```cpp
// msl_auto_handle_op_auto_handle.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

ref class ClassA {
protected:
   String^ m_s;
public:
   ClassA( String^ s ) : m_s( s ) {}

   virtual void PrintHello() {
      Console::WriteLine( "Hello from {0} A!", m_s );
   }
};

ref class ClassB : ClassA {
public:
   ClassB( String ^ s) : ClassA( s ) {}
   virtual void PrintHello() new {
      Console::WriteLine( "Hello from {0} B!", m_s );
   }
};

int main() {
   auto_handle<ClassB> b = gcnew ClassB("first");
   b->PrintHello();
   auto_handle<ClassA> a = (auto_handle<ClassA>)b;
   a->PrintHello();
}
```

```Output
Hello from first B!
Hello from first A!
```

## <a name="auto_handleoperator-bool"></a><a name="operator-bool"></a>auto_handle::オペレーターブール

条件式で`auto_handle`使用する演算子。

```cpp
operator bool();
```

### <a name="return-value"></a>戻り値

`true`ラップされたオブジェクトが有効な場合。`false`それ以外の場合。

### <a name="remarks"></a>解説

この演算子は、整数型`_detail_class::_safe_bool`に変換できないため、`bool`実際に変換する方が安全です。

### <a name="example"></a>例

```cpp
// msl_auto_handle_operator_bool.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

int main() {
   auto_handle<String> s1;
   auto_handle<String> s2 = "hi";
   if ( s1 ) Console::WriteLine( "s1 is valid" );
   if ( !s1 ) Console::WriteLine( "s1 is invalid" );
   if ( s2 ) Console::WriteLine( "s2 is valid" );
   if ( !s2 ) Console::WriteLine( "s2 is invalid" );
   s2.reset();
   if ( s2 ) Console::WriteLine( "s2 is now valid" );
   if ( !s2 ) Console::WriteLine( "s2 is now invalid" );
}
```

```Output
s1 is invalid
s2 is valid
s2 is now invalid
```

## <a name="auto_handleoperator"></a><a name="operator-logical-not"></a>auto_handle::オペレーター!

条件式で`auto_handle`使用する演算子。

```cpp
bool operator!();
```

### <a name="return-value"></a>戻り値

`true`ラップされたオブジェクトが無効な場合。`false`それ以外の場合。

### <a name="example"></a>例

```cpp
// msl_auto_handle_operator_not.cpp
// compile with: /clr
#include <msclr\auto_handle.h>

using namespace System;
using namespace msclr;

int main() {
   auto_handle<String> s1;
   auto_handle<String> s2 = "something";
   if ( s1) Console::WriteLine( "s1 is valid" );
   if ( !s1 ) Console::WriteLine( "s1 is invalid" );
   if ( s2 ) Console::WriteLine( "s2 is valid" );
   if ( !s2 ) Console::WriteLine( "s2 is invalid" );
   s2.reset();
   if ( s2 ) Console::WriteLine( "s2 is now valid" );
   if ( !s2 ) Console::WriteLine( "s2 is now invalid" );
}
```

```Output
s1 is invalid
s2 is valid
s2 is now invalid
```
