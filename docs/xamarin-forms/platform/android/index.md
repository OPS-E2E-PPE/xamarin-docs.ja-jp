---
title: Android プラットフォーム機能
description: この記事では、Xamarin.Forms アプリケーションを Android 固有の機能を追加する方法について説明します。
ms.prod: xamarin
ms.assetid: E24168F3-0138-4814-86EA-B467F6B8A545
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/07/2018
ms.openlocfilehash: dc02fdc8754db4ae97c29ba2a496804b2263abdc
ms.sourcegitcommit: 482aef652bdaa440561252b6a1a1c0a40583cd32
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65970727"
---
# <a name="android-platform-features"></a>Android プラットフォーム機能

Android 用の Xamarin.Forms アプリケーションの開発には、Visual Studio が必要です。 [要件ページ](~/get-started/requirements.md)の前提条件の詳細が含まれています。

## <a name="platform-specifics"></a>プラットフォーム固有設定

プラットフォーム仕様はカスタム レンダラーや特殊効果を実装することなく、特定のプラットフォームでのみ利用できる機能の使用を可能にします。

Xamarin.Forms のビュー、ページ、および Android でのレイアウトを次のプラットフォーム固有の機能が提供されます。

- 描画の順番を決定するための視覚要素の Z オーダーの制御。 詳細については、次を参照してください。 [android VisualElement 昇格](visualelement-elevation.md)します。
- サポートされている従来のカラー モードを無効にする[ `VisualElement`](xref:Xamarin.Forms.VisualElement)します。 詳細については、次を参照してください。 [android VisualElement レガシ カラー モード](legacy-color-mode.md)します。

Android で Xamarin.Forms のビューでは、次のプラットフォームに固有の機能が提供されます。

- 既定のパディングと Android のボタンの影の値を使用します。 詳細については、次を参照してください。[ボタンのパディングと Android でのシャドウ](button-padding-shadow.md)します。
- 入力方式のソフト キーボードのエディター オプションの設定、 [ `Entry`](xref:Xamarin.Forms.Entry)します。 詳細については、次を参照してください。 [android エントリ入力方式エディター オプション](entry-ime-options.md)します。
- ドロップ シャドウを有効にすると、`ImageButton`します。 詳細については、次を参照してください。 [android ImageButton ドロップ シャドウ](imagebutton-drop-shadow.md)します。
- 高速のスクロールを有効にする、 [ `ListView` ](xref:Xamarin.Forms.ListView)詳細については、次を参照してください。 [Android で高速スクロールを ListView](listview-fast-scrolling.md)します。
- 制御するかどうかを[ `WebView` ](xref:Xamarin.Forms.WebView)混合コンテンツを表示できます。 詳細については、次を参照してください。 [WebView 混合コンテンツ android](webview-mixed-content.md)します。
- ズームを有効にすると、 [ `WebView`](xref:Xamarin.Forms.WebView)します。 詳細については、次を参照してください。 [android web ビューのズーム](webview-zoom-controls.md)します。

Android で Xamarin.Forms のページでは、次のプラットフォームに固有の機能が提供されます。

- 上のナビゲーション バーの高さを設定、 [ `NavigationPage`](xref:Xamarin.Forms.NavigationPage)します。 詳細については、次を参照してください。 [android NavigationPage バーの高さ](navigationpage-bar-height.md)します。
- 内のページ間を移動するときに、遷移アニメーションを無効にすると、 [ `TabbedPage`](xref:Xamarin.Forms.TabbedPage)します。 詳細については、次を参照してください。 [android TabbedPage ページ遷移アニメーション](tabbedpage-transition-animations.md)します。
- [`TabbedPage`](xref:Xamarin.Forms.TabbedPage)でのページ間のスワイプ操作の有効化。 詳細については、次を参照してください。 [TabbedPage ページは Android でスワイプ](tabbedpage-page-swiping.md)します。
- ツールバーの配置と色を設定、 [ `TabbedPage`](xref:Xamarin.Forms.TabbedPage)します。 詳細については、次を参照してください。 [TabbedPage ツールバーの配置と Android での色](tabbedpage-toolbar-placement-color.md)します。

Xamarin.Forms のプラットフォーム固有の次の機能が提供される[ `Application` ](xref:Xamarin.Forms.Application) Android 上のクラス。

- ソフトキーボードの操作モードの設定。 詳細については、次を参照してください。 [Android でのソフト キーボードの入力モード](soft-keyboard-input-mode.md)します。
- AppCompat を使用するアプリケーションに対し、一時停止や再開時に [`Disappearing`](xref:Xamarin.Forms.Page.Appearing)や[`Appearing`](xref:Xamarin.Forms.Page.Appearing) といったぺージのライフサイクルのイベントをそれぞれ無効化する。 詳細については、次を参照してください。 [Android でのページのライフ サイクル イベント](page-lifecycle-events.md)します。

## <a name="platform-support"></a>プラットフォームのサポート

最初に、Xamarin.Forms の Android プロジェクトの既定では、Android 5.0 より前に共通したコントロールのレンダリングの以前のスタイルが使用されます。 テンプレートを使用して構築されたアプリケーションが`FormsApplicationActivity`メイン アクティビティの基本クラスとして。

## <a name="material-design-via-appcompat"></a>AppCompat 経由で素材のデザイン

Xamarin.Forms の Android プロジェクトに使用される`FormsAppCompatActivity`メイン アクティビティの基本クラスとして。 このクラスを使用して**AppCompat**マテリアル デザインのテーマを実装するために Android によって提供される機能です。

Xamarin.Forms の Android プロジェクトには、マテリアル デザインのテーマを追加するには、次の[AppCompat のインストール手順についてのサポート](appcompat-material-design.md)

ここでは、 **Todo** 、既定値は、サンプル`FormsApplicationActivity`:

[![](images/before-appcompat-sml.png "Todo サンプル アプリケーション AppCompat 使わず")](images/before-appcompat.png#lightbox "AppCompat なしの Todo サンプル アプリケーション")

これは、使用するプロジェクトをアップグレードした後の同じコードと`FormsAppCompatActivity`(およびその他のテーマ情報を追加する)。

[![](images/post-appcompat-sml.png "AppCompat とテーマの Todo サンプル アプリケーション")](images/post-appcompat.png#lightbox "AppCompat とテーマの Todo サンプル アプリケーション")

> [!NOTE]
> 使用する場合`FormsAppCompatActivity`、[一部の Android カスタム レンダラー クラスの基本](~/xamarin-forms/app-fundamentals/custom-renderer/renderers.md)異なるものになります。

## <a name="related-links"></a>関連リンク

- [素材のデザインのサポートを追加します。](appcompat-material-design.md)
