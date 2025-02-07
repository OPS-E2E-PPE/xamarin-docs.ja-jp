---
title: Android リソース
description: この記事では、Xamarin.Android で Android のリソースの概念を紹介し、その使用方法を文書化されます。 アプリケーションのローカライズ、およびさまざまな画面サイズおよび密度を含む複数のデバイスをサポートするために、Android アプリケーションでリソースを使用する方法を説明します。
ms.prod: xamarin
ms.assetid: C0DCC856-FA36-04CD-443F-68D26075649E
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 02/01/2018
ms.openlocfilehash: f14b3fd31fdda200f51f429367465677d389b1ca
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61013746"
---
# <a name="android-resources"></a>Android リソース

_この記事では、Xamarin.Android で Android のリソースの概念を紹介し、その使用方法を文書化されます。アプリケーションのローカライズ、およびさまざまな画面サイズおよび密度を含む複数のデバイスをサポートするために、Android アプリケーションでリソースを使用する方法を説明します。_


## <a name="overview"></a>概要

Android アプリケーションは、ソース コードだけではめったにありません。 多くの場合、アプリケーションを構成する他の多くのファイルがある: ビデオ、イメージ、フォント、およびオーディオ ファイルがいくつかの名前にします。 総称して、これら以外のソース コード ファイル リソースとして参照されます (ソース コード) と共にビルド プロセス中にコンパイルされ、は、APK の配布とデバイスにインストールとしてパッケージ化します。

![パッケージ化の図](images/packaging-diagram.png)

リソースは、Android アプリケーションにいくつかの利点を提供します。

-  **コード分離付き**&ndash;イメージ、文字列、メニューのアニメーション、色などからソース コードを分離します。そのためのリソースはことができますをローカライズする場合、かなり役立ちます。

-  **複数のデバイスを対象に**&ndash;コードを変更せずにさまざまなデバイス構成の簡単なサポートを提供します。

-  **コンパイル時チェック**&ndash;リソースは、静的で、アプリケーションにコンパイルします。 これにより、簡単にキャッチし、実行時の検索が難しく、修正するコストがかかる場合ではなく、誤りを修正する場合、コンパイル時にチェックするリソースの使用ができます。

新しい Xamarin.Android プロジェクトを開始するときに、いくつかのサブディレクトリと共に、"リソース"という特殊なディレクトリが作成します。

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

![リソースのフォルダーと内容](images/resources-folder-vs.png)

上記の図でアプリケーションのリソースが これらのサブディレクトリには、その型に従って構成されています: イメージは、予定、 **drawable** directory; ビューで、**レイアウト**サブディレクトリなど。
 
# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

![リソースのフォルダーと内容](images/resources-folder-xs.png)

上記の図でアプリケーションのリソースが これらのサブディレクトリには、その型に従って構成されています: イメージは、予定、 **mipmap** directory; ビューで、**レイアウト**サブディレクトリなど。
 
-----

Xamarin.Android アプリケーションでこれらのリソースにアクセスする 2 つの方法があります:*プログラムで*コード内と*宣言によって*特別な XML 構文を使用して xml。

これらのリソースが呼び出される*既定のリソースの*詳細一致が指定されていない限り、すべてのデバイスで使用されます。 さらに、すべての種類のリソースのことができます*代替リ ソース*Android が特定のデバイスを対象に使用できることです。 リソースをユーザーのロケールでは、画面のサイズをターゲットに提供される可能性など、デバイスが縦から横に 90 度回転またはなど。このような場合の各、Android は、アプリケーション開発者によって余分なコーディング作業なしで使用するためのリソースを読み込みます。

呼ばれる、短い文字列を追加して代替のリソースが指定されて、*修飾子*、特定の種類のリソースを保持するディレクトリの末尾にします。

たとえば、**リソース/drawable de**ドイツ語のロケールに設定されているデバイスのイメージを指定中**リソース/drawable fr**イメージは、デバイスがフランス語のロケールに設定を保持します。 デバイスの変更のロケールだけに、同じアプリケーションが実行されているされる次の図では、代替のリソースを提供する例を表示できます。

![さまざまなロケールの例の画面](images/localized-screenshots.png)

この記事では包括的なリソースの使用について見てし、次のトピックについて説明します。

-  **Android リソースの基本**&ndash;画像やフォントなどのリソースの種類をアプリケーションに追加のプログラムと宣言では、既定のリソースを使用します。

-  **デバイスの具体的な構成**&ndash;アプリケーションで、さまざまな画面解像度と密度をサポートします。

-  **ローカリゼーション**&ndash;リソースを使用して、アプリケーションを使用する別のリージョンをサポートします。


## <a name="related-links"></a>関連リンク

- [Android アセットの使用](~/android/app-fundamentals/resources-in-android/android-assets.md)
- [アプリケーションの基礎](https://developer.android.com/guide/topics/fundamentals.html)
- [アプリケーション リソース](https://developer.android.com/guide/topics/resources/index.html)
- [複数の画面をサポートしています。](https://developer.android.com/guide/practices/screens_support.html)
