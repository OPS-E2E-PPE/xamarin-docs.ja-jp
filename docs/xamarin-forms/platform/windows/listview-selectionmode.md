---
title: Windows 上の ListView SelectionMode
description: プラットフォーム仕様はカスタム レンダラーや特殊効果を実装することなく、特定のプラットフォームでのみ利用できる機能の使用を可能にします。 この記事では、ListView 内の項目をタップ ジェスチャに応答できるかどうかを制御する Windows のプラットフォームに固有の使用方法について説明します。
ms.prod: xamarin
ms.assetid: 57EF3A7F-1407-4B31-AE21-D149293D4228
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/24/2018
ms.openlocfilehash: 59b9025b58af4d7080d0506d4994cb72bf4f096d
ms.sourcegitcommit: b23a107b0fe3d2f814ae35b52a5855b6ce2a3513
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65924758"
---
# <a name="listview-selectionmode-on-windows"></a>Windows 上の ListView SelectionMode

[![サンプルのダウンロード](~/media/shared/download.png)サンプルのダウンロード](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)

既定では、Xamarin.Forms、ユニバーサル Windows プラットフォームで[ `ListView` ](xref:Xamarin.Forms.ListView)ネイティブを使用して`ItemClick`ネイティブではなくとの対話に応答するイベント`Tapped`イベント。 これにより Windows ナレーターとキーボードで操作できるように、ユーザー補助機能、`ListView`します。 ただし、内の任意のタップ ジェスチャ レンダリングも、`ListView`使用できなくなります。

このユニバーサル Windows プラットフォームのプラットフォーム固有のコントロールかどうか内の項目を[ `ListView` ](xref:Xamarin.Forms.ListView)タップ ジェスチャに応答できるため、かどうか、ネイティブ`ListView`発生、`ItemClick`または`Tapped`イベント。 これは、 XAML で[`ListView.SelectionMode`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListView.SelectionModeProperty)添付プロパティを[`ListViewSelectionMode`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode)列挙型の値に設定して使用します。

```xaml
<ContentPage ...
             xmlns:windows="clr-namespace:Xamarin.Forms.PlatformConfiguration.WindowsSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout>
        <ListView ... windows:ListView.SelectionMode="Inaccessible">
            ...
        </ListView>
    </StackLayout>
</ContentPage>
```

代わりに、fluent API を使用して C# から使用できます。

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.WindowsSpecific;
...

listView.On<Windows>().SetSelectionMode(ListViewSelectionMode.Inaccessible);
```

`ListView.On<Windows>`メソッドは、このプラットフォームに固有はユニバーサル Windows プラットフォームでのみ実行されるを指定します。 [ `ListView.SetSelectionMode` ](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListView.SetSelectionMode(Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Windows,Xamarin.Forms.ListView},Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode))メソッドで、 [ `Xamarin.Forms.PlatformConfiguration.WindowsSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific)名前空間を使用しているかどうかの項目を[ `ListView` ](xref:Xamarin.Forms.ListView)でジェスチャをタップに応答できる、[ `ListViewSelectionMode` ](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode)列挙型の 2 つの値を提供します。

- [`Accessible`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode.Accessible) – ことを示します、`ListView`はネイティブに起動`ItemClick`との対話を処理し、そのためユーザー補助機能を提供するイベントです。 そのため、Windows ナレーターおよびキーボードと対話できます、`ListView`します。 ただし、項目を`ListView`タップ ジェスチャに応答できません。 既定の動作は、この`ListView`ユニバーサル Windows プラットフォーム上のインスタンス。
- [`Inaccessible`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode.Inaccessible) – ことを示します、`ListView`はネイティブに起動`Tapped`の対話を処理するイベントです。 そのため、項目を`ListView`タップ ジェスチャに応答できます。 ただし、ユーザー補助機能はありませんし、Windows ナレーターとキーボードと対話できませんので、`ListView`します。

> [!NOTE]
> `Accessible`と`Inaccessible`選択モードは相互に排他的と、アクセス可能な間を選択する必要があります[ `ListView` ](xref:Xamarin.Forms.ListView)または`ListView`タップ ジェスチャに応答することができます。

さらに、 [ `GetSelectionMode` ](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListView.GetSelectionMode(Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Windows,Xamarin.Forms.ListView}))メソッドを使用して、現在を返す[ `ListViewSelectionMode`](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode)します。

結果はするが、指定された[ `ListViewSelectionMode` ](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific.ListViewSelectionMode)に適用される、 [ `ListView` ](xref:Xamarin.Forms.ListView)、どのコントロールかどうか内の項目、`ListView`タップ ジェスチャに応答できるため、かどうか、ネイティブ`ListView`発生、`ItemClick`または`Tapped`イベント。

## <a name="related-links"></a>関連リンク

- [プラットフォーム仕様 (サンプル)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/PlatformSpecifics/)
- [プラットフォーム仕様の作成](~/xamarin-forms/platform/platform-specifics/index.md#creating-platform-specifics)
- [WindowsSpecific API](xref:Xamarin.Forms.PlatformConfiguration.WindowsSpecific)
