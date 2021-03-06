---
title: "倉庫作業者の管理"
description: "この記事では、倉庫の従業員によって実行される作業の管理と監視に、Dynamics 365 for Finance and Operations を使用する方法について説明します。"
author: perlynne
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: HcmWorker, InventLocation, WHSLaborStandards, WHSWorker, WHSWorkTable, WHSWorkTableListPage
audience: Application User
ms.reviewer: bis
ms.search.scope: Core, Operations
ms.custom: 72891
ms.assetid: feaa6f15-49d2-41f5-9b87-453463c52e4e
ms.search.region: Global
ms.author: perlynne
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: a0739304723d19b910388893d08e8c36a1f49d13
ms.openlocfilehash: 211ced007e7729265621a05c2162a228eb0023c2
ms.contentlocale: ja-jp
ms.lasthandoff: 03/26/2018

---

# <a name="manage-warehouse-workers"></a>倉庫作業者の管理

[!include [banner](../includes/banner.md)]

この記事では、倉庫の従業員によって実行される作業の管理と監視に、Microsoft Dynamics 365 for Finance and Operations を使用する方法について説明します。

倉庫管理で機能を使用すると、すべての倉庫作業員の工程は*作業*呼ばれます。 ピッキング、移動、および手持在庫の棚卸などの作業は、モバイル デバイスを使用して記録されます。 倉庫作業者が作業を実行する前に、作業者は人事管理の作業者と関連付けられる必要があります。 各**作業者**のアカウントは、関連付けられる複数の倉庫のユーザーが使用できます。 これらの作業ユーザーは異なる倉庫で、異なるレベルのさまざまなモバイル デバイス メニューへのアクセスを使用できます。 倉庫の作業ユーザーを、選択した作業者に対しての複数のログオンとして考えることができます。 各作業ユーザーには既定の倉庫があり、作業ユーザーに利用可能なメニュー項目によって特定のワークフローが公開されます。 

新たな作業ユーザーを作成する場合は、**倉庫**セクションの、**一般**タブの、**作業者**ページで、**作業者**をクリックします。 ユーザー ID、ユーザー名、既定の倉庫、およびメニュー名を指定する必要があります。 倉庫モバイル デバイス ポータルにユーザーがサインインするとき、このメニューが読み込まれ、どのメニュー項目へユーザーがアクセスできるかを定義できます。 

各作業ユーザーの設定の一部として、特定のワークフロー プロセスも定義できます。 たとえば、**循環棚卸の監督ですか**フィールドを使用して、ユーザーが棚卸の工程中に循環棚卸の不一致の調整を処理できるか、または、これらの調整を別のユーザーが最初に確認するべきかを指定できます。

## <a name="defining-labor-standards"></a>労務標準の定義
**労務標準**ページで、システムが特定のタイプの作業が必要とする見積時間の計算に使用する計算方法を定義できます。 この定義は、一般レベルまたは特定のレベルで設定できます。 たとえば、特定のピッキング プロセスが使用されるとき、特定の定義単位重量あたりの、販売注文のピッキング処理をするために必要な時間を定義できます。 同時に、ピッキング済の手持在庫のプット工程を、別の計算方法に基づいて記録できます。 

ユーザー定義の労務標準を有効にするには、労務標準を使用する各倉庫の**労務標準の許可**オプションを選択する必要があります。

## <a name="monitoring-and-controlling-warehouse-work"></a>倉庫作業の監視および制御
**すべての作業**ページで、計画された、処理中の、および完了したすべての作業を監視および管理することができます。 このページで、倉庫のユーザーの割り当ておよび作業優先順位のさまざまなプロセスを更新できます。 予定あるいは完成作業プロセスを理解するために、作業ヘッダーおよび作業明細行に関連付けられた詳細にドリルダウンすることもできます。 

**労務標準**オプションを有効にすると、作業の計算された見積時間を確認できます。 その後、作業を処理する場合、各作業の実際の時間も示されます。 これにより、実際の時間と見積時間を比較できます。 

また、作業の作成時に自動的に作業を分割するルールで見積時間を使用できます。 これにより、タスクを完了する予想時間に基づいて、負荷分散作業をすることができます。 

作業項目の処理に使用される時間の分析は、倉庫作業員の効率の改善に役立ちます。 次のレポートがこの分析に使用できます:

-   **ユーザー別の労務** – このレポートは、予想時間に対して、実際の時間に基づいて作業者の生産性を表示します。
-   **作業トランザクション タイプ別の労務** – 特定の倉庫プロセスの非能率性を調査するのに、このレポートを使用できます。 たとえば、移動オーダーのピッキングが、今週は前の週よりも長い時間がかかっていることに気づきます。 詳細な調査に対してこの情報を使用できます。





