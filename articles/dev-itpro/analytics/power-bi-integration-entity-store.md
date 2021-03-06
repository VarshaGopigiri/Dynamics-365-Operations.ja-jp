---
title: "エンティティ ストアとの Power BI の統合"
description: "エンティティ格納は、Microsoft Dynamics 365 for Finance and Operations に含まれている運用データ ストアです。 このトピックでは、エンティティ ストアで Power BI を Finance and Operations と統合する方法について説明します。"
author: MilindaV2
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
ms.search.form: BIMeasurementDeployManagementEntityStore
audience: IT Pro
ms.reviewer: sericks
ms.search.scope: Core, Operations
ms.custom: 265974
ms.assetid: 434b5d9f-9877-4769-ad96-d4e8d460a7fa
ms.search.region: Global
ms.author: milindav
ms.search.validFrom: 2016-05-31
ms.dyn365.ops.version: Platform update 1
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 22ae0aef14086d06be32f88495a25a96cfb32850
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="overview-of-power-bi-integration-with-entity-store"></a>エンティティ ストアとの Power BI の統合

[!include [banner](../includes/banner.md)]

エンティティ格納は、Microsoft Dynamics 365 for Finance and Operations に含まれている運用データ ストアです。 このトピックでは、エンティティ ストアで Power BI を Finance and Operations と統合する方法について説明します。

エンティティ格納は、Microsoft Dynamics 365 for Finance and Operations に含まれている運用データ ストアです。 エンティティ格納の機能は、Microsoft Dynamics AX プラットフォーム更新プログラム 1 (2016 年 5 月) リリースで導入されました。 この機能を使用すると、管理者またはパワーユーザーは、レポートおよび分析用の専用データストアで測定値を公開できます。 (集計の測定は、エンティティを使用してモデル化されたスター スキーマです)。このデータ ストアをエンティティ格納と呼びます。 レポート用に最適化されたデータベースです。 エンティティ格納では、Microsoft SQL Server に組み込まれたメモリ内の集合縦棒ストア インデックス (CCI) 機能を使用して、レポートとクエリを最適化します。 顧客は、Microsoft Power BI の DirectQuery モデルをエンティティ格納と共に使用し、大量のデータに対して大量のほぼリアルタイムの分析レポートを有効にすることができます。

## <a name="power-bi-directquery-mode"></a>Power BI DirectQuery モード
Microsoft Dynamics AX の 2016 年 2 月のリリースでは、データ エンティティ (集計データのエンティティと、詳細または通常のデータ エンティティの両方) で公開される OData エンドポイントを使用して Power BI レポートを作成することができました。 この方法は引き続き Dynamics 365 for Operations でサポートされていますが、エンティティ格納でも Power Users は Power BI DirectQuery レポートを作成できます。

[![DirectQuery モード](./media/entity-store-architecture-1024x587.jpg)](./media/entity-store-architecture.jpg) 

前の図に示すように、DirectQuery はエンティティ格納で直接レポートを実行するレポート モードです。 このレポート モードでは、データは Power BI のキャッシュにステージングされません。 このモードでは、2 つの直接的な利点があります。

-   大量のデータに対して Power BI レポートを作成することができます。
-   レポートは、Power BI を使って更新する必要がなくなります。 エンティティ格納が更新されると、レポートに最新のデータが反映されます。

また、Power BI サービスにキャッシュされるデータがないため、データは、Dynamics 365 for Finance and Operations の環境から離れません。

## <a name="stage-aggregate-measurements-in-entity-store"></a>エンティティ格納における集計測定のステージング
集計測定は分析シナリオのためにモデル化されたスター スキーマです。 2016 年 2 月のリリースでは、リアルタイムなメモリ内集計の測定が有効になりました。 リアルタイムの集計測定を使用することにより、データのリアルタイム操作に対応する埋め込みチャートおよび主要業績評価指標 (KPI) を有効にすることができます。 詳細については、[メモリ内リアルタイム集計モデルによる SSAS キューブの置換](../migration-upgrade/in-memory-real-time-aggregate-models.md) を参照してください。 リアルタイム集計測定は、インメモリの非クラスター化縦棒ストア インデックス (NCCI) の技術を活用します。 リアルタイムの集計の測定で作成されたビジュアルおよび集計計算に数秒以内のトランザクションが反映されます。 プラットフォーム更新プログラム 1 (2016 年 5 月) のリリースでは、エンティティ格納でステージングできる集計測定を有効にしました。 エンティティ ストアで実施された集計測定は、Power BI を使用して大量のデータを調べる必要がある、ほぼリアルタイムの分析シナリオで使用できます。 開発者は、[モデリングおよび集計データを使用して](model-aggregate-data.md) 集計の測定でリアルタイム分析をモデル化する方法について学びました。 プラットフォーム更新プログラム 1 (2016 年 5 月) のリリースでは、エンティティ格納でステージングできる集計測定をモデル化する機能も追加しました。 Microsoft Visual Studio で、**StagedEntityStore** を集計の測定の用途プロパティとして指定します。 この新しいプロパティは、2016 年 5 月で追加されました。 以前は、**InMemoryRealTime** は用途プロパティとして使用できました。 

[![Visual Studio にある新しい StagedEntityStore の使用プロパティ](https://msdnshared.blob.core.windows.net/media/2016/06/New-usage-property-in-VS-300x242.png)](https://msdnshared.blob.core.windows.net/media/2016/06/New-usage-property-in-VS.png) 

ただし、ステージングできるように集計測定をモデル化するのはなぜかと疑問に思われるかもしれません。 メモリ内リアルタイム集計測定を常に使用しないのはなぜですか。 **StagedEntityStore** パターンを使用する理由はいくつかあります。

-   調査して分析する必要がある、大量のデータが存在する可能性があります。
-   コード アップグレード プロセスの一部として Microsoft Dynamics AX 2012 R3 から Dynamics 365 for Finance and Operations に移行する解析プロジェクト (つまり、キューブ) を所持する場合があります。 スキーマには複雑なビューと結合が存在するため、クエリ応答時間は埋め込まれたビジュアルには受け入れられない場合があります。 ただし、NCCI テクノロジーを直ちに活用するためにビジュアルをリファクタリングする必要はありません。
-   運用データベースのスキーマとは異なり、エンティティ ストアのスキーマは特にレポートのためにモデル化されています。 したがって、エンティティ ストアのスキーマから新しいレポートを作成する方がはるかに簡単です。
-   自分のシナリオが、操作の数秒以内での分析データの更新を必要としない場合があります。 データ検索を有効にするために構築されているほとんどの Power BI レポートは、このカテゴリに分類されます。 約 10 分でデータをリフレッシュすることがシナリオで許容される場合は、段階的なパターンを使用する場合があります。

上記の理由のいずれかによってユーザーの状況がカバーされる場合、エンティティ店舗で集計測定を実行し、Power BI 統合に対して使用する必要があります。

## <a name="update-entity-store"></a>エンティティ店舗の更新
クライアントで、**エンティティ格納**ページは**システム管理** &gt; **設定** &gt; **エンティティ格納**で表示できます。 

[![エンティティ格納ページ](./media/entity-store-form-1024x548.jpg)](./media/entity-store-form.jpg) 

このページには、集計の測定の一覧が含まれています。 これらの集計測定はエンティティ格納内で実施することができます。 開発者で、アプリケーション オブジェクト ツリー (AOT) で使用できる集計測定に関する知識があれば、なぜ一部の集計測定値がここに表示されないのか疑問に思われるかもしれません。 AX 2012 R3 (つまり、アップグレード プロセスの一部として移行された SQL Server Analysis Service プロジェクト) から移行した測定値を集計する場合は、開発者が用途プロパティを **StagedEntityStore** に変更するまで展開できません。 この動作は意図的です。 集計の測定に影響を与える一般的なアップグレードの問題のいくつかを取り込むことを目的とする、ベスト プラクティスの警告とエラーを有効にしました。 ほぼリアルタイムな (NCCI) モードを使用する場合は、ベスト プラクティスのエラーや警告を修正する必要があります。 2016 年 5 月の更新時点で、管理者は**エンティティ格納**ページで**更新**をクリックして定期更新をスケジュールする必要があります。 **更新** ボタンを使用すると、以下の図に示すように、1 回限りの更新 (つまり、デモ) または定期的な更新のスケジュールを実行することができます。 

[![ダイアログ ボックスの更新構成](./media/retail-cube-refresh-1024x548.jpg)](./media/retail-cube-refresh.jpg) 

バッチ フレームワークはスケジューリングに使用されます。 したがって、更新ジョブは、バッチ フレームワークの機能を使用して監視、負荷分散、優先順位付けを行うことができます。 2016 年 5 月更新時点では、完全な更新プログラムのみがサポートされます。 ただし、まもなく差分更新が有効化されます。 最終的には、将来の更新プログラムにおいて、システムが実際の使用パターンに基づくエンティティ格納が更新されます。 したがって、管理者は **更新のコンフィギュレーション** ダイアログ ボックスを例外としてのみ使用する必要があります。




