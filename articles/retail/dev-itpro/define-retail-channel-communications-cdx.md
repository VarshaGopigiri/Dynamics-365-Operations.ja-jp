---
title: "小売チャンネル通信 (Commerce Data Exchange) の定義"
description: "このトピックでは、Commerce Data Exchange とそのコンポーネントの概要を示します。 ここでは、Microsoft Dynamics 365 for Retail と小売チャンネルとの間でのデータの転送で各コンポーネントが果たす役割について説明します。"
author: athinesh99
manager: AnnBe
ms.date: 11/14/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
audience: IT Pro
ms.reviewer: sericks
ms.search.scope: Core, Operations, Retail
ms.custom: 27021
ms.assetid: 179b1629-ac90-4cfb-b46a-5bda56c4f451
ms.search.region: global
ms.search.industry: Retail
ms.author: athinesh
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0, Retail July 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 29fbc3c844356df0bc415147168ee75c86b6a1f6
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="define-retail-channel-communications-commerce-data-exchange"></a>小売チャンネル通信 (Commerce Data Exchange) の定義

[!include [banner](../includes/banner.md)]

このトピックでは、Commerce Data Exchange とそのコンポーネントの概要を示します。 ここでは、Microsoft Dynamics 365 for Retail headquarters と小売チャンネルとの間でのデータの転送で各コンポーネントが果たす役割について説明します。

<a name="overview"></a>概要
--------

Commerce Data Exchange は、小売用バックオフィスと、オンライン ストア、実際の店舗などの小売チャンネルの間でデータを転送するシステムです。 小売チャンネルのデータを格納するデータベースは、小売りデータベースとは別にあります。 チャンネルのデータベースは、小売トランザクションに必要なデータのみ格納します。 マスター データが小売用バックオフィスでコンフィギュレーションされ、チャネルに配分されます。 トランザクション データは販売時点管理 (POS) システムまたはオンライン店舗で作成され、小売用バックオフィスにアップロードされます。 データ配送は非同期です。 つまり、データを収集してソースでパッケージングするプロセスは、データを取得して適用するプロセスとは別に行われます。 価格および在庫検索などのシナリオの場合、データはリアルタイムに取得する必要があります。 これらのシナリオをサポートするために、Commerce Data Exchange には、小売用バックオフィスとチャンネル間のリアルタイム通信を可能にするサービスが含まれます。 

[![更新済小売グラフィック](./media/updated-retail-graphic.png)](./media/updated-retail-graphic.png)  

## <a name="async-service"></a>非同期サービス
Retail データベースの Microsoft SQL Server 変更追跡は、チャネルに送信する必要のあるデータの変更内容を特定するのに使用されます。 配送スケジュールに基づいて、小売用バックオフィスはそのデータをパッケージングして中央の保存場所 (Azure blob storage) に保存します。 別のバッチ処理は、このデータ パッケージをチャンネルのデータベースに挿入するために Commerce Data Exchange: Async Client ライブラリを使用します。 

[![非同期サービス](./media/async-300x239.png)](./media/async.png)

### <a name="retail-scheduler"></a>小売用スケジューラ

スケジューラ ジョブとは、データを配送場所へ (から) 配送するためのメカニズムです。 ジョブは、配分するデータを含むテーブルおよびテーブル フィールドを指定するサブジョブで構成されます。 小売用バックオフィスには、ほとんどの組織のレプリケーションの要件を満たすサブジョブと定義済スケジューラ ジョブが含まれます。 次のタイプの定義済ジョブが作成されます。

-   **ダウンロード ジョブ** - ダウンロード ジョブは、小売用バックオフィスからチャネル データベースに変更されたデータを送信します。 レコードへの変更は、SQL Server 変更履歴によって追跡されます。
-   **アップロード ジョブ (P ジョブ)** – アップロード ジョブは、チャンネルから小売データベースへの販売トランザクションをプルします。 P ジョブは、データを漸増的にアップロードします。 P ジョブが実行されると、Async Client ライブラリが場所から既に受け取ったレコードに対するレプリケーション カウンターをチェックします。 レコードは、レプリケーション カウンターが検出された最大値を超える場合のみアップロードされます。 P ジョブは以前にアップロードされたデータを更新しません。

配送スケジュールは、手動または小売用バックオフィスでスケジューリングされたバッチ ジョブによるデータ転送の実行に使用されます。 配送スケジュールには、1 つ以上のチャンネル データ グループと 1 つ以上のスケジューラ ジョブを含めることができます。 スケジューラー・ジョブが円滑に実行されていることを確認するには、インスタンス用に構成された「既定の」データベース名を変更せず、2 番目のデータベースを作成しないでください。 非小売店舗スケール単位のすべてのデータベースは Microsoft により管理され、1 つの既定のデータベースのみが必要です。 

## <a name="realtime-service"></a>リアルタイム サービス
Commerce Data Exchange: Real-time Service は、小売用バックオフィスと小売チャンネル間のリアルタイム通信を提供する統合サービスです。 リアル タイム サービスにより、個々の POS コンピューターとオンライン ストアが小売用バックオフィスから特定のデータをリアルタイムで取得できるようになります。 ほとんどのキー操作はローカルのチャンネル データベースで実行できますが、次のシナリオは小売用バックオフィスに格納されているデータへの直接アクセスが必要です。

-   ギフトカードの発行および引換え
-   ロイヤルティ ポイントを引き換え
-   クレジット メモの発行および引換え
-   顧客レコードを作成または更新します
-   販売注文を作成、更新、完了しています
-   発注書または移動オーダーに対する在庫を入荷
-   棚卸資産会計の実行
-   店舗間から販売トランザクションを取得し、返品トランザクションを完了します

[![Real-time Service](./media/rts.png)](./media/rts.png) 

定義済の Real-time Service プロファイルが作成されます。

