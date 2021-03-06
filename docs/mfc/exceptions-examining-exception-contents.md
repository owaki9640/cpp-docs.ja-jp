---
title: '例外処理 : 例外の内容の調査'
ms.date: 11/04/2016
helpviewer_keywords:
- exception handling [MFC], MFC
- try-catch exception handling [MFC], MFC function exceptions
- catch blocks, MFC function exceptions
- CException class [MFC], class exceptions
- try-catch exception handling [MFC], exception contents
- throwing exceptions [MFC], exception contents
ms.assetid: dfda4782-b969-4f60-b867-cc204ea7f33a
ms.openlocfilehash: 8554dda2f465aa058cea3d257c22ec38bc6e2c18
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84625902"
---
# <a name="exceptions-examining-exception-contents"></a>例外処理 : 例外の内容の調査

**Catch**ブロックの引数はほぼすべてのデータ型にすることができますが、MFC 関数はクラスから派生した型の例外をスローし `CException` ます。 MFC 関数によってスローされた例外をキャッチするには**catch** 、引数が `CException` オブジェクト (またはから派生したオブジェクト) へのポインターである catch ブロックを記述し `CException` `CMemoryException` ます。 例外の正確な型によっては、例外オブジェクトのデータメンバーを調べて、例外の特定の原因に関する情報を収集できます。

たとえば、型に `CFileException` は、 `m_cause` ファイルの例外の原因を指定する列挙型を含むデータメンバーがあります。 返される戻り値の例とし `CFileException::fileNotFound` ては、とがあり `CFileException::readOnly` ます。

次の例は、の内容を確認する方法を示して `CFileException` います。 他の種類の例外は同様に調べることができます。

[!code-cpp[NVC_MFCExceptions#13](codesnippet/cpp/exceptions-examining-exception-contents_1.cpp)]

詳細については、「例外[: 例外の解放」](exceptions-freeing-objects-in-exceptions.md)と「例外」を参照してください。例外の[キャッチと削除](exceptions-catching-and-deleting-exceptions.md)。

## <a name="see-also"></a>関連項目

[例外処理](exception-handling-in-mfc.md)
