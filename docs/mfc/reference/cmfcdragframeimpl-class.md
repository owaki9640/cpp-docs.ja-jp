---
title: クラスをドラッグします。
ms.date: 10/18/2018
f1_keywords:
- CMFCDragFrameImpl
helpviewer_keywords:
- CMFCDragFrameImpl class [MFC]
ms.assetid: 500cd824-8188-43c2-8754-b7bb46b5648a
ms.openlocfilehash: 527fd089962e05c44a7e47b1ae52345116da4470
ms.sourcegitcommit: 7a6116e48c3c11b97371b8ae4ecc23adce1f092d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81752444"
---
# <a name="cmfcdragframeimpl-class"></a>クラスをドラッグします。

この`CMFCDragFrameImpl`クラスは、ユーザーが標準ドック モードでペインをドラッグしたときに表示されるドラッグ四角形を描画します。
詳細については、Visual Studio のインストールの**\\VC\\atlmfc\\src mfc**フォルダーにあるソース コードを参照してください。

## <a name="syntax"></a>構文

```
class CMFCDragFrameImpl
```

## <a name="remarks"></a>解説

このクラスのオブジェクトは、各[CPane クラス](../../mfc/reference/cpane-class.md)オブジェクトに埋め込まれます。 したがって、メソッドを使用する各`CanFloat`ペインは、ユーザーがドラッグしたときにドラッグ四角形を表示します。

ドラッグ長方形の厚みは[、AFX_GLOBAL_DATA::m_nDragFrameThicknessFloat](afx-global-data-structure.md#m_ndragframethicknessfloat)と[AFX_GLOBAL_DATA::m_nDragFrameThicknessDock](afx-global-data-structure.md#m_ndragframethicknessdock)を使用して制御できます。

## <a name="inheritance-hierarchy"></a>継承階層

[CMFCDragFrameImpl](../../mfc/reference/cmfcdragframeimpl-class.md)

## <a name="requirements"></a>必要条件

**ヘッダー:** afxdragframeimpl.h

## <a name="cmfcdragframeimplenddrawdragframe"></a><a name="enddrawdragframe"></a>CMFCドラッグフレームインプル::エンドドロードラッグフレーム

```cpp
void EndDrawDragFrame(BOOL bClearInternalRects = TRUE);
```

### <a name="parameters"></a>パラメーター

[in]*内部レクトをクリアする*<br/>

### <a name="remarks"></a>解説

## <a name="cmfcdragframeimplinit"></a><a name="init"></a>CMFCドラッグフレームインプル::イニト

```cpp
void Init(CWnd* pDraggedWnd);
```

### <a name="parameters"></a>パラメーター

[in]*プリドウンド*<br/>

### <a name="remarks"></a>解説

## <a name="cmfcdragframeimplmovedragframe"></a><a name="movedragframe"></a>CMFCドラッグフレームインプル::移動ドラッグフレーム

```cpp
void MoveDragFrame(BOOL bForceMove = FALSE);
```

### <a name="parameters"></a>パラメーター

[in]*を動かす*<br/>

### <a name="remarks"></a>解説

## <a name="cmfcdragframeimplplacetabpredocking"></a><a name="placetabpredocking"></a>CMFCドラッグフレームインプル::Pレースタブプレドッキング

```cpp
void PlaceTabPreDocking(
    CBaseTabbedPane* pTabbedBar,
    BOOL bFirstTime);

void PlaceTabPreDocking(CWnd* pCBarToPlaceOn);
```

### <a name="parameters"></a>パラメーター

[in]*pタブ付きバー*<br/>

[in]*bファーストタイム*<br/>

[in]*pCBarToプレープレイソン*<br/>

### <a name="remarks"></a>解説

## <a name="cmfcdragframeimplremovetabpredocking"></a><a name="removetabpredocking"></a>CMFCドラッグフレームインプル::タブプレドッキングの削除

```cpp
void RemoveTabPreDocking(CDockablePane* pOldTargetBar = NULL);
```

### <a name="parameters"></a>パラメーター

[in]*ターゲット バー*<br/>

### <a name="remarks"></a>解説

## <a name="cmfcdragframeimplresetstate"></a><a name="resetstate"></a>CMFCドラッグフレームインプル::リセットステート

```cpp
void ResetState();
```

### <a name="remarks"></a>解説

## <a name="see-also"></a>関連項目

[階層グラフ](../../mfc/hierarchy-chart.md)<br/>
[クラス](../../mfc/reference/mfc-classes.md)<br/>
[CPane Class](../../mfc/reference/cpane-class.md)
