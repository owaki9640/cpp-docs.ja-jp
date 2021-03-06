---
title: '[全般] プロパティ ページ (ファイル)'
ms.date: 08/30/2019
f1_keywords:
- VC.Project.VCFileConfiguration.ExcludedFromBuild
- VC.Project.VCFileConfiguration.Tool
ms.assetid: 26e3711e-9e7d-4e8d-bc4c-2474538efdad
ms.openlocfilehash: a9281a0ea02bd9b1fd529453cb9a67e54e4ddda7
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80168976"
---
# <a name="general-property-page-file"></a>[全般] プロパティ ページ (ファイル)

このトピックは、Windows プロジェクトに適用されます。 Windows 以外のプロジェクトについては、「 [Linux C++プロパティページリファレンス](../../linux/prop-pages-linux.md)」を参照してください。

**ソリューションエクスプローラー**ファイルノードを右クリックすると、 **[構成プロパティ]** ノードの下の **[全般]** プロパティページが開きます。 次のプロパティが含まれています。

- **ビルドから除外**

   現在の構成のビルドに、ファイルを含めるかどうかを指定します。

   プログラムを使用してこのプロパティにアクセスする方法については、「<xref:Microsoft.VisualStudio.VCProjectEngine.VCFileConfiguration.ExcludedFromBuild%2A>」を参照してください。

- **コンテンツ**(UWP アプリにのみ適用されます)アプリパッケージに含めるコンテンツがファイルに含まれるかどうかを指定します。

- **項目の種類**

   **項目の種類**は、ビルド処理中にファイルを処理するために使用されるツールを指定します。 [拡張機能が Visual Studio で認識され](/visualstudio/extensibility/visual-cpp-project-extensibility?view=vs-2019#project-items)ているファイルには、このプロパティの既定値があります。 カスタムファイルの種類がある場合、または既知のファイルの種類の既定のツールをオーバーライドする場合は、ここでカスタムツールを指定できます。 詳細については、「[カスタム ビルド ツールの指定](../specifying-custom-build-tools.md)」を参照してください。 このプロパティページを使用して、ファイルがビルド処理の一部ではないことを指定することもできます。

   *.Cpp*ファイルのプロパティページを次の図に示します。 この種類のファイルの既定の**項目の種類**は**C/C++コンパイラ**(*cl.exe*) で、プロパティページは、このファイルにのみ適用できるさまざまなコンパイラ設定を公開します。

   ![プロジェクト項目の [全般] プロパティページ](media/file-general-item-type.png "項目の種類の選択")

    次の表に、既定の項目の種類を示します。

    |[ファイル拡張子]|アイテムの種類|既定のツール|
    |-|-|-|
    |.appx|XAML アプリケーション定義|[アプリパッケージャー](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)|
    |hlsl、cso|HLSL コンパイラ|[fxc .exe](/windows/win32/direct3dtools/fxc)|
    |.h|C/C++ヘッダー|[C/C++ プロセッサ](../../preprocessor/c-cpp-preprocessor-reference.md)|
    |該当なし|ビルドに参加しません|該当なし|
    |.xml、.xslt、.xsl|xml|[XML エディター](/visualstudio/xml-tools/xml-editor)|
    |. resw、. resw|PRI リソース (UWP アプリ)|[MakePri .exe](/windows/uwp/app-resources/compile-resources-manually-with-makepri)|
    ||メディア (UWP)|[アプリパッケージャー](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)|
    |.xsd|XML データジェネレーターツール|[XML スキーマ定義ツール (xsd.exe)](/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe) (.net ワークロードが必要です。 MSVC には含まれていません。)|
    ||マニフェスト ツール|[mt.exe](/windows/win32/sbscs/mt-exe)|
    |.rc|リソース|[Windows リソースコンパイラ (rc .exe)](/windows/win32/menurc/resource-compiler)|
    |. package.appxmanifest|アプリケーションパッケージマニフェスト|[アプリパッケージャー](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)|
    |.obj|Object|[C/C++リンカー (link .exe)](cl-invokes-the-linker.md)|
    |...|フォント|該当なし|
    |.txt|Text|該当なし|
    |該当なし|カスタムビルドツール|ユーザー定義|
    |該当なし|ファイルのコピー|該当なし|
    |.packagelayout|アプリケーションパッケージのレイアウト|[アプリパッケージャー](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)|
    |.resx|コンパイラマネージリソース|[Resgen.exe (リソース ファイル ジェネレーター)](/dotnet/framework/tools/resgen-exe-resource-file-generator)|
    |. natvis|C++デバッガーの視覚化ファイル|[Natvis framework](/visualstudio/debugger/create-custom-views-of-native-objects)|
    |.jpg、.bmp、.ico など。|Image|アプリケーションの種類に基づくリソースコンパイラ。|
    |.cpp|C/C++コンパイラ|cl.exe|

   プログラムを使用してこのプロパティにアクセスする方法については、「<xref:Microsoft.VisualStudio.VCProjectEngine.VCFileConfiguration.Tool%2A>」を参照してください。

**[構成プロパティ]** ノードの下の **[全般]** プロパティページにアクセスする方法の詳細については、「 [Visual Studio でのコンパイラおよびビルドプロパティの設定C++ ](../working-with-project-properties.md)」を参照してください。

## <a name="see-also"></a>参照

[C++プロジェクトプロパティページのリファレンス](property-pages-visual-cpp.md)
