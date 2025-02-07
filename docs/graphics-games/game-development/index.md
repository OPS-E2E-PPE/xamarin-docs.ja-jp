---
title: Xamarin を使用したゲーム開発の概要
description: このドキュメントでは、ゲームの作成方法と Xamarin.iOS および Xamarin.Android で使用するために使用できるテクノロジのサンプリングの両方を記述する xamarin では、ゲーム開発の概要を説明します。
ms.prod: xamarin
ms.assetid: 0E3CDCD2-FBE4-49F5-A70E-8A7B937BAF1D
author: conceptdev
ms.author: crdun
ms.date: 03/24/2017
ms.openlocfilehash: 314bedcb6bb2d7ebf9d8f98428b6a7cad059f73b
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61382060"
---
# <a name="introduction-to-game-development-with-xamarin"></a>Xamarin を使用したゲーム開発の概要

ゲームを開発できる非常に魅力的な特にモバイル プラットフォームでの作業を発行することが簡単であるかを指定します。 この記事では、概念を説明します。 し、目標は、ゲームやプログラムを楽しむのために、高品質の AAA を作成するかどうか、どのようにゲームの開発に関連するテクノロジが、ゲームを作成します。

ここでは、次のトピックについて説明します。

- **非ゲーム プログラミングの概念とゲーム**– では、いくつかの概念について説明します、ゲームの開発に固有またはその他の種類の開発と共有されますが、強調をここで、重要度のために必要です。
- **ゲームの開発チーム**– このセクションではゲーム開発者のチームでさまざまな役割を確認します。
- **ゲームのアイデアを作成する**– このセクションを参照して、新しいアイデアをゲームの作成: 最初の手順で新しいゲームを作成します。
- **ゲームの開発テクノロジ**– ここで、ゲーム開発者として、生産性を向上させるためのクロス プラットフォーム テクノロジの一部を示します。

## <a name="game-vs-non-game-programming-concepts"></a>ゲームと非ゲーム プログラミングの概念

新しい概念と開発パターンの多くの場合、プログラマのゲーム開発への移動が表示されます。 このセクションでは、これらの概念の概要を表示します。

### <a name="the-game-loop"></a>ゲームのループ

一般的なゲームでは、定数の動きや画面ユーザーの操作と自動のゲーム ロジックの両方への応答で発生するへの変更が必要です。 これは通常対極としてによって実現、*ゲーム ループ*します。 ゲームのループが何らかの種類のループ (while ループ) などのステートメント、30、60 などの非常に高い頻度で実行され*秒あたりのフレーム*します。

単純なゲーム ループを次の図を次に示します。

![](images/image1.png "これは、単純なゲーム ループを次の図")

以下について説明します。 テクノロジは抽象化実際 while のループがこの抽象化に関係なく、フレームごとの更新プログラムの概念は表示されます。

コードのパフォーマンスがあっても、最もシンプルなゲームで優先されます。 例: を実行する 10 ミリ秒を受け取る関数はフレームごとに複数回呼び出された場合に特に – ゲームのパフォーマンスに大きな影響を与える可能性があります。 30 フレームごとに、ゲームが実行されている場合 2 つ目、つまり各フレームが 33 ミリ秒単位で実行する必要があります。 これに対し、そのような関数できない可能性がありますも顕著なは、ゲーム以外のアプリケーションで、ボタン クリックに応答でのみ実行される場合。

一般的なフレームごとの実行可能性のあるロジックの種類は次のとおりです。

- **読み取り入力**– ゲームをタッチ画面、キーボード、マウス、またはゲーム コント ローラーなどの入力のハードウェアをチェックして、ユーザーがゲームに操作されたかを確認する必要があります。
- **移動**– オブジェクト別に 1 つの場所からどの移動が非常に小さな移動通常すべてのフレームに滑らかな動きの奥行の金額。
- **衝突**– 多くのゲームでは、さまざまなオブジェクトが重複または交差するかどうかの頻繁に行う必要があります。 競合がこの記事では、後のセクションで詳しく説明します。 専用の物理シミュレーション システムでの移動との競合を処理できます。
- **ゲームに固有の状態の確認**– プレーヤー十分なポイントまたは割り当てられた時間実行するかどうかを獲得したかどうかなど、特定の条件を使ってゲームの状態を制御できます。
- **AI 動作**– 哨戒敵の対戦相手のドライバーをレースの周囲の移動など、player によって制御されないオブジェクトの動作を制御するために使用するフレームごとのロジック。
- **レンダリング**– ほとんどのゲームは表示される内容を更新ですべてのフレームを画面します。 これは、レベル内を移動する文字) などのゲーム プレイまたは単に影響する変更に応答で行うことがあります (落下雪やアニメーション化されたアイコン) の洗練された視覚効果を提供します。

多くのゲームではないアプリが発生したイベントに応答の状態を変更する傾向がありますに、多くの上に示したアクティビティ全体のアプリケーションの状態を変更できることに留意してください。

### <a name="content-loading-and-unloading"></a>コンテンツの読み込みとアンロード

手動で読み込みおよびアンロード (破棄) のコンテンツは開発で使用するテクノロジに応じて必要あります。 手動で読み込むと、資産のアンロードはさまざまな理由のために必要な可能性があります。

 - 資産を読み込む 1 つのフレームの長さに関連した時間がかかる場合があります。 一部の資産は、mid ゲームプレイを読み込まれている場合、エクスペリエンスが中断される重大を読み込むには、秒をもかかる場合があります。 読み込み時間が長い (2 秒以上、2 つなど) の場合は、アニメーション化された表示たい画面または進行状況バーをロードします。
 - 資産は、大量のゲームのターゲット プラットフォームで提供されているものに収まるように読み込まれる内容のアクティブな管理を必要とする RAM を使用できます。
 - ゲームは、RAM 内に収まるよりも多くの資産を表示する必要があります。 多くの場合、「開いている World」のゲームには、プレイヤーがシームレスにナビゲートできます – しない読み込み画面を作成するが、大規模な環境が含まれます。 ここでは、ストリーミング コンテンツのカスタム システムと管理のメモリ使用量を作成する必要があります。

カスタム ファイル形式は、読み込み時に処理がカスタムの読み込みコードを必要とする必要があります。

### <a name="math"></a>数値演算

多くのゲームでは、ゲーム以外のアプリケーションよりもより高度な数学が必要です。 もちろん、数学のレベルは、ゲームの複雑さによって異なります。 一般に 3D ゲームでは、2 D よりも複数の数値演算が必要です。 さいわいなことに単純なゲームで常に開始することができ、更に学びを深めることが可能です。 ゲーム開発は、数学を学習する優れた方法かもしれません。

使用している – デカルト平面に慣れている場合、X と Y 座標を – オブジェクトを配置し、ゲーム開発の概要を十分に理解します。 正 Y 指して上方デカルトを次に示します。

![](images/image2.png "正 Y 指して上方デカルトが表示されます。")

> [!IMPORTANT]
> いくつかエンジン/Api では、場所、オブジェクトの Y 値を増やすことが下に移動、他のシステムを正の Y は、座標系を使用して、座標系を使用します。 システム間で移動する場合は、この点に留意してください。
正弦と余弦) などの三角関数は、回転の任意の形式を実装する 2D ゲームでよく使用されます。

3D ゲームをすることを計画している場合は、線形代数 (回転、および 3 次元空間で移動) 用に (高速化を実装する) のいくつかの計算からの概念を理解する必要があります。

### <a name="content-pipelines"></a>コンテンツ パイプライン

用語*コンテンツ パイプライン*ゲームで使用すると、最終的な形式のファイル (.png 画像ファイルなど) を作成する際に、その形式から取得するまでにするプロセスを参照します。 終了の形式をコンテンツの種類が使用されているコンテンツの表示に使用されるテクノロジだけでなくによって異なります。

一部のコンテンツ パイプラインは、非常に高速し、労力を必要としない可能性があります。 たとえば、ほとんどのゲーム エンジンと Api は、未処理の形式で、.png ファイル形式を読み込むことができます。 その一方で、読み込まれる前に別の形式に処理する必要があります (3 D モデル) などのより複雑な形式と、この処理は、資産のサイズと複雑さに応じて時間がかかることができます。

## <a name="game-development-teams"></a>ゲームの開発チーム

ゲーム開発には、プロセスに関連する個人向けの新しい役割とタイトルが導入されています。 ほとんどのゲーム開発者は、さまざまな分野がいくつか存在するために、完全なゲームを解放するために必要なスキルを満たすことはできません。 これが開発 – 最も一般的な問題の一部の領域の完全な一覧ではないことに留意してください。

- **プログラマ**– ほとんどの人が読み取るこの記事では、このカテゴリに分類されます。 ゲーム開発のプログラマの役割は、ゲーム以外のアプリケーションで、プログラマの役割に似ています。 責任には、当然ながらバグの修正の追加と、コンテンツを表示する、指定されたプロジェクトのコンテキストでの一般的なタスクをシステムの開発、ゲームの流れを制御するためのロジックを記述が含まれます。
- **2D アーティスト**– 2D アーティストが作成を担当する*2D アセット*します。 ゲームの GUI、パーティクル、環境、および文字のイメージ ファイルが含まれます。 3D ゲームを開発している場合は、し、2 D アーティストできない可能性があります環境と文字を担当します。 無料見つかりますでゲームのアート[ http://opengameart.org/ ](http://opengameart.org/)します。
- **3D アーティスト**– 3D アーティストが作成を担当する*3D アセット*します。 3D モデル、環境、文字、およびプロパティ (家具、プラント、およびその他の直言) にはが含まれます。 一部のチームは、3 D のアーティストとチームの規模に応じて 3D アニメーターによって区別されます。 無料見つかりますでゲームの 3D のアート[ http://opengameart.org/ ](http://opengameart.org/)します。
- **ゲームのデザイナー** – ゲームのデザイナーは、ゲームをプレイする方法を定義する責任を負います。 これにより、設定など、ゲーム、ゲームとゲームでプレーヤーの進行の全体的な目的は、高度な意思決定が含めることができます。 ゲームのデザイナーはことが移動またはレベル アップ、係数を定義して、レベルのレイアウトのデザインの操作に対する入力のマッピングなどの非常に詳細な意思決定に関連するできます。 注意用語*デザイナー*可能性があります、ゲームやコンテキストに応じてビジュアル デザイナーを参照してください。
- **デザイナーのサウンド**– サウンド デザイナーは、ゲームのオーディオ アセットを担当します。 チームによっては、小規模のチームが担当者のすべてのオーディオの 1 つあります。 中に、効果音や作曲者 の作成を担当する個人の区別可能性があります。

## <a name="creating-a-game-idea"></a>ゲームのアイデアを作成します。

ゲームの設計が表示される簡単 – すべての唯一の要件を行うには、"make 何かおもしろい" 残念ながら、多くの開発者にとって自体には開発を起動するアイデアを作成するとき。

ゲームの設計の分野が簡単に説明しませんし、アートと同様に向上することが必要です、プログラミングは、またはが、このセクションを使用して、パスを開始できます。

新しい開発者は、小規模で開始する必要があります。 我慢して大規模な最新のビデオ ゲームを作り直すに難しいことができますが、小さなゲームは、強化学習環境とより満足感のあるエクスペリエンスと、高速化の進行状況。

両方の学習と商用のゲームの目的で多くのゲームでは、改善または既存のゲームを変更すると開始します。 アイデアを生成する方法の 1 つがひらめきを得るための他のゲームで検索されます。 たとえば、個人をゲームとゲーム プレイに関するどのような特性を確認してくださいに楽しく学べるようにを検討できます。 探索、ゲームのメカニズム、またはストーリーの進行の支配的である可能性があります。 忘れずに、新しいアイデアを検索するときに「レトロ」ゲームも検討してください。

新しいアイデアを生成するための別の手法では、パズル ゲーム、戦略ゲームなど場合など、特定のジャンルを検討してください。 ジャンルを使い慣れた開発者には、出発点として適していますが提供します。

既存のゲームを作り変えても教育エクスペリエンスが、この完成品の商用の実行可能性を制限することができます。 正確な複製では、あるものも含めて、ゲームを作成するプロセスでは、貴重な教育エクスペリエンスを提供します。

## <a name="game-development-technology"></a>ゲーム開発テクノロジ

Xamarin.Android と Xamarin.iOS を使用している開発者があるさまざまなテクノロジを利用できるように、ゲーム開発を支援します。 このセクションではいくつかの最も人気のあるクロスプラット フォーム ソリューションについて説明します。

### <a name="cocossharp"></a>CocosSharp

CocosSharp は、Cocos 2D ゲーム エンジンのオープン ソースのクロスプラット フォーム対応バージョンです。 エンジンは、Android、iOS、Mac OS X、Windows デスクトップ、Windows RT および Windows Phone へのアクセスを提供します。

CocosSharp の 2D ゲーム開発用の単純なプログラマ API について説明します。 趣味と同様の商用のプロジェクトの実行可能なテクノロジを CocosSharp よう、2 D ゲーム開発の普及を reignite をモバイル デバイスでのゲームで成長してきました。 (これは NuGet から入手可能) ソース コードまたは .dll ファイルとして提供されますが、ビジュアル エディター; は提供されません。そのため、CocosSharp エンジンとの対話には、プログラミングの知識が必要です。

CocosSharp による開始をチェック アウト、 [CocosSharp ガイド](~/graphics-games/cocossharp/index.md)します。

ゲーム、CocosSharp による怒りの ninja オブジェクトが作成され、複数のプラットフォームを既に実行中のゲームを探している場合の出発点として適してできます。

![](images/image3.png "怒りの ninja オブジェクトを作成して CocosSharp によるゲーム")

これをダウンロードして取得の詳細については、 [AngryNinjas Github ページ](https://github.com/xamarin/AngryNinjas)します。

### <a name="monogame"></a>MonoGame

MonoGame は、オープン ソースのクロス プラットフォームのバージョンの Microsoft の XNA API です。 MonoGame を iOS、Android、Mac OS X、Linux、Windows、Windows RT、PS4、PSVita、Xbox One、およびスイッチ用のゲームを作成できます。

異なり、CocosSharp MonoGame は技術的にはないゲーム エンジンをゲームの開発 API ではなくです。 これは、直接ゲーム オブジェクトの管理、手動でオブジェクトを描画、およびカメラなどの一般的なオブジェクトの実装に MonoGame を使用した作業が必要であることを意味し、*シーン グラフ*(親子階層のゲーム オブジェクトとの間)。 違いを理解するには、CocosSharp が MonoGame の上に構築されたことを検討してください。 MonoGame を一般化グラフィック、レンダリング、および、オーディオなどのプラットフォーム固有のテクノロジのいくつか CocosSharp 整理し、ゲーム ロジックを実装するコードを提供します。

MonoGame は、MonoGame を使用した作業は、プログラミングの知識が必要ですので、標準的なビジュアル開発環境を提供しません。

MonoGame を使用してゲームの注目すべき例があります。

FEZ:

![](images/image7.png "FEZ")

要塞:

![](images/image8.jpg "要塞")

MonoGame を使用した作業を開始するには に進み、 [MonoGame ガイド](~/graphics-games/monogame/index.md)します。

### <a name="urhosharp"></a>UrhoSharp

UrhoSharp は、クロスプラット フォームで高度な 3D および 2D エンジンのジオメトリで素材、ライトとカメラを使用して、アプリケーションのアニメーションが 2D と 3D のシーンを作成するために使用できます。

![](images/urhosharp.gif "UrhoSharp は、クロスプラット フォームで高度な 3D および 2D エンジン 3D および 2D のアニメーションのシーンを作成するために使用できます。")

チェック アウト、 [UrhoSharp ガイド](~/graphics-games/urhosharp/index.md)を開始します。

### <a name="additional-technology"></a>その他のテクノロジ

上の強調表示されているテクノロジは、使用できるテクノロジのサンプルだけです。 注目すべきその他のテクノロジは次のとおりです。

- **Sprite Kit** – Xamarin は、Apple の Sprite Kit ゲームのフレームワークのすべてのネイティブ API の機能にアクセスできるようサポートを提供します。 Sprite Kit は、Apple が作成したテクノロジであるため、iOS のエコシステムの残りの部分との統合を提供します。 もちろん、Sprite Kit はクロスプラット フォーム対応ため、Android では使用できません。 Sprite Kit の使用に関する詳細については、この投稿を参照してください。  [https://blog.xamarin.com/make-games-with-xamarin.ios-and-sprite-kit/](https://blog.xamarin.com/make-games-with-xamarin.ios-and-sprite-kit/)
- **シーンのキット**– Xamarin iOS アプリに 3D グラフィックの実装を簡素化、Apple のシーン キット framework のサポートも提供します。 シーンのキットは、統合とプラットフォーム固有の考慮事項の Sprite Kit を上記で説明したように、Apple によって提供されるテクノロジもです。 シーンのキットの詳細については、この投稿を参照してください。 [https://blog.xamarin.com/3d-in-ios-8-with-scene-kit/](https://blog.xamarin.com/3d-in-ios-8-with-scene-kit/)
- **OpenTK –** OpenTK (が開いているツール キットの略) は、iOS、Apple、および Mac への低レベルの OpenGL アクセスを提供します。 ハードウェア。 OpenTK の詳細については、メイン ページを参照してください。  [http://www.opentk.com/](http://www.opentk.com/)

## <a name="related-links"></a>関連リンク

- [CocosSharp のガイド](~/graphics-games/cocossharp/index.md)
- [MonoGame ガイド](~/graphics-games/monogame/index.md)
- [UrhoSharp のガイド](~/graphics-games/urhosharp/index.md)
