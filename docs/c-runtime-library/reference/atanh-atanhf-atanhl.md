---
title: atanh、atanhf、atanhl
ms.date: 4/2/2020
api_name:
- atanhl
- atanhf
- atanh
- _o_atanh
- _o_atanhf
- _o_atanhl
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
- api-ms-win-crt-math-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- atanhl
- atanhf
- atanh
helpviewer_keywords:
- atanhf function
- atanhl function
- atanh funciton
ms.assetid: 83a43b5b-2580-4461-854f-dc84236d9f32
ms.openlocfilehash: ce40cf25fde12c6413e88519906b807f2ee65faa
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82920064"
---
# <a name="atanh-atanhf-atanhl"></a>atanh、atanhf、atanhl

逆ハイパーボリック タンジェントを計算します。

## <a name="syntax"></a>構文

```C
double atanh( double x );
float atanhf( float x );
long double atanhl( long double x );
```

```cpp
float atanh( float x );  // C++ only
long double atanh( long double x );  // C++ only
```

### <a name="parameters"></a>パラメーター

*x*<br/>
浮動小数点値。

## <a name="return-value"></a>戻り値

**Atanh**関数は、 *x*の逆ハイパーボリックタンジェント (アークハイパーボリックタンジェント) を返します。 *X*が1より大きいか、または-1 未満の場合、 **errno**は**EDOM**に設定され、結果は簡易な NaN になります。 *X*が1または-1 の場合、それぞれ正または負の無限大が返され、 **errno**は**ERANGE**に設定されます。

|入力|SEH 例外|**Matherr**例外的|
|-----------|-------------------|-------------------------|
|± QNAN、IND|なし|なし|
|*X* ≥ 1;*x* ≤-1|なし|なし|

## <a name="remarks"></a>解説

C++ ではオーバーロードが可能であるため、 **float 型**または**long** **double**型の値を受け取って返す**atanh**のオーバーロードを呼び出すことができます。 C プログラムでは、 **atanh**は常にを受け取り、 **double**を返します。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

## <a name="requirements"></a>必要条件

|関数|C ヘッダー|C++ ヘッダー|
|--------------|--------------|------------------|
|**atanh**、 **atanhf**、 **atanhl**|\<math.h>|\<cmath> または \<math.h>|

互換性の詳細については、「[互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="example"></a>例

```C
// crt_atanh.c
// This program displays the hyperbolic tangent of pi / 4
// and the arc hyperbolic tangent of the result.
//

#include <math.h>
#include <stdio.h>

int main( void )
{
   double pi = 3.1415926535;
   double x, y;

   x = tanh( pi / 4 );
   y = atanh( x );
   printf( "tanh( %f ) = %f\n", pi/4, x );
   printf( "atanh( %f ) = %f\n", x, y );
}
```

```Output
tanh( 0.785398 ) = 0.655794
atanh( 0.655794 ) = 0.785398
```

## <a name="see-also"></a>関連項目

[浮動小数点サポート](../../c-runtime-library/floating-point-support.md)<br/>
[acosh、acoshf、acoshl](acosh-acoshf-acoshl.md)<br/>
[asinh、asinhf、asinhl](asinh-asinhf-asinhl.md)<br/>
[cosh、coshf、coshl](cosh-coshf-coshl.md)<br/>
[sinh、sinhf、sinhl](sinh-sinhf-sinhl.md)<br/>
[tanh、tanhf、tanhl](tanh-tanhf-tanhl.md)<br/>
