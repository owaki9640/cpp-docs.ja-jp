---
title: DeferrableEventArgs クラス
ms.date: 10/03/2018
ms.topic: reference
f1_keywords:
- event/Microsoft::WRL::DeferrableEventArgs
- event/Microsoft::WRL::DeferrableEventArgs::GetDeferral
- event/Microsoft::WRL::DeferrableEventArgs::InvokeAllFinished
helpviewer_keywords:
- Microsoft::WRL::DeferrableEventArgs class
- Microsoft::WRL::DeferrableEventArgs::GetDeferral method
- Microsoft::WRL::DeferrableEventArgs::InvokeAllFinished method
ms.assetid: ece89267-7b72-40e1-8185-550c865b070a
ms.openlocfilehash: 066918bf2c76b17f06871ee08be674be9b36c161
ms.sourcegitcommit: 89d9e1cb08fa872483d1cde98bc2a7c870e505e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82032461"
---
# <a name="deferrableeventargs-class"></a>DeferrableEventArgs クラス

遅延のイベント引数の型に使用されるテンプレート クラス。

## <a name="syntax"></a>構文

```cpp
template <typename TEventArgsInterface, typename TEventArgsClass>
class DeferrableEventArgs : public TEventArgsInterface;
```

### <a name="parameters"></a>パラメーター

*インターフェイス*<br/>
遅延イベントの引数を宣言するインターフェイスの型。

*イベントクラス*<br/>
インターフェイスを実装*する*クラス。

## <a name="members"></a>メンバー

### <a name="public-methods"></a>パブリック メソッド

| 名前 | 説明 |
|--|--|
| [デフェラルイベント引数::GetDeferral](#getdeferral) | 遅延イベントを表す[Deferral](/uwp/api/windows.foundation.deferral)オブジェクトへの参照を取得します。 |
| [デフェランブルイベント引数::呼び出しオールフィニッシュ](#invokeallfinished) | 遅延イベントを処理するすべての処理が完了したことを示すために呼び出されます。 |

## <a name="remarks"></a>解説

このクラスのインスタンスは、遅延イベントのイベント ハンドラーに渡されます。 テンプレート パラメーターは、遅延イベントの特定の種類のイベント引数の詳細を定義するインターフェイスと、そのインターフェイスを実装するクラスを表します。

クラスは遅延イベントのイベント ハンドラーの最初の引数として表示されます。 [GetDeferral](#getdeferral)メソッドを呼び出して[、遅延](/uwp/api/windows.foundation.deferral)イベントに関するすべての情報を取得できる保留オブジェクトを取得できます。 イベント処理を完了した後、遅延オブジェクトで Complete を呼び出す必要があります。 次に、イベント ハンドラー メソッドの最後に[InvokeAllFinished](#invokeallfinished)を呼び出す必要があります。

## <a name="requirements"></a>必要条件

**ヘッダー:** イベント.h

**名前空間:** Microsoft::WRL

## <a name="deferrableeventargsgetdeferral"></a><a name="getdeferral"></a>デフェラルイベント引数::GetDeferral

遅延イベントを表す[Deferral](/uwp/api/windows.foundation.deferral)オブジェクトへの参照を取得します。

```cpp
HRESULT GetDeferral([out, retval] Windows::Foundation::IDeferral** result)
```

### <a name="parameters"></a>パラメーター

*result*<br/>
呼び出しが完了したときに[Deferral](/uwp/api/windows.foundation.deferral)オブジェクトを参照するポインター。

### <a name="return-value"></a>戻り値

成功した場合は S_OK、そうでない場合はエラーを示す HRESULT。

## <a name="deferrableeventargsinvokeallfinished"></a><a name="invokeallfinished"></a>デフェランブルイベント引数::呼び出しオールフィニッシュ

遅延イベントを処理するすべての処理が完了したことを示すために呼び出されます。

```cpp
void InvokeAllFinished()
```

### <a name="remarks"></a>解説

イベント ソースが[InvokeAll](eventsource-class.md#invokeall)を呼び出した後、このメソッドを呼び出す必要があります。 このメソッドを呼び出すことで、さらに遅延が取られることを回避し、遅延が取られなかった場合は、完了ハンドラーの実行を強制します。
