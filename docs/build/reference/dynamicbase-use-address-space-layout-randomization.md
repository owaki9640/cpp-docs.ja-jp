---
title: /DYNAMICBASE (ASLR (Address Space Layout Randomization) の使用)
ms.date: 06/12/2018
f1_keywords:
- VC.Project.VCLinkerTool.RandomizedBaseAddress
helpviewer_keywords:
- -DYNAMICBASE linker option
- /DYNAMICBASE linker option
- DYNAMICBASE linker option
ms.assetid: 6c0ced8e-fe9c-4b63-b956-eb8a55fbceb2
ms.openlocfilehash: 66d6232ed43f9c842ebbb0e22b57c509cf610afa
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80170060"
---
# <a name="dynamicbase-use-address-space-layout-randomization"></a>/DYNAMICBASE (ASLR (Address Space Layout Randomization) の使用)

読み込み時にランダムに再配置できる実行可能イメージを生成するかどうかを指定します。これは、Windows Vista で初めて利用可能になった Windows のアドレス空間レイアウトランダム化 (ASLR) 機能を使用して行います。

## <a name="syntax"></a>構文

> **/DYNAMICBASE** **[: NO]**

## <a name="remarks"></a>解説

**/DYNAMICBASE**オプションは、*実行可能イメージ*(.dll または .exe ファイル) のヘッダーを変更して、読み込み時にアプリケーションをランダムに再配置する必要があるかどうかを示し、仮想アドレス割り当てのランダム化を有効にします。これは、ヒープ、スタック、およびその他のオペレーティングシステムの割り当ての仮想メモリ位置に影響します。 **/DYNAMICBASE**オプションは、32ビットイメージと64ビットイメージの両方に適用されます。 ASLR は、Windows Vista 以降のオペレーティングシステムでサポートされています。 このオプションは、以前のオペレーティングシステムでは無視されます。

既定では、 **/DYNAMICBASE**は有効になっています。 このオプションを無効にするには、 **/DYNAMICBASE: NO**を使用します。 [/HIGHENTROPYVA](highentropyva-support-64-bit-aslr.md)オプションが効果を持つようにするには、 **/DYNAMICBASE**オプションを指定する必要があります。

### <a name="to-set-this-linker-option-in-visual-studio"></a>このリンカー オプションを Visual Studio で設定するには

1. プロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 詳しくは、「[Visual Studio で C++ コンパイラとビルド プロパティを設定する](../working-with-project-properties.md)」をご覧ください。

1. **[構成プロパティ]**  > [**リンカー** > **詳細設定**] プロパティページを選択します。

1. ランダム化された**ベースアドレス**プロパティを変更します。

### <a name="to-set-this-linker-option-programmatically"></a>このリンカーをコードから設定するには

- [https://docs.microsoft.com/azure/active-directory/develop/scenario-protected-web-api-overview](<xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.RandomizedBaseAddress%2A>) をご覧ください。

## <a name="see-also"></a>参照

- [MSVC リンカーのリファレンス](linking.md)
- [MSVC リンカー オプション](linker-options.md)
- [/HIGHENTROPYVA](highentropyva-support-64-bit-aslr.md)
- [Windows ISV ソフトウェアセキュリティ防御](https://msdn.microsoft.com/library/bb430720.aspx)
