---
title: コンパイラの警告 (レベル 1) C4183
ms.date: 11/04/2016
f1_keywords:
- C4183
helpviewer_keywords:
- C4183
ms.assetid: dc48312c-4b34-44dd-80ff-eb5f11d5ca47
ms.openlocfilehash: 4c2c7ce23cfaea5ebf31e78d84b7ff7fbdbf4c85
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80175936"
---
# <a name="compiler-warning-level-1-c4183"></a>コンパイラの警告 (レベル 1) C4183

' identifier ': 戻り値の型がありません。' int ' を返すメンバー関数であると想定されます

クラスまたは構造体のメンバー関数のインライン定義に戻り値の型がありません。 このメンバー関数は、`int`の既定の戻り値の型を持つと見なされます。

次の例では、C4183 が生成されます。

```cpp
// C4183.cpp
// compile with: /W1 /c
#pragma warning(disable : 4430)
class MyClass1;
class MyClass2 {
   MyClass1() {};   // C4183
};
```
