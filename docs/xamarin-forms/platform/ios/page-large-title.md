---
title: IOS での大きいページ タイトル
description: プラットフォーム仕様はカスタム レンダラーや特殊効果を実装することなく、特定のプラットフォームでのみ利用できる機能の使用を可能にします。 この記事では、NavigationPage のナビゲーション バーでの大規模なタイトルとページ タイトルを表示します。 iOS プラットフォームに固有の使用方法について説明します。
ms.prod: xamarin
ms.assetid: 45FD9145-8319-452C-9AE6-624431A4D43C
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
ms.openlocfilehash: 01c5e4f449a1aed84a73b0284ba15e0c03deeed7
ms.sourcegitcommit: b23a107b0fe3d2f814ae35b52a5855b6ce2a3513
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65925775"
---
# <a name="large-page-titles-on-ios"></a>IOS での大きいページ タイトル

[![サンプルのダウンロード](~/media/shared/download.png)サンプルのダウンロード](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)

この iOS プラットフォームに固有のナビゲーション バーでの大規模なタイトルとページ タイトルの表示に使用する[ `NavigationPage` ](xref:Xamarin.Forms.NavigationPage)、iOS 11 以降を使用するデバイス。 大タイトルは左寄せで大きいフォントが使われます。そして画面の領域を効率的に使うために、ユーザーがコンテンツをスクロールした時に、標準のタイトルに移り変わります。 しかし横向きの画面では、コンテンツのレイアウトを最適化するためにタイトルはナビゲーションバーの中央に戻ります。 この機能は XAML で `NavigationPage.PrefersLargeTitles` 添付プロパティを `boolean` 値に設定して使用します。

```xaml
<NavigationPage xmlns="http://xamarin.com/schemas/2014/forms"
                xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
                ...
                ios:NavigationPage.PrefersLargeTitles="true">
  ...
</NavigationPage>
```

または、fluent API を使用して C# から使用できます。

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

var navigationPage = new Xamarin.Forms.NavigationPage(new iOSLargeTitlePageCS());
navigationPage.On<iOS>().SetPrefersLargeTitles(true);
```

`NavigationPage.On<iOS>` メソッドは、このプラットフォーム仕様が iOS上 でのみ動作することを指定します。 `NavigationPage.SetPrefersLargeTitle`メソッドは、 [ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)名前空間に存在し、大タイトルを有効にするかどうかを制御します。

[`NavigationPage`](xref:Xamarin.Forms.NavigationPage)で大タイトルが有効になると、ナビゲーションスタックにあるすべてのページは大タイトルで表示されるようになります。 この動作は個々のページ上で `Page.LargeTitleDisplay` 添付プロパティを `LargeTitleDisplayMode` 列挙型の値に設定することで上書きできます。


```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
             Title="Large Title"
             ios:Page.LargeTitleDisplay="Never">
  ...
</ContentPage>
```

または、fluent API を使用して、C# からページの動作を上書きできます。

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

public class iOSLargeTitlePageCS : ContentPage
{
    public iOSLargeTitlePageCS(ICommand restore)
    {
        On<iOS>().SetLargeTitleDisplay(LargeTitleDisplayMode.Never);
        ...
    }
    ...
}
```

`Page.On<iOS>`メソッドは、このプラットフォーム仕様が iOS上 でのみ動作することを指定します。  `Page.SetLargeTitleDisplay` メソッドは、 [ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific) 名前空間に存在し、[ `Page`](xref:Xamarin.Forms.Page) 上の大タイトルの動作を `LargeTitleDisplayMode`列挙型が提供する次の 3 つ値を使って制御します。

- `Always` – 強制的にナビゲーションバーとフォントサイズに大きいフォーマットを使う。
- `Automatic` – ナビゲーションスタックの前のアイテムと同じスタイル（大または小）を使う
- `Never` – 強制的に標準の小さいフォーマットのナビゲーションバーを使う。

さらに、`SetLargeTitleDisplay` メソッドは、現在の `LargeTitleDisplay` を返す `LargeTitleDisplayMode` メソッドを呼び出すことによって列挙値を切り替えるのに使用することができます。

```csharp
switch (On<iOS>().LargeTitleDisplay())
{
    case LargeTitleDisplayMode.Always:
        On<iOS>().SetLargeTitleDisplay(LargeTitleDisplayMode.Automatic);
        break;
    case LargeTitleDisplayMode.Automatic:
        On<iOS>().SetLargeTitleDisplay(LargeTitleDisplayMode.Never);
        break;
    case LargeTitleDisplayMode.Never:
        On<iOS>().SetLargeTitleDisplay(LargeTitleDisplayMode.Always);
        break;
}
```

その結果、指定した `LargeTitleDisplayMode` が[`Page`](xref:Xamarin.Forms.Page) に適用され、大タイトルの動作を制御します。

![](page-large-title-images/large-title.png " \"Blur 効果 Platform-Specific\"")

## <a name="related-links"></a>関連リンク

- [プラットフォーム仕様 (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)
- [プラットフォーム仕様の作成](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
