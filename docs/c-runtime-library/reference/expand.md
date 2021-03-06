---
title: _expand
ms.date: 4/2/2020
api_name:
- _expand
- _o__expand
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
- api-ms-win-crt-heap-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _bexpand
- fexpand
- expand
- nexpand
- _fexpand
- _nexpand
- bexpand
- _expand
helpviewer_keywords:
- memory blocks, changing size
- _expand function
- expand function
ms.assetid: 4ac55410-39c8-45c7-bccd-3f1042ae2ed3
ms.openlocfilehash: 8878bb046a122b545f969dd067c37eeb97126387
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82920253"
---
# <a name="_expand"></a>_expand

メモリ ブロックのサイズを変更します。

## <a name="syntax"></a>構文

```C
void *_expand(
   void *memblock,
   size_t size
);
```

### <a name="parameters"></a>パラメーター

*memblock*<br/>
以前に割り当てられていたメモリ ブロックへのポインター。

*size*<br/>
新しいサイズ (バイト単位)。

## <a name="return-value"></a>戻り値

**_expand**は、再割り当てされたメモリブロックへの void ポインターを返します。 **_expand**は、 **realloc**とは異なり、ブロックを移動してサイズを変更することはできません。 したがって、ブロックを移動せずに拡張するために十分なメモリがある場合、 **_expand**の*memblock*パラメーターは戻り値と同じです。

操作中にエラーが検出された場合、 **_expand**は**NULL**を返します。 たとえば、メモリブロックを圧縮するために **_expand**を使用すると、小さなブロックヒープまたは無効なブロックポインターが破損していることが検出され、 **NULL**が返されることがあります。

ブロックを移動せずに特定のサイズに拡張するために使用できるメモリが不足している場合、関数は**NULL**を返します。 **_expand**は、要求よりも小さいサイズに拡張されたブロックを返しません。 エラーが発生した場合、 **errno**はエラーの性質を示します。 **Errno**の詳細については、「 [errno、_doserrno、_sys_errlist、および _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)」を参照してください。

戻り値は、どの型のオブジェクトを格納する場合でも適切なアラインメントが保証されるストレージ領域を指します。 項目の新しいサイズを確認するには、 **_msize**を使用します。 **Void**以外の型へのポインターを取得するには、戻り値に型キャストを使用します。

## <a name="remarks"></a>解説

**_Expand**関数は、以前に割り当てられたメモリブロックのサイズを変更します。そのためには、ヒープ内の位置を移動せずに、ブロックを拡張またはコントラクトします。 *Memblock*パラメーターは、ブロックの先頭を指します。 *Size*パラメーターは、ブロックの新しいサイズをバイト単位で示します。 ブロックの内容は、新しいサイズと古いサイズのうち小さい方のサイズまでは変更されません。 *memblock*は解放されたブロックである必要があります。

> [!NOTE]
> 64ビットプラットフォームでは、新しいサイズが現在のサイズよりも小さい場合、 **_expand**はブロックをコントラクトしない可能性があります。特に、ブロックのサイズが16K 未満で、低い断片化ヒープに割り当てられている場合、 **_expand**はブロックをそのままにし、 *memblock*を返します。

アプリケーションが C ランタイムライブラリのデバッグバージョンにリンクされている場合、 **_expand**は[_expand_dbg](expand-dbg.md)に解決されます。 デバッグ プロセス中のヒープの管理方法の詳細については、「[CRT デバッグ ヒープ](/visualstudio/debugger/crt-debug-heap-details)」を参照してください。

この関数は、パラメーターを検証します。 *Memblock*が null ポインターである場合、この関数は「[パラメーターの検証](../../c-runtime-library/parameter-validation.md)」で説明されているように、無効なパラメーターハンドラーを呼び出します。 実行の継続が許可された場合、 **errno**は**EINVAL**に設定され、関数は**NULL**を返します。 *Size*が **_HEAP_MAXREQ**より大きい場合、 **errno**は**ENOMEM**に設定され、関数は**NULL**を返します。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

## <a name="requirements"></a>必要条件

|関数|必須ヘッダー|
|--------------|---------------------|
|**_expand**|\<malloc.h>|

互換性の詳細については、「[互換性](../../c-runtime-library/compatibility.md)」を参照してください。

## <a name="example"></a>例

```C
// crt_expand.c

#include <stdio.h>
#include <malloc.h>
#include <stdlib.h>

int main( void )
{
   char *bufchar;
   printf( "Allocate a 512 element buffer\n" );
   if( (bufchar = (char *)calloc( 512, sizeof( char ) )) == NULL )
      exit( 1 );
   printf( "Allocated %d bytes at %Fp\n",
         _msize( bufchar ), (void *)bufchar );
   if( (bufchar = (char *)_expand( bufchar, 1024 )) == NULL )
      printf( "Can't expand" );
   else
      printf( "Expanded block to %d bytes at %Fp\n",
            _msize( bufchar ), (void *)bufchar );
   // Free memory
   free( bufchar );
   exit( 0 );
}
```

```Output
Allocate a 512 element buffer
Allocated 512 bytes at 002C12BC
Expanded block to 1024 bytes at 002C12BC
```

## <a name="see-also"></a>関連項目

[メモリの割り当て](../../c-runtime-library/memory-allocation.md)<br/>
[calloc](calloc.md)<br/>
[空け](free.md)<br/>
[malloc](malloc.md)<br/>
[_msize](msize.md)<br/>
[realloc](realloc.md)<br/>
