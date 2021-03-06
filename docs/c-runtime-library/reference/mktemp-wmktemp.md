---
title: _mktemp、_wmktemp
ms.date: 4/2/2020
api_name:
- _wmktemp
- _mktemp
- _o__mktemp
- _o__wmktemp
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
- api-ms-win-crt-stdio-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _tmktemp
- wmktemp
- tmktemp
- _wmktemp
- _mktemp
helpviewer_keywords:
- _wmktemp function
- _mktemp function
- files [C++], temporary
- tmktemp function
- _tmktemp function
- wmktemp function
- mktemp function
- temporary files [C++]
ms.assetid: 055eb539-a8c2-4a7d-be54-f5b6d1eb5c85
ms.openlocfilehash: 536a63841c6e29fa003eb8b99c896f6d1cf5519f
ms.sourcegitcommit: 5a069c7360f75b7c1cf9d4550446ec2fa2eb2293
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82919103"
---
# <a name="_mktemp-_wmktemp"></a>_mktemp、_wmktemp

一意のファイル名を作成します。 これらの関数のセキュリティを強化したバージョンについては、「[_mktemp_s、_wmktemp_s](mktemp-s-wmktemp-s.md)」をご覧ください。

## <a name="syntax"></a>構文

```C
char *_mktemp(
   char *nameTemplate
);
wchar_t *_wmktemp(
   wchar_t *nameTemplate
);
template <size_t size>
char *_mktemp(
   char (&nameTemplate)[size]
); // C++ only
template <size_t size>
wchar_t *_wmktemp(
   wchar_t (&nameTemplate)[size]
); // C++ only
```

### <a name="parameters"></a>パラメーター

*nameTemplate*<br/>
ファイル名のパターン。

## <a name="return-value"></a>戻り値

これらの各関数は、変更された nameTemplate へのポインターを返します。 *Nametemplate*の形式が正しくない場合、または指定された nametemplate から一意の名前を作成できない場合、関数は**NULL**を返します。

## <a name="remarks"></a>解説

**_Mktemp**関数は、 *nametemplate*引数を変更することによって、一意のファイル名を作成します。 は、ランタイムシステムが現在使用しているマルチバイトコードページに従ってマルチバイト文字のシーケンスを認識し、マルチバイト文字列の引数を適切な方法で自動的に処理します。 **_mktemp** **_wmktemp**は **_mktemp**のワイド文字バージョンです。**_wmktemp**の引数と戻り値はワイド文字列です。 **_wmktemp**と **_mktemp**は、 **_wmktemp**がマルチバイト文字列を処理しない点を除いて、同じように動作します。

既定では、この関数のグローバル状態はアプリケーションにスコープが設定されています。 これを変更するには、「 [CRT でのグローバル状態](../global-state.md)」を参照してください。

### <a name="generic-text-routine-mappings"></a>汎用テキスト ルーチンのマップ

|Tchar.h のルーチン|_UNICODE および _MBCS が未定義の場合|_MBCS が定義されている場合|_UNICODE が定義されている場合|
|---------------------|--------------------------------------|--------------------|-----------------------|
|**_tmktemp**|**_mktemp**|**_mktemp**|**_wmktemp**|

*Nametemplate*引数の形式は*base*XXXXXX です。ここで、 *base*は指定する新しいファイル名の一部で、各 X は **_mktemp**によって提供される文字のプレースホルダーです。 *Nametemplate*内の各プレースホルダー文字は、大文字の x である必要があります。 **_mktemp**は*base*を保持し、最初の末尾の x をアルファベット文字に置き換えます。 **_mktemp**は、次の末尾の X を5桁の値に置き換えます。この値は、呼び出し元のプロセスを識別する一意の番号、またはマルチスレッドプログラムでの呼び出し元のスレッドを示します。

**_Mktemp**の呼び出しが成功するたびに、 *nametemplate*が変更されます。 同じ*Nametemplate*引数を持つ同じプロセスまたはスレッドからの後続の呼び出しでは、 **_mktemp**は、前の呼び出しで **_mktemp**によって返された名前と一致するファイル名を確認します。 指定された名前のファイルが存在しない場合、 **_mktemp**はその名前を返します。 以前に返されたすべての名前のファイルが存在する場合、 **_mktemp**は、以前に返された名前で使用されていた英字を ' a ' から ' z ' の順に使用可能な次の小文字で置き換えることによって、新しい名前を作成します。 たとえば、 *base*がの場合は次のようになります。

> **1億**

**_mktemp**によって指定された5桁の値は12345であり、最初に返される名前は次のとおりです。

> **fna12345**

この名前を使用してファイル FNA12345 を作成しても、このファイルがまだ存在する場合、 *Nametemplate*の同じ*ベース*を持つ同じプロセスまたはスレッドから次の名前が返されます。

> **fnb12345**

FNA12345 が存在しない場合、次に返される名前はもう一度次のようになります。

> **fna12345**

**_mktemp**は、 *Base*と*nametemplate*の値の任意の組み合わせに対して最大26個の一意のファイル名を作成できます。 したがって、FNZ12345 は、この例で使用される*base*および*nametemplate*の値に対して作成できる **_mktemp**最後の一意のファイル名です。

エラーが発生すると、 **errno**が設定されます。 *Nametemplate*の形式が無効な場合 (たとえば、6 X 未満)、 **errno**は**EINVAL**に設定されます。 使用可能なすべてのファイル名が既に存在するため **_mktemp**が一意の名前を作成できない場合は、nametemplate を空の文字列に設定して、 **eexist**を返す **_mktemp**ます。

C++ では、これらの関数にテンプレートのオーバーロードがあります。このオーバーロードは、これらの関数に対応するセキュリティで保護された新しい関数を呼び出します。 詳細については、「[セキュリティ保護されたテンプレート オーバーロード](../../c-runtime-library/secure-template-overloads.md)」を参照してください。

## <a name="requirements"></a>必要条件

|ルーチン|必須ヘッダー|
|-------------|---------------------|
|**_mktemp**|\<io.h>|
|**_wmktemp**|\<io.h> または \<wchar.h>|

互換性について詳しくは、「 [Compatibility](../../c-runtime-library/compatibility.md)」をご覧ください。

## <a name="example"></a>例

```C
// crt_mktemp.c
// compile with: /W3
/* The program uses _mktemp to create
* unique filenames. It opens each filename
* to ensure that the next name is unique.
*/

#include <io.h>
#include <string.h>
#include <stdio.h>
#include <errno.h>

char *template = "fnXXXXXX";
char *result;
char names[27][9];

int main( void )
{
   int i;
   FILE *fp;

   for( i = 0; i < 27; i++ )
   {
      strcpy_s( names[i], sizeof( names[i] ), template );
      /* Attempt to find a unique filename: */
      result = _mktemp( names[i] );  // C4996
      // Note: _mktemp is deprecated; consider using _mktemp_s instead
      if( result == NULL )
      {
         printf( "Problem creating the template\n" );
         if (errno == EINVAL)
         {
             printf( "Bad parameter\n");
         }
         else if (errno == EEXIST)
         {
             printf( "Out of unique filenames\n");
         }
      }
      else
      {
         fopen_s( &fp, result, "w" );
         if( fp != NULL )
            printf( "Unique filename is %s\n", result );
         else
            printf( "Cannot open %s\n", result );
         fclose( fp );
      }
   }
}
```

```Output
Unique filename is fna03912
Unique filename is fnb03912
Unique filename is fnc03912
Unique filename is fnd03912
Unique filename is fne03912
Unique filename is fnf03912
Unique filename is fng03912
Unique filename is fnh03912
Unique filename is fni03912
Unique filename is fnj03912
Unique filename is fnk03912
Unique filename is fnl03912
Unique filename is fnm03912
Unique filename is fnn03912
Unique filename is fno03912
Unique filename is fnp03912
Unique filename is fnq03912
Unique filename is fnr03912
Unique filename is fns03912
Unique filename is fnt03912
Unique filename is fnu03912
Unique filename is fnv03912
Unique filename is fnw03912
Unique filename is fnx03912
Unique filename is fny03912
Unique filename is fnz03912
Problem creating the template.
Out of unique filenames.
```

## <a name="see-also"></a>関連項目

[ファイル処理](../../c-runtime-library/file-handling.md)<br/>
[fopen、_wfopen](fopen-wfopen.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_getpid](getpid.md)<br/>
[_open、_wopen](open-wopen.md)<br/>
[_setmbcp](setmbcp.md)<br/>
[_tempnam、_wtempnam、tmpnam、_wtmpnam](tempnam-wtempnam-tmpnam-wtmpnam.md)<br/>
[tmpfile](tmpfile.md)<br/>
