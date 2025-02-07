---
title: コンテナー化 Microservices
description: この章では、信頼性の高い最新のクラウド アプリケーションとマイクロ サービスとコンテナーを使用して、アジャイル、拡張性の高いを構築する方法について説明します。
ms.prod: xamarin
ms.assetid: 5872ad92-04e0-4f1a-9691-79d5602f5683
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/07/2017
ms.openlocfilehash: 33be84bc17f72c8b70d117a0742b001f1f763d3d
ms.sourcegitcommit: 4b402d1c508fa84e4fc3171a6e43b811323948fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61300759"
---
# <a name="containerized-microservices"></a>コンテナー化 Microservices

クライアント サーバー アプリケーションの開発と、各レベルで特定のテクノロジを使用する階層化されたアプリケーションの構築に重点を置いたもたらされました。 このようなアプリケーションと呼ばれる多くの場合、*モノリシック*アプリケーション、およびはピーク時の負荷を事前にスケールするハードウェア上にパッケージ化されています。 この開発アプローチの主な欠点は、確実、個々 のコンポーネントは簡単に拡大縮小、各層内のコンポーネントとテストのコストの間の密結合です。 単純な更新が持つことができます、層の他の予期しない現象その全体のレベルを再評価し、再展開するアプリケーション コンポーネントを変更する必要があるためです。

特に関係、クラウドの時代にはスケーリング個々 のコンポーネントが簡単にすることはできません。 モノリシック アプリケーションは、ドメイン固有の機能を含みは通常、フロント エンド、ビジネス ロジック、データ ストレージなどの機能の層で分かれています。 図 8-1 に示すように、複数のコンピューターにアプリケーション全体を複製することにより、モノリシック アプリケーションはスケールされます。

![](containerized-microservices-images/monolithicapp.png "モノリシック アプリケーションのスケーリング方法")

**図 8-1**:モノリシック アプリケーションのスケーリング方法

## <a name="microservices"></a>マイクロサービス

マイクロ サービスは、アプリケーションの開発とデプロイに別のアプローチで俊敏性、スケール、および最新のクラウド アプリケーションの信頼性の要件には適していますアプローチを提供します。 マイクロ サービス アプリケーションは、連携して、アプリケーションの全体的な機能を提供する独立したコンポーネントに分解されます。 用語のマイクロ サービスには、各マイクロ サービスは、1 つの関数を実装するために、アプリケーションがの独立系の懸念事項を反映するために十分な小さいサービスで構成することが強調されています。 また、各マイクロ サービスでは他のマイクロ サービスが通信してそのデータを共有できるように適切に定義されたコントラクト。 マイクロ サービスの一般的な例は、ショッピング カートが含まれて、処理のインベントリ、購入サブシステム、および支払い処理。

マイクロ サービス スケール アウトできるで個別に規模をまとめて giant のモノリシック アプリケーションと比較しています。 これは、特定の機能領域を必要な処理能力やネットワーク帯域幅需要をサポートするためを不必要にスケール アウト アプリケーションの他の領域ではなくスケールできることを意味します。 図 8-2 は、マイクロ サービスの展開を個別にスケーリングと、この方法を示しています。 マシン間でサービスのインスタンスを作成します。

![](containerized-microservices-images/microservicesapp.png "マイクロ サービス アプリケーションのスケーリング方法")

**図 8-2**:マイクロ サービス アプリケーションのスケーリング方法

マイクロ サービスのスケール アウトは、アプリケーションの負荷の変化に適応することにより、ほぼ瞬時にできます。 たとえば、アプリケーションの web に接続する機能に単一のマイクロ サービスでは、追加の受信トラフィックを処理するためにスケール アウトする必要があるアプリケーションでのみ、マイクロ サービス可能性があります。

アプリケーションのスケーラビリティのクラシック モデルで永続的なデータを格納する外部データ ストアを共有、負荷分散でステートレスな層です。 ステートフル マイクロ サービスは、通常サーバーに配置されますにローカルに保存、独自の永続的なデータを管理、ネットワークのオーバーヘッドを回避するためにアクセスし、複雑なサービス間で操作します。 これにより、データの最速の可能な処理を有効にされ、システムをキャッシュする必要があります。 さらに、スケーラブルなステートフル マイクロ サービスには通常、これを超える単一のサーバーがサポートできる、データのサイズと転送のスループットを管理する、インスタンス間でデータがパーティション分割します。

マイクロ サービスでは、独立した更新プログラムもサポートします。 この疎結合のマイクロ サービス間では、高速で信頼性の高いアプリケーションの進化を提供します。 その独立した、分散型の性質には、ローリング更新プログラムは、単一のマイクロ サービスのインスタンスのサブセットのみが、特定の時点で更新されますがサポートしています。 そのため、問題が検出された場合、バグの更新できますロールバック、問題のあるコードまたは構成ですべてのインスタンスを更新する前に。 同様に、マイクロ サービスでは通常、スキーマのバージョン管理を使用して、クライアントに伝達されているインスタンスどのマイクロ サービスに関係なく、更新プログラムを適用されている、ときに、一貫したバージョンを表示するようにします。

そのため、マイクロ サービス アプリケーションでは、モノリシック アプリケーション経由で多くのメリットがあります。

-   各マイクロ サービスは、比較的小さな、進化の管理に簡単です。
-   各マイクロ サービスの開発方法およびその他のサービスから独立してデプロイします。
-   各マイクロ サービス スケール アウトされた個別にできます。 たとえば、カタログ サービスとショッピング バスケット サービスは、受注サービスを超えるスケール アウトする必要があります。 そのため、スケール アウトする際、結果として得られるインフラストラクチャはリソースを消費より効率的にします。
-   各マイクロ サービスは、すべての問題を分離します。 たとえば、サービスで問題がある場合にだけ影響するサービス。 その他のサービスは、要求の処理を続行できます。
-   各マイクロ サービスは、最新のテクノロジを使用できます。 マイクロ サービスは自律的であり実行サイド バイ サイドであるため、最新のテクノロジとフレームワークができます、強制的にモノリシック アプリケーションで使用することが以前のフレームワークを使用するのではなく。

ただし、マイクロ サービス ベースのソリューションでは、潜在的な欠点もあります。

-   アプリケーションをマイクロ サービスをパーティション分割する方法を選択すると、各マイクロ サービスが完全に自律的、エンド ツー エンド、そのデータ ソースに対する責任を含む、困難ことができます。
-   開発者は、複雑さと待機時間をアプリケーションに追加するサービス間の通信を実装する必要があります。
-   通常、複数のマイクロ サービス間のアトミック トランザクションは、行うことができません。 そのため、ビジネス要件では、マイクロ サービス間の最終的な整合性を採用する必要があります。
-   運用環境で、多くの独立したサービスの侵害されたシステムの管理の展開および運用の複雑さがあります。
-   マイクロ サービスへのクライアントへの直接的な通信によりようにマイクロ サービスのコントラクトのリファクタリングが困難です。 たとえば、時間の経過と共に、システムがサービスにパーティション分割方法必要がありますを変更します。 1 つのサービスを 2 つ以上のサービスに分割して、2 つのサービスがマージ可能性があります。 クライアントは、マイクロ サービスと直接通信、ときに、このリファクタリング作業は、クライアント アプリとの互換性を中断できます。

## <a name="containerization"></a>コンテナー詰め

コンテナリゼーションは、これでアプリケーションと依存関係、および配置マニフェストのファイルとして抽象化の環境の構成のバージョン管理されたパッケージにまとめられたのユニットとしてテスト、コンテナー イメージとしてソフトウェア開発へのアプローチとホストのオペレーティング システムにデプロイされます。

コンテナーとは、分離された、リソース制御、およびポータブル オペレーティング環境、アプリケーションが他のコンテナーまたはホストのリソースに触れることがなく実行できます。 そのため、コンテナーが検索され、新しくインストールされた物理コンピューターまたは仮想マシンのように機能します。

コンテナーと仮想マシンの場合は、多くの類似点がある図 8-3 に示すようにします。

![](containerized-microservices-images/containersvsvirtualmachines.png "マイクロ サービス アプリケーションのスケーリング方法")

**図 8-3**:Virtual machines とコンテナーの比較

コンテナーは、オペレーティング システムを実行するには、ファイル システムが、および場合と、物理または仮想マシンがネットワーク経由でアクセスできます。 ただし、テクノロジ、およびコンテナーで使用される概念では仮想マシンとは大きく異なります。 仮想マシンには、アプリケーション、必須の依存関係、および完全なゲスト オペレーティング システムが含まれます。 コンテナーは、アプリケーションとその依存関係が含まれますが、他のコンテナー (コンテナーごとの特別な仮想マシン内で実行される HYPER-V コンテナー) とは別のホスト オペレーティング システムでは、分離されたプロセスとして実行されているオペレーティング システムと共有します。 そのため、コンテナーは、リソースを共有し、通常の仮想マシンよりも少ないリソースが必要です。

コンテナー指向の開発とデプロイ方法の利点は、一貫性のない環境のセットアップとそれに付随する問題に起因する問題のほとんどがなくなることです。 さらに、コンテナーは、必要に応じて新しいコンテナーをインスタンス化して高速なアプリケーションのスケール アップ機能を許可します。

コンテナーの作成と操作時に、主要な概念は次のとおりです。

-   コンテナー ホスト:物理マシンまたは仮想マシンのコンテナーをホストするように構成します。 コンテナー ホストは、1 つまたは複数のコンテナーで実行されます。
-   コンテナー イメージ:イメージは、相互に積み重ねられたファイル システムを階層型の和集合から成る、コンテナーの基礎です。 イメージには、状態はありません。 とは別の環境に展開された変更しません。
-   コンテナー:コンテナーは、イメージのランタイム インスタンスです。
-   コンテナー OS イメージ:コンテナーは、イメージからデプロイされます。 コンテナーのオペレーティング システム イメージは、コンテナーを構成する可能性のある多くのイメージ レイヤーの最初のレイヤーです。 コンテナーのオペレーティング システムは変更できないと、変更ことはできません。
-   コンテナー リポジトリ:コンテナー イメージが作成されるたびに、イメージとその依存関係は、ローカル リポジトリに格納されます。 コンテナー ホストでは、これらのイメージを何度も再利用できます。 コンテナー イメージも格納できる、パブリックまたはプライベート レジストリになど[Docker Hub](https://hub.docker.com/)、別のコンテナー ホスト間で使用できるようにします。

企業はベースのアプリケーション、マイクロ サービスを実装して、Docker はほとんどのソフトウェア プラットフォームやクラウドのベンダーによって採用された標準的なコンテナーの実装になったときに、ますますコンテナー採用することです。

EShopOnContainers 参照アプリケーションは、図 8-4 に示すように、コンテナー化の 4 つのバック エンド microservices をホストするのに Docker を使用します。

![](containerized-microservices-images/microservicesarchitecture.png "eShopOnContainers 参照アプリケーションのバックエンド マイクロ サービス")

**図 8-4**: eShopOnContainers 参照アプリケーションのバックエンド マイクロ サービス

参照アプリケーションのバックエンド サービスのアーキテクチャは、連携する複数のマイクロ サービスとコンテナーの形式で複数の自律的なサブシステムに分解されます。 各マイクロ サービスの機能の 1 つの領域を提供します。 id サービスやカタログ サービス、受注サービス、バスケット サービス。

各マイクロ サービスは、独自のデータベースは、他のマイクロ サービスから完全に切り離すことすることができます。 必要に応じて、アプリケーション レベルのイベントを使用して別のマイクロ サービスからのデータベース間の整合性が実現されます。 詳細については、次を参照してください。[マイクロ サービス間通信](#communication_between_microservices)します。

詳細については、参照アプリケーションは、次を参照してください。 [.NET マイクロ サービス。Architecture for Containerized .NET Applications](https://aka.ms/microservicesebook)」(.NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ) を参照してください。

<a name="communication_between_client_and_microservices" />

## <a name="communication-between-client-and-microservices"></a>クライアントとマイクロ サービス間の通信

EShopOnContainers のモバイル アプリがバック エンドのコンテナー化されたマイクロ サービスを使用して、通信*マイクロ サービスへのクライアントを直接*通信で、図 8-5 が表示されます。

![](containerized-microservices-images/directclienttomicroservicecommunication.png "マイクロ サービス アプリケーションのスケーリング方法")

**図 8-5**:クライアントからマイクロサービスへの直接通信

マイクロ サービスへのクライアントへの直接の通信でモバイル アプリは、パブリック エンドポイントをマイクロ サービスごとに異なる TCP ポートで使用して直接各マイクロ サービスを要求します。 運用環境で、エンドポイントは、使用可能なインスタンス間で要求を分散するマイクロ サービスのロード バランサーに通常マップ。

> [!TIP]
> API ゲートウェイの通信を使用してください。 マイクロ サービスへのクライアントへの直接的な通信は、ベースのアプリケーションで大規模で複雑なマイクロ サービスの構築は小規模なアプリケーションの複数の適切なときに欠点を持つことができます。 ベースのマイクロ サービスの数十のアプリケーションを大規模なマイクロ サービスの設計時に、API ゲートウェイの通信の使用を検討します。 詳細については、次を参照してください。 [.NET マイクロ サービス。Architecture for Containerized .NET Applications](https://aka.ms/microservicesebook)」(.NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ) を参照してください。

<a name="communication_between_microservices" />

## <a name="communication-between-microservices"></a>マイクロ サービス間の通信

マイクロ サービス ベースのアプリケーションは、複数のコンピューターで実行されている可能性、分散システムです。 通常、各サービス インスタンスはプロセスです。 そのため、サービスは、HTTP、TCP、Advanced Message Queuing Protocol (AMQP)、各サービスの性質によって、バイナリ プロトコルなど、プロセス間通信プロトコルを使用して対話する必要があります。

マイクロ サービスへのマイクロ サービスの通信の 2 つの一般的なアプローチは、データ、および軽量な非同期メッセージングの更新プログラムを複数のマイクロ サービス間で通信するときにクエリを実行するときに、HTTP ベースの REST 通信です。

非同期メッセージングに基づいてイベント ドリブンの通信は、複数のマイクロ サービス間で変更を反映するときに重要です。 このアプローチでは、マイクロ サービスは、何か重要なときの動作、たとえば、ビジネス エンティティを更新するときにイベントを発行します。 その他のマイクロ サービスは、これらのイベントをサブスクライブします。 次に、マイクロ サービスが、イベントを受け取ると、公開されるイベントの詳細をさらに生じる可能性があります、独自のビジネス エンティティを更新します。 これは、パブリッシュ/サブスクライブ機能、イベント バスは、通常により実現されます。

イベント バスは、図 8-6 に示すように、互いを明示的に認識するコンポーネントを必要とせず、マイクロ サービス間の通信の発行-サブスクライブします。

![](containerized-microservices-images/eventbus.png "パブリッシュ/サブスクライブ イベント バスを")

**図 8-6:** パブリッシュ/サブスクライブ イベント バスを

アプリケーションの観点からに、イベント バスは単に発行-サブスクライブ チャンネル インターフェイス経由で公開されています。 ただし、イベント バスを実装する方法が異なることができます。 たとえば、イベント バスの実装では、RabbitMQ や Azure Service Bus、NServiceBus、MassTransit など他のサービス バスを使用できます。 図 8-7 では、eShopOnContainers 参照アプリケーションでイベント バスを使用する方法を示します。

![](containerized-microservices-images/microservicesarchitecturewitheventbus.png "参照アプリケーションで非同期イベント ドリブンの通信")

**図 8-7:** 参照アプリケーションで非同期イベント ドリブンの通信

EShopOnContainers イベント バスは、RabbitMQ を使用して実装では、1 対多非同期パブリッシュ/サブスクライブ機能を提供します。 これは、イベントを発行した後があること、同じイベントをリッスンしている複数のサブスクライバーを意味します。 図 8-9 では、この関係を示します。

![](containerized-microservices-images/eventdrivencommunication.png "一対多の通信")

**図 8-9**:一対多の通信

この一対多の通信方法は、サービス間の最終的な整合性の確保、複数のサービスにまたがるビジネス トランザクションを実装するのにイベントを使用します。 最終的な整合性のトランザクションは、一連の分散の手順で構成されます。 そのため、ユーザー プロファイルのマイクロ サービスは、UpdateUser コマンドを受信すると、そのデータベース内のユーザーの詳細を更新し、UserUpdated イベントをイベント バスに発行します。 このイベントを受信し、応答で、それぞれのデータベースで、購入者の情報を更新するバスケット マイクロ サービスと、注文マイクロ サービスの両方がサブスクライブしています。

> [!NOTE]
> EShopOnContainers イベント バスは、RabbitMQ を使用して実装の目的は、概念実証としてのみ使用します。 実稼働システムでは、別のイベント バス実装を検討してください。

イベント バスの実装については、次を参照してください。 [.NET マイクロ サービス。Architecture for Containerized .NET Applications](https://aka.ms/microservicesebook)」(.NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ) を参照してください。

## <a name="summary"></a>まとめ

マイクロ サービスは、アプリケーションの開発と最新のクラウド アプリケーションの機敏性、スケール、および信頼性の要件に適した展開するためのアプローチを提供します。 できますであるスケール アウトされた個別に、つまり、特定の機能領域はスケールされることが必要な処理能力やネットワーク帯域幅の領域を不必要にスケーリングすることがなく、要求をサポートするためにマイクロ サービスの主な利点の 1 つです。要求の増加が発生していないアプリケーションです。

コンテナーとは、分離された、リソース制御、およびポータブル オペレーティング環境、アプリケーションが他のコンテナーまたはホストのリソースに触れることがなく実行できます。 企業はベースのアプリケーション、マイクロ サービスを実装して、Docker はほとんどのソフトウェア プラットフォームやクラウドのベンダーによって採用された標準的なコンテナーの実装になったときに、ますますコンテナー採用することです。


## <a name="related-links"></a>関連リンク

- [(2 Mb の PDF) 電子ブックをダウンロードします。](https://aka.ms/xamarinpatternsebook)
- [eShopOnContainers (GitHub) (サンプル)](https://github.com/dotnet-architecture/eShopOnContainers)
