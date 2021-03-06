---
title: 変換フェーズ
ms.date: 08/29/2019
helpviewer_keywords:
- translation phases
- preprocessor, translation
- translation, compiler process
- preprocessor
- file translation [C++], compiler process
- files [C++], translation
ms.assetid: a7f7a8c9-e8ba-4321-9e50-ebfbbdcce9db
ms.openlocfilehash: d072c9aec48d815ba85f8a12576baa6447703f8c
ms.sourcegitcommit: 6e1c1822e7bcf3d2ef23eb8fac6465f88743facf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70218309"
---
# <a name="phases-of-translation"></a>変換フェーズ

C および C++ プログラムは、それぞれがプログラムのテキストの一部を含む 1 つ以上のソース ファイルで構成されます。 ソースファイルとその*インクルードファイル*、 `#include`プリプロセッサディレクティブを使用してインクルードされたファイル、など`#if`の条件付きコンパイルディレクティブによって削除されたコードセクションは*含まれません。翻訳単位*。

ソースファイルは、異なるタイミングで変換できます。 実際には、古いファイルのみを変換するのが一般的です。 変換された翻訳単位は個別のオブジェクト ファイルまたはオブジェクト コード ライブラリに処理できます。 次に、変換された各翻訳単位は、実行可能プログラムやダイナミック リンク ライブラリ (DLL) を形成するためにリンクされます。 リンカーへの入力として使用できるファイルの詳細については、「 [LINK input files](../build/reference/link-input-files.md)」を参照してください。

翻訳単位は次を使用して通信できます。

- 外部リンケージを持つ関数の呼び出し。

- 外部リンケージを持つクラス メンバー関数の呼び出し。

- 外部リンケージを持つオブジェクトの直接的な変更。

- ファイルの直接的な変更。

- プロセス間通信 (Microsoft Windows ベースのアプリケーションのみ)。

次の一覧では、コンパイラがファイルを変換するフェーズについて説明します。

*文字のマッピング*\
ソース ファイルの文字はソースの内部表現にマップされます。 トライグラフ シーケンスはこのフェーズの単一文字の内部表現に変換されます。

*ラインスプライス*\
円記号 ( **\\** ) で終わるすべての行の直後に改行文字が続くと、ソースファイルの次の行と結合され、物理的な行から論理行が形成されます。 空でない場合、ソースファイルは、円記号ではなく改行文字で終わる必要があります。

*分割*\
ソース ファイルはプリプロセッサ トークンと空白文字に分割されます。 ソース ファイル内のコメントは、それぞれ 1 個の空白文字と置き換えられます。 改行文字は保持されます。

*前処理*\
前処理ディレクティブが実行され、マクロがソース ファイルに展開されます。 `#include` ステートメントは、インクルードされたテキストで前の 3 つの書き換え手順から開始する変換を呼び出します。

*文字セットのマッピング*\
すべてのソース文字セット メンバーとエスケープ シーケンスは、実行文字セットの同等のものに変換されます。 Microsoft C および C++ にとって、ソース文字セットと実行文字セットはいずれも ASCII 文字セットです。

*文字列の連結*\
すべての隣接する文字列とワイド文字列リテラルは連結されます。 たとえば、`"String " "concatenation"` が `"String concatenation"` になります。

*変換*\
すべてのトークンは、構文的および意味的に分析され、オブジェクト コードに変換されます。

*シー*\
すべての外部参照は実行可能プログラムまたはダイナミック リンク ライブラリを作成するために解決されます。

コンパイラは、構文エラーを検出した変換のフェーズ中に警告やエラーを発行します。

リンカーは、すべての外部参照を解決し、1 つ以上の個別に処理された翻訳単位を結合して、標準ライブラリと共に実行可能プログラムまたは DLL を作成します。

## <a name="see-also"></a>関連項目

[プリプロセッサ](../preprocessor/preprocessor.md)
