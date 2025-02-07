---
title: Xamarin.Forms シェルのポップアップ
description: ポップアップは、シェル アプリケーションのルート メニューであり、アイコンから、または画面の横からスワイプして、アクセスすることが可能です。 ポップアップは、オプションのヘッダー、ポップアップ項目、およびオプションのメニュー項目から構成されています。
ms.prod: xamarin
ms.assetid: FEDE51EB-577E-4B3E-9890-B7C1A5E52516
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/23/2019
ms.openlocfilehash: 51d8764854db2fb62a412fab6e1e48c8beabbf1f
ms.sourcegitcommit: 6ad272c2c7b0c3c30e375ad17ce6296ac1ce72b2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66178060"
---
# <a name="xamarinforms-shell-flyout"></a>Xamarin.Forms シェルのポップアップ

[![サンプルのダウンロード](~/media/shared/download.png)サンプルのダウンロード](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/Xaminals/)

ポップアップは、シェル アプリケーションのルート メニューであり、アイコンから、または画面の横からスワイプして、アクセスすることが可能です。 ポップアップは、オプションのヘッダー、ポップアップ項目、およびオプションのメニュー項目から構成されています。

![シェルの注釈付きポップアップのスクリーンショット](flyout-images/flyout-annotated.png "注釈付きポップアップ")

ポップアップの背景色は、必要に応じて、バインド可能なプロパティ `Shell.FlyoutBackgroundColor` を使って [`Color`](xref:Xamarin.Forms.Color) に設定することができます。 このプロパティはカスケード スタイル シート (CSS) から設定することもできます。 詳しくは、「[Xamarin.Forms シェル固有のプロパティ](~/xamarin-forms/user-interface/styles/css/index.md#xamarinforms-shell-specific-properties)」をご覧ください。

## <a name="flyout-icon"></a>ポップアップのアイコン

シェル アプリケーションには既定でハンバーガー アイコンがあり、これを押すとポップアップが開きます。 このアイコンは、バインド可能なプロパティ `Shell.FlyoutIcon` ([`ImageSource`](xref:Xamarin.Forms.ImageSource) 型) を設定することで、適切なアイコンに変更できます。

```xaml
<Shell ...
       FlyoutIcon="flyouticon.png">
    ...       
</Shell>
```

## <a name="flyout-behavior"></a>ポップアップの動作

ポップアップには、ハンバーガー アイコンを使うか、画面の側面からスワイプすることでアクセスできます。 しかし、`Shell.FlyoutBehavior` 添付プロパティを次の `FlyoutBehavior` 列挙メンバーのいずれかに設定することで、この動作を変更することができます。

- `Disabled` – ユーザーはポップアップを開けません。
- `Flyout` – ユーザーはポップアップを開いたり閉じたりできます。 これは、`FlyoutBehavior` プロパティの既定値です。
- `Locked` – ポップアップはユーザーによって閉じられず、コンテンツとは重なりません。

次の例は、ポップアップを無効にする方法を示しています。

```xaml
<Shell ...
       FlyoutBehavior="Disabled">
    ...
</Shell>
```

> [!NOTE]
> `FlyoutBehavior` 添付プロパティを `Shell`、`FlyoutItem`、`ShellContent`、およびページ オブジェクトで設定し、ポップアップの既定の動作をオーバーライドすることができます。

さらに、プログラムでポップアップを開いたり閉じたりすることができます。それにはバインド可能なプロパティ `Shell.FlyoutIsPresented` を、現在ポップアップを表示するかどうかを示す `boolean` 値に設定します。

```csharp
Shell.Current.FlyoutIsPresented = false;
```

## <a name="flyout-header"></a>ポップアップのヘッダー

ポップアップ ヘッダーは、`Shell.FlyoutHeader` プロパティ値によって設定できる `object` で定義されている外観を持ち、必要に応じてポップアップの上部に表示されるコンテンツです。

```xaml
<Shell.FlyoutHeader>
    <controls:FlyoutHeader />
</Shell.FlyoutHeader>
```

`FlyoutHeader` の種類を次の例に示します。

```xaml
<ContentView xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="Xaminals.Controls.FlyoutHeader"
             HeightRequest="200">
    <Grid BackgroundColor="Black">
        <Image Aspect="AspectFill"
               Source="xamarinstore.jpg"
               Opacity="0.6" />
        <Label Text="Animals"
               TextColor="White"
               FontAttributes="Bold"
               HorizontalTextAlignment="Center"
               VerticalTextAlignment="Center" />
    </Grid>
</ContentView>
```

これにより、次のポップアップ ヘッダーが得られます。

![ポップアップ ヘッダーのスクリーンショット](flyout-images/flyout-header.png "ポップアップ ヘッダー")

または、`Shell.FlyoutHeaderTemplate` プロパティを [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) に設定することでもポップアップ ヘッダーの外観を定義できます。

```xaml
<Shell.FlyoutHeaderTemplate>
    <DataTemplate>
        <Grid BackgroundColor="Black"
              HeightRequest="200">
            <Image Aspect="AspectFill"
                   Source="xamarinstore.jpg"
                   Opacity="0.6" />
            <Label Text="Animals"
                   TextColor="White"
                   FontAttributes="Bold"
                   HorizontalTextAlignment="Center"
                   VerticalTextAlignment="Center" />
        </Grid>            
    </DataTemplate>
</Shell.FlyoutHeaderTemplate>
```

既定では、ポップアップ ヘッダーはポップアップ内で固定されますが、十分な項目がある場合は以下のコンテンツはスクロールされます。 しかし、この動作はバインド可能なプロパティ `Shell.FlyoutHeaderBehavior` を次の `FlyoutHeaderBehavior` 列挙メンバーのいずれかに設定することで変更できます。

- `Default` – プラットフォームの既定の動作を使います。 これは、`FlyoutHeaderBehavior` プロパティの既定値です。
- `Fixed` – ポップアップ ヘッダーは常に表示され、変更されません。
- `Scroll` – ユーザーが項目をスクロールすると、ポップアップ ヘッダーはスクロールしてビューから外れます。
- `CollapseOnScroll` – ユーザーが項目をスクロールすると、ポップアップ ヘッダーは折りたたまれてタイトルだけが表示されます。

ユーザーがスクロールするとポップアップ ヘッダーが折りたたまれるようにする方法を次の例に示します。

```xaml
<Shell ...
       FlyoutHeaderBehavior="CollapseOnScroll">
    ...
</Shell>
```

## <a name="flyout-items"></a>ポップアップの項目

アプリケーションのナビゲーション パターンにポップアップが含まれる場合、サブクラス化された `Shell` オブジェクトに 1 つまたは複数の `FlyoutItem` オブジェクトを含めて、各 `FlyoutItem` オブジェクトがポップアップ上の 1 つの項目を表す必要があります。 各 `FlyoutItem` オブジェクトは、`Shell` オブジェクトの子である必要があります。

次の例では、ポップアップ ヘッダーと 2 つのポップアップ項目を含むポップアップを作成します。

```xaml
<Shell xmlns="http://xamarin.com/schemas/2014/forms"
       xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
       xmlns:controls="clr-namespace:Xaminals.Controls"
       xmlns:views="clr-namespace:Xaminals.Views"
       x:Class="Xaminals.AppShell">
    <Shell.FlyoutHeader>
        <controls:FlyoutHeader />
    </Shell.FlyoutHeader>
    <FlyoutItem Title="Cats"
                Icon="cat.png">
        <Tab>
            <ShellContent>
                <views:CatsPage />
            </ShellContent>
        </Tab>
    </FlyoutItem>
    <FlyoutItem Title="Dogs"
                Icon="dog.png">
        <Tab>
            <ShellContent>
                <views:DogsPage />
            </ShellContent>
        </Tab>
    </FlyoutItem>
</Shell>
```

この例では、各 [`ContentPage`](xref:Xamarin.Forms.ContentPage) はポップアップ項目からのみアクセスできます。

[![iOS と Android での、ポップアップ項目を備えたシェルの 2 ページ アプリのスクリーンショット](flyout-images/two-page-app-flyout.png "ポップアップ項目を備えたシェルの 2 ページ アプリ")](flyout-images/two-page-app-flyout-large.png#lightbox "ポップアップ項目を備えたシェルの 2 ページ アプリ")

> [!NOTE]
> ポップアップ ヘッダーが存在しない場合、ポップアップ項目はポップアップの一番上に表示されます。 それ以外の場合、それらはポップアップ ヘッダーの下に表示されます。

シェルには暗黙的な変換演算子が備わっています。これにより、ビジュアル ツリーに追加のビューを導入することなくシェルの視覚階層を単純化できます。 これが可能になるのは、サブクラス化された `Shell` オブジェクトには `FlyoutItem` オブジェクトまたは `TabBar` オブジェクトしか含めることができず、それには `Tab` オブジェクトしか含めることができず、それには `ShellContent` オブジェクトしか含めることができないためです。 このような暗黙的な変換演算子を使って、前の例から `FlyoutItem`、`Tab`、`ShellContent` オブジェクトを削除することができます。

```xaml
<Shell xmlns="http://xamarin.com/schemas/2014/forms"
       xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
       xmlns:controls="clr-namespace:Xaminals.Controls"
       xmlns:views="clr-namespace:Xaminals.Views"
       x:Class="Xaminals.AppShell">
    <Shell.FlyoutHeader>
        <controls:FlyoutHeader />
    </Shell.FlyoutHeader>
    <views:CatsPage IconImageSource="cat.png" />
    <views:DogsPage IconImageSource="dog.png" />
</Shell>
```

この暗黙的な変換では、各 [`ContentPage`](xref:Xamarin.Forms.ContentPage) オブジェクトが自動的に `ShellContent` オブジェクトでラップされ、それが `Tab` オブジェクトでラップされ、それが `FlyoutItem` オブジェクトでラップされます。

> [!IMPORTANT]
> シェル アプリケーションでは、`ShellContent` オブジェクトの子である各 [`ContentPage`](xref:Xamarin.Forms.ContentPage) は、アプリケーションの起動中に作成されます。 この手法を利用して追加の `ShellContent` オブジェクトを付け加えると、アプリケーションの起動時に追加のページが作成され、起動エクスペリエンスの低下を引き起こす場合があります。 ただし、シェルでは、ナビゲーションに応答して、必要に応じてページを作成することも可能です。 詳しくは、「[Xamarin.Forms シェルのタブ](tabs.md)」ガイドにある「[効率的なページの読み込み](tabs.md#efficient-page-loading)」をご覧ください。

### <a name="flyoutitem-class"></a>FlyoutItem クラス

`FlyoutItem` クラスには、ポップアップ項目の外観と動作を制御する次のプロパティが含まれています。

- `FlyoutDisplayOptions`: `FlyoutDisplayOptions` 型、ポップアップで項目とその子を表示する方法を定義します。 既定値は `AsSingleItem` です。
- `CurrentItem`: `Tab` 型、選択された項目。
- `Items`: `IList<Tab>` 型、`FlyoutItem` 内のすべてのタブを定義します。
- `FlyoutIcon`: `ImageSource` 型、項目用に使用するアイコン。 このプロパティが設定されていない場合は、代わりに `Icon` プロパティ値が使われます。
- `Icon`: `ImageSource` 型、ポップアップではないクロムのパーツに表示するアイコンを定義します。
- `IsChecked`: `boolean` 型、現在ポップアップで項目を強調表示するかどうかを定義します。
- `IsEnabled`: `boolean` 型、クロム内の項目を選択できるかどうかを定義します。
- `IsTabStop`: `bool` 型、タブのナビゲーションに `FlyoutItem` を含めるかどうかを指定します。 既定値は `true` で、値を `false` にすると、`FlyoutItem` は、`TabIndex` が設定されているかどうかにかかわらず、タブ ナビゲーション インフラストラクチャによって無視されます。
- `TabIndex`: `int` 型、ユーザーが Tab キーを押して項目間を移動するときに、`FlyoutItem` オブジェクトがフォーカスを受け取る順序を指定します。 このプロパティの既定値は 0 です。
- `Title`: `string` 型、UI に表示するタイトル。
- `Route`: `string` 型、項目を処理するために使う文字列。

`Route` プロパティを除き、これらのプロパティはすべて [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) オブジェクトを基盤としています。つまり、プロパティはデータ バインディングの対象にすることができます。

> [!NOTE]
> サブクラス化されたシェル オブジェクトの `FlyoutItem` オブジェクトは、すべて `Shell.Items` コレクションに追加されます。これによってポップアップに表示される項目のリストが定義されます。

また、`FlyoutItem` ク ラスでは、オーバーライドできる次のメソッドが公開されます。

- `OnTabIndexPropertyChanged`: `TabIndex` プロパティが変更されるたびに呼び出されます。
- `OnTabStopPropertyChanged`: `IsTabStop` プロパティが変更されるたびに呼び出されます。
- `TabIndexDefaultValueCreator`: `int` を返します。`TabIndex` プロパティの既定値を設定するために呼び出されます。
- `TabStopDefaultValueCreator`: `bool` を返します。`TabStop` プロパティの既定値を設定するために呼び出されます。

## <a name="flyout-display-options"></a>ポップアップの表示オプション

`FlyoutDisplayOptions` 列挙体を使って、次のメンバーを定義できます。

- `AsSingleItem`: 項目は 1 つの項目として表示されます。
- `AsMultipleItems`: 項目とその子は、項目のグループとしてポップアップに表示されます。

`FlyoutItem.FlyoutDisplayOptions` プロパティを `AsMultipleItems` に設定することで、`FlyoutItem` 内の `Tab` ごとのポップアップ項目を作成できます。

```xaml
<Shell xmlns="http://xamarin.com/schemas/2014/forms"
       xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
       xmlns:controls="clr-namespace:Xaminals.Controls"
       xmlns:views="clr-namespace:Xaminals.Views"
       FlyoutHeaderBehavior="CollapseOnScroll"
       x:Class="Xaminals.AppShell">

    <Shell.FlyoutHeader>
        <controls:FlyoutHeader />
    </Shell.FlyoutHeader>

    <FlyoutItem Title="Animals"
                FlyoutDisplayOptions="AsMultipleItems">
        <Tab Title="Domestic"
             Icon="paw.png">
            <ShellContent Title="Cats"
                          Icon="cat.png"
                          ContentTemplate="{DataTemplate views:CatsPage}" />
            <ShellContent Title="Dogs"
                          Icon="dog.png"
                          ContentTemplate="{DataTemplate views:DogsPage}" />
        </Tab>
        <ShellContent Title="Monkeys"
                      Icon="monkey.png"
                      ContentTemplate="{DataTemplate views:MonkeysPage}" />
        <ShellContent Title="Elephants"
                      Icon="elephant.png"
                      ContentTemplate="{DataTemplate views:ElephantsPage}" />  
        <ShellContent Title="Bears"
                      Icon="bear.png"
                      ContentTemplate="{DataTemplate views:BearsPage}" />
    </FlyoutItem>

    <ShellContent Title="About"
                  Icon="info.png"
                  ContentTemplate="{DataTemplate views:AboutPage}" />    
</Shell>
```

この例では、`FlyoutItem` オブジェクトの子である `Tab` オブジェクトと、`FlyoutItem` オブジェクトの子である `ShellContent` オブジェクトに向けてポップアップ項目が作成されます。 こうなる理由は、`FlyoutItem` オブジェクトの子である各 `ShellContent` オブジェクトが、自動的に `Tab` オブジェクトでラップされるためです。 さらに、最後の `ShellContent` オブジェクトに向けてポップアップ項目が作成されます。これは `Tab` オブジェクト、`FlyoutItem` オブジェクトの順でラップされます。

これにより、次のポップアップ項目が得られます。

[![iOS と Android での FlyoutItem オブジェクトを含むポップアップのスクリーンショット](flyout-images/flyout-reduced.png "FlyoutItem オブジェクトを含むシェルのポップアップ")](flyout-images/flyout-reduced-large.png#lightbox "FlyoutItem オブジェクトを含むシェルのポップアップ")

## <a name="define-flyoutitem-appearance"></a>ポップアップの外観を定義する

各 `FlyoutItem` の外観は、`Shell.ItemTemplate` 添付プロパティを [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) に設定することでカスタマイズできます。

```xaml
<Shell ...>
    ...
    <Shell.ItemTemplate>
        <DataTemplate>
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="0.2*" />
                    <ColumnDefinition Width="0.8*" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding FlyoutIcon}"
                       Margin="5"
                       HeightRequest="45" />
                <Label Grid.Column="1"
                       Text="{Binding Title}"
                       FontAttributes="Italic"
                       VerticalTextAlignment="Center" />
            </Grid>
        </DataTemplate>
    </Shell.ItemTemplate>
</Shell>
```

この例では、各 `FlyoutItem` オブジェクトのタイトルを斜体で表示します。

[![iOS と Android でのテンプレート化された FlyoutItem オブジェクトのスクリーンショット](flyout-images/flyoutitem-templated.png "シェルのテンプレート化された FlyoutItem オブジェクト")](flyout-images/flyoutitem-templated-large.png#lightbox "シェルのテンプレート化された FlyoutItem オブジェクト")

> [!NOTE]
> シェルには、`ItemTemplate` の [`BindingContext`](xref:Xamarin.Forms.BindableObject.BindingContext) に対する `Title` と `FlyoutIcon` プロパティが用意されています。

## <a name="flyoutitem-tab-order"></a>FlyoutItem のタブ オーダー

既定では、`FlyoutItem` オブジェクトのタブ オーダーは、XAML に記載されている順序、またはプログラムで子コレクションに追加された順序と同じです。 この順序は、キーボードを使って `FlyoutItem` オブジェクト間をナビゲートする際の順序であり、多くの場合、この既定の順序が最善の順序です。

既定のタブ オーダーは `FlyoutItem.TabIndex` プロパティを設定することで変更できます。これは、ユーザーが Tab キーを押して項目間を移動するときに、`FlyoutItem` オブジェクトがフォーカスを受け取る順序を示します。 プロパティの既定値は 0 で、任意の `int` 値に設定できます。

既定のタブ オーダーを使用するとき、または `TabIndex` プロパティを設定するときは、次の規則が適用されます。

- `TabIndex` が 0 に設定されている `FlyoutItem` オブジェクトは、XAML または子コレクション内でのその宣言の順序に基づいて、タブ オーダーに追加されます。
- `TabIndex` が 0 よりも大きい `FlyoutItem` オブジェクトは、その `TabIndex` の値に基づいてタブ オーダーに追加されます。
- `TabIndex` が 0 よりも小さい `FlyoutItem` オブジェクトは、値が 0 のすべてのものより先にタブ オーダーに追加され、表示されます。
- `TabIndex` が競合する場合は、宣言の順序によって解決されます。

タブ オーダーを定義した後、Tab キーを押すと、フォーカスは `TabIndex` の昇順で `FlyoutItem` オブジェクト間を移動し、最後のオブジェクトに達すると先頭に戻ります。

`FlyoutItem` オブジェクトのタブ オーダーを設定するだけでなく、タブ オーダーから一部のオブジェクトを除外することが必要な場合があります。 これは `FlyoutItem.IsTabStop` プロパティを使って実現できます。これは、`FlyoutItem` がタブ ナビゲーションに含まれるかどうかを示します。 既定値は `true` で、値を `false` にすると、`FlyoutItem` は、`TabIndex` が設定されているかどうかにかかわらず、タブ ナビゲーション インフラストラクチャによって無視されます。

## <a name="set-the-current-flyoutitem"></a>現在の FlyoutItem を設定する

`Shell` クラスには、`CurrentItem` という名前のバインド可能な `FlyoutItem` 型のプロパティがあります。これは現在選択されている `FlyoutItem` を表します。 シェル アプリケーションを最初に実行すると、このプロパティはサブクラス化された `Shell` オブジェクトの最初の `FlyoutItem` に設定されます。 しかし、次の例に示すように、このプロパティは別の `FlyoutItem` にも設定できます。

```xaml
<Shell ...
       CurrentItem="{x:Reference aboutItem}">
    <FlyoutItem Title="Animals"
                FlyoutDisplayOptions="AsMultipleItems">
        ...
    </FlyoutItem>
    <ShellContent x:Name="aboutItem"
                  Title="About"
                  Icon="info.png"
                  ContentTemplate="{DataTemplate views:AboutPage}" />
</Shell>
```

このコードでは、`aboutItem` という名前の `ShellContent` オブジェクトを `CurrentItem` プロパティとして設定し、それが表示されるようにしています。 この例では暗黙的な変換が使われ、`ShellContent` オブジェクトが `Tab` オブジェクトでラップされ、それが `FlyoutItem` オブジェクトでラップされています。

これに相当する C# コードを次に示します。

```csharp
Shell.Current.CurrentItem = aboutItem;
```

## <a name="menu-items"></a>メニュー項目

メニュー項目は必要に応じてポップアップに追加できますが、各メニュー項目は [ `MenuItem`](xref:Xamarin.Forms.MenuItem) オブジェクトによって表されます。 ポップアップ上の `MenuItem` オブジェクトの位置は、シェル ビジュアル階層内の宣言の順序によって異なります。 そのため、`FlyoutItem` オブジェクトの前に宣言された `MenuItem` オブジェクトは、ポップアップの一番上に表示され、`FlyoutItem` オブジェクトの後に宣言された `MenuItem` オブジェクトは、ポップアップの一番下に表示されます。

> [!NOTE]
> `MenuItem` クラスには、[`Clicked`](xref:Xamarin.Forms.MenuItem.Clicked) イベントと [`Command`](xref:Xamarin.Forms.MenuItem.Command) プロパティがあります。 そのため、`MenuItem` オブジェクトを使って、タップされた `MenuItem` への応答としてアクションを実行するシナリオを実現できます。 このようなシナリオには、ナビゲーションの実行や、特定の Web ページで Web ブラウザーを開くことなどが含まれます。

次の例に示すように、[`MenuItem`](xref:Xamarin.Forms.MenuItem) オブジェクトをポップアップに追加できます。

```xaml
<Shell ...>
    ...            
    <MenuItem Text="Random"
              IconImageSource="random.png"
              Command="{Binding RandomPageCommand}" />
    <MenuItem Text="Help"
              IconImageSource="help.png"
              Command="{Binding HelpCommand}"
              CommandParameter="https://docs.microsoft.com/xamarin/xamarin-forms/app-fundamentals/shell" />    
</Shell>
```

このコードでは、すべてのポップアップ項目の下で、2 つの [`MenuItem`](xref:Xamarin.Forms.MenuItem) オブジェクトがポップアップに追加されます。

[![iOS と Android での MenuItem オブジェクトを含むポップアップのスクリーンショット](flyout-images/flyout.png "MenuItem オブジェクトを含むシェルのポップアップ")](flyout-images/flyout-large.png#lightbox "MenuItem オブジェクトを含むシェルのポップアップ")

最初の [`MenuItem`](xref:Xamarin.Forms.MenuItem)オブジェクトでは `RandomPageCommand` という名前の `ICommand` が実行され、アプリケーション内のランダムなページに移動します。 2 番目の `MenuItem` オブジェクトでは `HelpCommand` という名前の `ICommand` が実行され、`CommandParameter` プロパティで指定した URL が Web ブラウザーで開かれます。

> [!NOTE]
> 各 `MenuItem` の [`BindingContext`](xref:Xamarin.Forms.BindableObject.BindingContext) は、サブクラス化された `Shell` オブジェクトから継承されます。

## <a name="define-menuitem-appearance"></a>MenuItem の外観を定義する

各 `MenuItem` の外観は、`Shell.MenuItemTemplate` 添付プロパティを [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) に設定することでカスタマイズできます。

```xaml
<Shell ...>
    <Shell.MenuItemTemplate>
        <DataTemplate>
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="0.2*" />
                    <ColumnDefinition Width="0.8*" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding Icon}"
                       Margin="5"
                       HeightRequest="45" />
                <Label Grid.Column="1"
                       Text="{Binding Text}"
                       FontAttributes="Italic"
                       VerticalTextAlignment="Center" />
            </Grid>
        </DataTemplate>
    </Shell.MenuItemTemplate>
    ...
    <MenuItem Text="Random"
              IconImageSource="random.png"
              Command="{Binding RandomPageCommand}" />
    <MenuItem Text="Help"
              IconImageSource="help.png"
              Command="{Binding HelpCommand}"
              CommandParameter="https://docs.microsoft.com/xamarin/xamarin-forms/app-fundamentals/shell" />  
</Shell>
```

この例では、シェルレベルの `MenuItemTemplate` を各 `MenuItem` オブジェクトに添付し、各 `MenuItem` オブジェクトのタイトルを斜体で表示します。

[![iOS と Android でのテンプレート化された MenuItem オブジェクトのスクリーンショット](flyout-images/menuitem-templated.png "シェルのテンプレート化された MenuItem オブジェクト")](flyout-images/menuitem-templated-large.png#lightbox "シェルのテンプレート化された MenuItem オブジェクト")

> [!NOTE]
> シェルには、`MenuItemTemplate` の [`BindingContext`](xref:Xamarin.Forms.BindableObject.BindingContext) に対する [`Text`](xref:Xamarin.Forms.MenuItem.Text) と [`IconImageSource`](xref:Xamarin.Forms.MenuItem.IconImageSource) プロパティが用意されています。`

`Shell.MenuItemTemplate` は添付プロパティであるため、さまざまなテンプレートを特定の `MenuItem` オブジェクトに添付できます。

```xaml
<Shell ...>
    <Shell.MenuItemTemplate>
        <DataTemplate>
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="0.2*" />
                    <ColumnDefinition Width="0.8*" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding Icon}"
                       Margin="5"
                       HeightRequest="45" />
                <Label Grid.Column="1"
                       Text="{Binding Text}"
                       FontAttributes="Italic"
                       VerticalTextAlignment="Center" />
            </Grid>
        </DataTemplate>
    </Shell.MenuItemTemplate>
    ...
    <MenuItem Text="Random"
              IconImageSource="random.png"
              Command="{Binding RandomPageCommand}" />
    <MenuItem Text="Help"
              Icon="help.png"
              Command="{Binding HelpCommand}"
              CommandParameter="https://docs.microsoft.com/xamarin/xamarin-forms/app-fundamentals/shell">
        <Shell.MenuItemTemplate>
            <DataTemplate>
                ...
            </DataTemplate>
        </Shell.MenuItemTemplate>
    </MenuItem>
</Shell>
```

この例では、シェルレベルの `MenuItemTemplate` を最初の `MenuItem` オブジェクトに添付し、インライン `MenuItemTemplate` を 2 番目の `MenuItem` に添付しています。

## <a name="related-links"></a>関連リンク

- [Xaminals (サンプル)](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/Xaminals/)
