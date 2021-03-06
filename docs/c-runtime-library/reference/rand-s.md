---
title: rand_s
ms.date: 4/2/2020
api_name:
- rand_s
- _o_rand_s
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
- api-ms-win-crt-utility-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- rand_s
helpviewer_keywords:
- generating pseudorandom numbers
- random numbers, cryptographically secure
- random numbers, generating
- rand_s function
- numbers, pseudorandom
- cryptographically secure random numbers
- pseudorandom numbers
- numbers, generating pseudorandom
ms.openlocfilehash: cad1740e64c7bbda553ac1a6c777d7e2295152ba
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82919539"
---
# <a name="rand_s"></a>rand_s

疑似乱数を生成します。 これは、「 [CRT のセキュリティ機能](../../c-runtime-library/security-features-in-the-crt.md)」の説明にあるとおり、セキュリティが強化された、関数[rand](rand.md)のより安全なバージョンです。

## <a name="syntax"></a>構文

```C
errno_t rand_s(unsigned int* randomValue);
```

### <a name="parameters"></a>パラメーター

*randomValue*<br/>
生成された値を保持する整数へのポインター。

## <a name="return-value"></a>戻り値

正常に終了した場合は 0 を返し、それ以外の場合はエラー コードを返します。 入力ポインター _randomValue_が null ポインターの場合、この関数は、「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、無効なパラメーターハンドラーを呼び出します。 実行の継続が許可された場合、関数は**einval**を返し、 **errno**を**einval**に設定します。 他の何らかの理由で関数が失敗した場合、*_randomValue_は0に設定されます。

## <a name="remarks"></a>解説

**Rand_s**関数は、0の範囲のランダムな整数を書き込み、入力ポインターに**UINT_MAX**します。 **Rand_s**関数は、オペレーティングシステムを使用して、暗号的に保護されたランダムな数値を生成します。 [Srand](srand.md)関数によって生成されたシードは使用されません。また、 [rand](rand.md)で使用される乱数シーケンスにも影響しません。

**Rand_s**関数を使用するには、次の例のように、関数を宣言するために、include ステートメントの前に定数 **_CRT_RAND_S**定義する必要があります。

```C
By default, this function's global state is scoped to the application. To change this, see [Global state in the CRT](../global-state.md).

#define _CRT_RAND_S
#include <stdlib.h>
```

**rand_s**は、Windows XP 以降でのみ使用できる[Rtlgenrandom](/windows/win32/api/ntsecapi/nf-ntsecapi-rtlgenrandom) API に依存しています。

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|
|-------------|---------------------|
|**rand_s**|\<stdlib.h>|

詳細については、「 [互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="example"></a>例

```C
// crt_rand_s.c
// This program illustrates how to generate random
// integer or floating point numbers in a specified range.

// Remembering to define _CRT_RAND_S prior
// to inclusion statement.
#define _CRT_RAND_S

#include <stdlib.h>
#include <stdio.h>
#include <limits.h>

int main( void )
{
    int             i;
    unsigned int    number;
    double          max = 100.0;
    errno_t         err;

    // Display 10 random integers in the range [ 1,10 ].
    for( i = 0; i < 10;i++ )
    {
        err = rand_s( &number );
        if (err != 0)
        {
            printf_s("The rand_s function failed!\n");
        }
        printf_s( "  %u\n", (unsigned int) ((double)number /
                       ((double) UINT_MAX + 1 ) * 10.0) + 1);
    }

    printf_s("\n");

    // Display 10 random doubles in [0, max).
    for (i = 0; i < 10;i++ )
    {
        err = rand_s( &number );
        if (err != 0)
        {
            printf_s("The rand_s function failed!\n");
        }
        printf_s( "  %g\n", (double) number /
                          ((double) UINT_MAX + 1) * max );
    }
}
```

### <a name="sample-output"></a>サンプル出力

```Output
10
4
5
2
8
2
5
6
1
1

32.6617
29.4471
11.5413
6.41924
20.711
60.2878
61.0094
20.1222
80.9192
65.0712
```

## <a name="see-also"></a>関連項目

[浮動小数点サポート](../../c-runtime-library/floating-point-support.md)<br/>
[rand](rand.md)<br/>
[srand](srand.md)<br/>
