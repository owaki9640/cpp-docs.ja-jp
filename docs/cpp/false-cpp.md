---
title: false (C++)
ms.date: 11/04/2016
f1_keywords:
- false_cpp
helpviewer_keywords:
- false keyword [C++]
ms.assetid: cc13aec5-1f02-4d38-8dbf-5473ea2b354f
ms.openlocfilehash: f363e309b91e44472447d040aa36752750afec6f
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80188936"
---
# <a name="false-c"></a>false (C++)

キーワードは、 [bool](../cpp/bool-cpp.md)型の変数または条件式の2つの値のいずれかです (条件式は、**真**のブール式になります)。 たとえば、`i` が**bool**型の変数である場合、`i = false;` ステートメントは `i`に**false**を割り当てます。

## <a name="example"></a>例

```cpp
// bool_false.cpp
#include <stdio.h>

int main()
{
    bool bb = true;
    printf_s("%d\n", bb);
    bb = false;
    printf_s("%d\n", bb);
}
```

```Output
1
0
```

## <a name="see-also"></a>参照

[キーワード](../cpp/keywords-cpp.md)
