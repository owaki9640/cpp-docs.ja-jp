---
title: _mbctohira、_mbctohira_l、_mbctokata、_mbctokata_l
ms.date: 4/2/2020
api_name:
- _mbctohira
- _mbctohira_l
- _mbctokata
- _mbctokata_l
- _o__mbctohira
- _o__mbctohira_l
- _o__mbctokata
- _o__mbctokata_l
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-multibyte-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _mbctokata
- mbctohira
- _mbctohira
- _mbctohira_l
- mbctokata
- mbctokata_l
- mbctohira_l
- _mbctokata_l
helpviewer_keywords:
- _mbctokata function
- _mbctokata_l function
- _mbctohira_l function
- mbctohira_l function
- mbctohira function
- mbctokata_l function
- _mbctohira function
- mbctokata function
ms.assetid: f949afd7-44d4-4f08-ac8f-1fef2c915a1c
ms.openlocfilehash: b5af94932fc90e6bcaee584e16f3056ee36dab51
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82914379"
---
# <a name="_mbctohira-_mbctohira_l-_mbctokata-_mbctokata_l"></a>_mbctohira、_mbctohira_l、_mbctokata、_mbctokata_l

ひらがなとカタカナの文字変換をします。

> [!IMPORTANT]
> この API は、Windows ランタイムで実行するアプリケーションでは使用できません。 詳細については、「[ユニバーサル Windows プラットフォーム アプリでサポートされていない CRT 関数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)」を参照してください。

## <a name="syntax"></a>構文

```C
unsigned int _mbctohira(
   unsigned int c
);
unsigned int _mbctohira_l(
   unsigned int c,
   _locale_t locale
);
unsigned int _mbctokata(
   unsigned int c
);
unsigned int _mbctokata_l(
   unsigned int c,
   _locale_t locale
);
```

### <a name="parameters"></a>パラメーター

*40u-c*<br/>
変換するマルチバイト文字。

*locale*<br/>
使用するロケール。

## <a name="return-value"></a>戻り値

これらの関数は、可能であれば、変換された文字*c*を返します。 それ以外の場合は、文字*c*を変更せずに返します。

## <a name="remarks"></a>解説

**_Mbctohira**関数と **_mbctokata**関数は*c*文字をテストし、可能であれば、次の変換のいずれか1つを適用します。

|ルーチン|変換|
|--------------|--------------|
|**_mbctohira**、 **_mbctohira_l**|マルチバイトのカタカナをマルチバイトのひらがなに変換します。|
|**_mbctokata**、 **_mbctokata_l**|マルチバイトのひらがなをマルチバイトのカタカナに変換します。|

出力値は、ロケールの **LC_CTYPE** カテゴリの設定に影響されます。詳細については、「[setlocale](setlocale-wsetlocale.md)」を参照してください。 これらの関数のバージョンは同じですが、 **_l**サフィックスが付いていないバージョンでは、このロケールに依存する動作に現在のロケールを使用し、 **_l**サフィックスが付いているものは、渡されたロケールパラメーターを代わりに使用する点が異なります。 詳細については、「 [Locale](../../c-runtime-library/locale.md)」を参照してください。

以前のバージョンでは、 **_mbctohira**に**jtohira**という名前が付けられ、 **_mbctokata**に**jtokata**という名前が付けられていました。 新しいコードには、新しい名前を使用してください。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|
|-------------|---------------------|
|**_mbctohira**|\<mbstring.h>|
|**_mbctohira_l**|\<mbstring.h>|
|**_mbctokata**|\<mbstring.h>|
|**_mbctokata_l**|\<mbstring.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="see-also"></a>関連項目

[データ変換](../../c-runtime-library/data-conversion.md)<br/>
[_mbcjistojms、_mbcjistojms_l、_mbcjmstojis、_mbcjmstojis_l](mbcjistojms-mbcjistojms-l-mbcjmstojis-mbcjmstojis-l.md)<br/>
[_mbctolower、_mbctolower_l、_mbctoupper、_mbctoupper_l](mbctolower-mbctolower-l-mbctoupper-mbctoupper-l.md)<br/>
[_mbctombb、_mbctombb_l](mbctombb-mbctombb-l.md)<br/>
