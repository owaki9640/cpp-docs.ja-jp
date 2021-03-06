---
title: ツール バー コントロールの外観のカスタマイズ
ms.date: 11/04/2016
f1_keywords:
- TBSTYLE_
helpviewer_keywords:
- flat toolbars
- CToolBar class [MFC], styles
- transparent toolbars
- TBSTYLE_ styles [MFC]
- CToolBarCtrl class [MFC], object styles
- toolbar controls [MFC], style
ms.assetid: fd0a73db-7ad1-4fe4-889b-02c3980f49e8
ms.openlocfilehash: ddccb5f05152d95377b430d7492ede3c86926e37
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84619283"
---
# <a name="customizing-the-appearance-of-a-toolbar-control"></a>ツール バー コントロールの外観のカスタマイズ

クラスに `CToolBarCtrl` は、ツールバーオブジェクトの外観 (および場合によっては動作) に影響するさまざまなスタイルが用意されています。 ツールバー `dwCtrlStyle` `CToolBarCtrl::Create` コントロールを最初に作成するときに、(または) メンバー関数のパラメーターを設定して、ツールバーオブジェクトを変更し `CToolBar::CreateEx` ます。

次のスタイルは、ツールバーボタンの "3D" の側面とボタンテキストの配置に影響します。

- **TBSTYLE_FLAT**ツールバーとボタンの両方が透明であるフラットなツールバーを作成します。 ボタンのテキストはボタンのビットマップの下に表示されます。 このスタイルを使用すると、カーソルの下にあるボタンが自動的に強調表示されます。

- **TBSTYLE_TRANSPARENT**透明なツールバーを作成します。 透過的なツールバーでは、ツールバーは透明ですが、ボタンは透明になっていません。 ボタンのテキストはボタンのビットマップの下に表示されます。

- **TBSTYLE_LIST**ボタンのビットマップの右側にボタンのテキストを配置します。

> [!NOTE]
> 再描画の問題を防ぐには、ツールバーオブジェクトを表示する前に、 **TBSTYLE_FLAT**スタイルと**TBSTYLE_TRANSPARENT**スタイルを設定する必要があります。

次のスタイルでは、ツールバーでドラッグアンドドロップを使用して、ツールバーオブジェクト内の個々のボタンの位置を変更できるかどうかを判断します。

- **TBSTYLE_ALTDRAG**ALT キーを押しながらドラッグして、ツールバーボタンの位置を変更できるようにします。 このスタイルが指定されていない場合、ユーザーはボタンをドラッグしている間、SHIFT キーを押したままにする必要があります。

    > [!NOTE]
    >  ツールバーボタンをドラッグできるようにするには、 **CCS_ADJUSTABLE**スタイルを指定する必要があります。

- **TBSTYLE_REGISTERDROP**マウスポインターがツールバーボタンの上に置かれたときにドロップ先オブジェクトを要求するために**TBN_GETOBJECT**通知メッセージを生成します。

残りのスタイルは、ツールバーオブジェクトのビジュアルおよび非表示の側面に影響します。

- **TBSTYLE_WRAPABLE**複数行のボタンを持つことができるツールバーを作成します。 ツールバーのボタンが狭すぎて同じ行にすべてのボタンを含めることができなくなると、ツールバーのボタンが次の行に折り返されることがあります。 ラップは、分離とグループ外の境界に対して行われます。

- **TBSTYLE_CUSTOMERASE****WM_ERASEBKGND**メッセージを処理するときに、 **NM_CUSTOMDRAW**通知メッセージを生成します。

- **TBSTYLE_TOOLTIPS**ツールバーのボタンの説明テキストを表示するためにアプリケーションで使用できるツールヒントコントロールを作成します。

ツールバーのスタイルと拡張スタイルの完全な一覧については、「[ツールバーコントロールとボタンのスタイル](/windows/win32/Controls/toolbar-control-and-button-styles)」および「[ツールバーの拡張スタイル](/windows/win32/Controls/toolbar-extended-styles)(Windows SDK)」を参照してください。

## <a name="see-also"></a>関連項目

[CToolBarCtrl の使い方](using-ctoolbarctrl.md)<br/>
[制限](controls-mfc.md)
