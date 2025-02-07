---
title: IOS での ListView の行のアニメーション
description: プラットフォーム仕様はカスタム レンダラーや特殊効果を実装することなく、特定のプラットフォームでのみ利用できる機能の使用を可能にします。 この記事では、ListView の項目のコレクションが更新されるときに、行のアニメーションが無効になっているかどうかを制御、iOS プラットフォームに固有の使用方法について説明します。
ms.prod: xamarin
ms.assetid: E8F5103F-4D8E-4A5A-A16C-7FA14EE786AC
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/21/2019
ms.openlocfilehash: ac71be25492866b1cf2b12d3343c2f4095fc738d
ms.sourcegitcommit: b23a107b0fe3d2f814ae35b52a5855b6ce2a3513
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65925789"
---
# <a name="listview-row-animations-on-ios"></a>IOS での ListView の行のアニメーション

[![サンプルのダウンロード](~/media/shared/download.png)サンプルをダウンロードします。](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)

この iOS プラットフォームに固有のコントロールがアニメーションを行かどうかが無効になっている場合、 [ `ListView` ](xref:Xamarin.Forms.ListView)項目のコレクションが更新されます。 XAML で設定して使用される、`ListView.RowAnimationsEnabled`バインド可能なプロパティを`false`:

```xaml
<ContentPage ...
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout Margin="20">
        <ListView ... ios:ListView.RowAnimationsEnabled="false">
            ...
        </ListView>
    </StackLayout>
</ContentPage>
```

代わりに、fluent API を使用して C# から使用できます。

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
...

listView.On<iOS>().SetRowAnimationsEnabled(false);
```

`ListView.On<iOS>`メソッドは、このプラットフォーム仕様が iOS上 でのみ動作することを指定します。  `ListView.SetRowAnimationsEnabled`メソッドで、 [ `Xamarin.Forms.PlatformConfiguration.iOSSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)行アニメーションがかどうか、名前空間を使用して無効になっているときに、 [ `ListView` ](xref:Xamarin.Forms.ListView)項目のコレクションが更新されます。 さらに、`ListView.GetRowAnimationsEnabled`メソッドを使用して、行のアニメーションが無効になっているかどうかを返す、`ListView`します。

> [!NOTE]
> [`ListView`](xref:Xamarin.Forms.ListView) 既定では、行のアニメーションが有効にします。 新しい行が挿入されると、そのため、アニメーションが発生する`ListView`します。

## <a name="related-links"></a>関連リンク

- [プラットフォーム仕様 (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)
- [プラットフォーム仕様の作成](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [iOSSpecific API](xref:Xamarin.Forms.PlatformConfiguration.iOSSpecific)
