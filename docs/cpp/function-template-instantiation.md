---
title: 関数テンプレートのインスタンス化
ms.date: 11/04/2016
helpviewer_keywords:
- templates, instantiation
- function templates, instantiation
- instantiation, function templates
ms.assetid: f22a07c7-3ad1-465a-84f5-8737e274bd47
ms.openlocfilehash: 6917448af067542fffb13aa043720bf8a26f7ba3
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80179758"
---
# <a name="function-template-instantiation"></a>関数テンプレートのインスタンス化

関数テンプレートが各型に対して最初に呼び出されるときに、コンパイラはインスタンス化を作成します。 各インスタンス化は、型に特殊化したテンプレート関数の 1 つのバージョンです。 このインスタンス化は、関数がこの型に対して使用されるたびに呼び出されます。 複数の同一のインスタンス化が存在する場合、それらが存在するのが別々のモジュール内であっても、実行可能ファイルには、1 つのインスタンス化のコピーのみが含まれます。

関数テンプレートでは、引数とパラメーターの任意のペアについて、そのパラメーターがテンプレート引数に依存しない場合、関数の引数の変換が許可されます。

関数テンプレートは、特定の型を引数として使用してテンプレートを宣言することで、明示的にインスタンス化できます。 たとえば、次のようなコードを記述できます。

```cpp
// function_template_instantiation.cpp
template<class T> void f(T) { }

// Instantiate f with the explicitly specified template.
// argument 'int'
//
template void f<int> (int);

// Instantiate f with the deduced template argument 'char'.
template void f(char);
int main()
{
}
```

## <a name="see-also"></a>参照

[関数テンプレート](../cpp/function-templates.md)
