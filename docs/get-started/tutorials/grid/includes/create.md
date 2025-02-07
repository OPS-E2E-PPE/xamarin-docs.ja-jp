---
ms.openlocfilehash: 807f0b7b2969d9f1039beb1a7ec7d535be5c84dc
ms.sourcegitcommit: a153623a69b5cb125f672df8007838afa32e9edf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67277318"
---
# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

このチュートリアルを完了するには、 **.NET によるモバイル開発**ワークロードがインストールされた、Visual Studio 2019 (最新リリース) が必要です。 さらに、iOS でチュートリアル アプリケーションを構築するには、ペアリング済みの Mac が必要になります。 Xamarin プラットフォームのインストールについては、「[Xamarin のインストール](~/get-started/installation/index.md)」を参照してください。 Mac ビルド ホストへの Visual Studio 2019 の接続については、「[Xamarin.iOS 開発のために Mac とペアリングする](~/ios/get-started/installation/windows/connecting-to-mac/index.md)」を参照してください。

1. Visual Studio を起動し、**GridTutorial** という名前の新しい空の Xamarin.Forms アプリを作成します。 共有コード メカニズムとして .NET Standard がアプリで使用されていることを確認します。

    > [!IMPORTANT]
    > このチュートリアルの C# スニペットと XAML スニペットでは、**GridTutorial** という名前のソリューションが必要です。 別の名前を使用すると、コードをこのチュートリアルからソリューションにコピーするときに、ビルド エラーが発生します。

    作成される .NET Standard ライブラリの詳細については、[Xamarin.Forms クイック スタート Deep Dive](~/get-started/first-app/index.md) の [Xamarin.Forms アプリケーションの構造](~/get-started/first-app/index.md)に関するページを参照してください。

1. **ソリューション エクスプローラー**の **[GridTutorial]** プロジェクトで、 **[MainPage.xaml]** をダブルクリックして開きます。 次に、 **[MainPage.xaml]** のテンプレート コードをすべて削除し、次のコードに置き換えます。

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="GridTutorial.MainPage">
        <Grid Margin="20,35,20,20">
            <Label Text="The Grid has its Margin property set, to control the rendering position of the Grid." />
        </Grid>
    </ContentPage>
    ```

    このコードでは、[`Grid`](xref:Xamarin.Forms.Grid) の中の [`Label`](xref:Xamarin.Forms.Label) から構成されるページのユーザー インターフェイスを宣言によって定義します。 既定では、`Grid` で 1 つの場所にその子ビューが配置されます。 そのため、複数の子を含む `Grid` では、列と行を指定する必要があります。これについては、次の演習で説明します。 さらに、[`Margin`](xref:Xamarin.Forms.View.Margin) プロパティは、[`ContentPage`](xref:Xamarin.Forms.ContentPage) 内の `Grid` のレンダリング位置を示します。

    > [!NOTE]
    > [`Margin`](xref:Xamarin.Forms.View.Margin) プロパティに加え、[`Padding`](xref:Xamarin.Forms.Layout.Padding) プロパティを [`Grid`](xref:Xamarin.Forms.Grid) に設定することもできます。 [`Padding`](xref:Xamarin.Forms.Layout.Padding) プロパティの値では、`Grid` のビュー間の距離が指定されます。 詳細については「[Margin and Padding](~/xamarin-forms/user-interface/layouts/margin-and-padding.md)」 (余白とスペース) を参照してください。

1. Visual Studio ツール バーで、 **[開始]** ボタン ([再生] ボタンに似た三角形のボタン) を押し、選択した iOS リモート シミュレーターまたは Android エミュレーター内でアプリケーションを起動します。

    [![iOS および Android での、Grid 内の Label のスクリーンショット](../images/create-grid.png "Label を含む Grid")](../images/create-grid-large.png#lightbox "Label を含む Grids")

    [`Grid`](xref:Xamarin.Forms.Grid) の詳細については、「[Xamarin.Forms Grid](~/xamarin-forms/user-interface/layouts/grid.md)」 (Xamarin.Forms のグリッド) を参照してください。

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

このチュートリアルを完了するには、iOS と Android のプラットフォームのサポートがインストールされた Visual Studio for Mac (最新リリース) が必要です。 さらに、Xcode (最新リリース) も必要になります。 Xamarin プラットフォームのインストールについて詳しくは、「[Xamarin のインストール](~/get-started/installation/index.md)」を参照してください。

1. Visual Studio for Mac を起動し、**GridTutorial** という名前の新しい空の Xamarin.Forms アプリを作成します。 共有コード メカニズムとして .NET Standard がアプリで使用されていることを確認します。

    > [!IMPORTANT]
    > このチュートリアルの C# スニペットと XAML スニペットでは、**GridTutorial** という名前のソリューションが必要です。 別の名前を使用すると、コードをこのチュートリアルからソリューションにコピーするときに、ビルド エラーが発生します。

    作成される .NET Standard ライブラリの詳細については、[Xamarin.Forms クイック スタート Deep Dive](~/get-started/first-app/index.md) の [Xamarin.Forms アプリケーションの構造](~/get-started/first-app/index.md)に関するページを参照してください。

1. **Solution Pad** の **[GridTutorial]** プロジェクトで、 **[MainPage.xaml]** をダブルクリックして開きます。 次に、 **[MainPage.xaml]** のテンプレート コードをすべて削除し、次のコードに置き換えます。

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="GridTutorial.MainPage">
        <Grid Margin="20,35,20,20">
            <Label Text="The Grid has its Margin property set, to control the rendering position of the Grid." />
        </Grid>
    </ContentPage>
    ```

    このコードでは、[`Grid`](xref:Xamarin.Forms.Grid) の中の [`Label`](xref:Xamarin.Forms.Label) から構成されるページのユーザー インターフェイスを宣言によって定義します。 既定では、`Grid` で 1 つの場所にその子ビューが配置されます。 そのため、複数の子を含む `Grid` では、列と行を指定する必要があります。これについては、次の演習で説明します。 さらに、[`Margin`](xref:Xamarin.Forms.View.Margin) プロパティは、[`ContentPage`](xref:Xamarin.Forms.ContentPage) 内の `Grid` のレンダリング位置を示します。

    > [!NOTE]
    > [`Margin`](xref:Xamarin.Forms.View.Margin) プロパティに加え、[`Padding`](xref:Xamarin.Forms.Layout.Padding) プロパティを [`Grid`](xref:Xamarin.Forms.Grid) に設定することもできます。 [`Padding`](xref:Xamarin.Forms.Layout.Padding) プロパティの値では、`Grid` のビュー間の距離が指定されます。 詳細については「[Margin and Padding](~/xamarin-forms/user-interface/layouts/margin-and-padding.md)」 (余白とスペース) を参照してください。

1. Visual Studio for Mac ツール バーで、 **[開始]** ボタン ([再生] ボタンに似た三角形のボタン) を押し、選択した iOS シミュレーターまたは Android エミュレーター内でアプリケーションを起動します。

    [![iOS および Android での、Grid 内の Label のスクリーンショット](../images/create-grid.png "Label を含む Grid")](../images/create-grid-large.png#lightbox "Label を含む Grids")

    [`Grid`](xref:Xamarin.Forms.Grid) の詳細については、「[Xamarin.Forms Grid](~/xamarin-forms/user-interface/layouts/grid.md)」 (Xamarin.Forms のグリッド) を参照してください。
