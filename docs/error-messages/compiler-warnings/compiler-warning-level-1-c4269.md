---
title: コンパイラの警告 (レベル 1) C4269
ms.date: 11/04/2016
f1_keywords:
- C4269
helpviewer_keywords:
- C4269
ms.assetid: 96c97bbc-068a-4b65-8cd8-4ed5dca04c15
ms.openlocfilehash: e2e1781bf4c1b9ac0ee29d0b5900daa6cfe94b45
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80199772"
---
# <a name="compiler-warning-level-1-c4269"></a>コンパイラの警告 (レベル 1) C4269

' identifier ': コンパイラが生成した既定のコンストラクターで ' const ' 自動データが初期化されました。信頼性の低い結果が生成されます

自明でないクラスの**定数**自動インスタンスは、コンパイラによって生成される既定のコンストラクターで初期化されます。

## <a name="example"></a>例

```cpp
// C4269.cpp
// compile with: /c /LD /W1
class X {
public:
   int m_data;
};

void g() {
   const X x1;   // C4269
};
```

クラスのこのインスタンスはスタック上で生成されるため、`m_data` の初期値は任意です。 また、 **const**インスタンスであるため、`m_data` の値を変更することはできません。
