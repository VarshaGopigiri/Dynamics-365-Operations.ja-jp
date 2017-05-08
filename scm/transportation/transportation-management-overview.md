---
title: "輸送管理の概要"
description: "このトピックでは、Microsoft Dynamics 365 for Operations の配送管理機能の概要が示されます。"
author: YuyuScheller
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
audience: Application User
ms.search.scope: AX 7.0.0, Operations, Core
ms.custom: 30251
ms.assetid: d4e3550c-bca8-469c-82df-56ac0083e4ac
ms.search.region: Global
ms.author: yuyus
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: 9ccbe5815ebb54e00265e130be9c82491aebabce
ms.openlocfilehash: 3136fd95c4c56495a391668d6c854a6ae1e36479
ms.lasthandoff: 03/31/2017


---

# <a name="transportation-management-overview"></a>輸送管理の概要

[!include[banner](../includes/banner.md)]


このトピックでは、Microsoft Dynamics 365 for Operations の配送管理機能の概要が示されます。

輸送管理では、会社の配送の管理および送受信オーダーのベンダーとルート指定の解決策の識別を使用できるようになります。 たとえば、出荷用の最速のルートまたは最低費用レートを識別できます。 次の表では、Microsoft Dynamics 365 for Operations で輸送管理を使用する主要なシナリオについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>シナリオ</th>
<th>輸送管理が役立つ方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>配送活動に外部物流プロバイダを使用します。</td>
<td>入庫または出庫輸送に輸送管理を使用します。</td>
</tr>
<tr class="even">
<td>会社の固有フリートを、出荷または集配のために使用でき、配送料が顧客に渡されます。</td>
<td>出荷プロセスで、配送料を確認し、顧客に渡すために輸送管理を使用できます。 ただし、配送業者の請求書の調整プロセスは必要ではありません。</td>
</tr>
<tr class="odd">
<td>会社の固有フリートは、出荷または集配のために使用できますが、製品の価格に配送が含まれるため、配送料は顧客には渡されません。</td>
<td>多くの輸送管理機能は必要ではありません。 ただし、配送率を確認し、それに応じて販売価格を調整する場合、配送管理を使用できます。</td>
</tr>
<tr class="even">
<td>同じ会社の別の法人によって物流サービスが提供されます。</td>
<td><ul>
<li>その他の配送業者など、他の法人による処理によって輸送管理を使用できます。 法人間の経済取引を自動化することはできません。 そのため、これらのトランザクションを手動で処理する必要があります (発注書の作成など)。</li>
<li>物流サービスを提供する法人の場合でも、配送率を決定するために輸送管理を使用できます。</li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="planning-transportation-in-dynamics-365-for-operations"></a>Dynamics 365 for Operations の配送計画
輸送管理では、 輸送計画は注文またはその注文に基づいて作成された出荷に基づきます。 出荷は特定の時点で常に存在しますが、輸送計画に必要ではありません。 移動オーダーは出荷シナリオの一部で、販売注文と共に計画できます。 

![積荷図面](./media/Load-drawing1-1024x477.jpg)

## <a name="inbound-transportation"></a>入庫輸送
仕入先から品目を発注し、その品目を倉庫に配達する必要がある場合は、品目の輸送を自分で手配することができます。 入庫積荷の輸送および入庫の計画に、Dynamics 365 for Operations を使用できます。 次の図は、入庫積荷用の輸送を計画するための業務プロセス フローを示します。 

![積荷の入庫輸送の業務プロセス フロー](./media/Businessprocessflowforinboundloadtransportation.jpg)

## <a name="outbound-transportation"></a>出庫輸送
会社の倉庫から顧客に特定の品目を出荷する場合は、出荷積荷を計画および処理できます。 出荷積荷の輸送および出荷の計画に Dynamics 365 for Operations を使用できます。 次の図は、出荷用の出荷積荷を計画および処理するための業務プロセス フローを示します。 

![出庫積荷の計画および処理](./media/Planningandprocessingoutboundloads.jpg)

## <a name="load-building"></a>積荷構築
Dynamics 365 for Operations には、容積ベースの積荷構築戦略という積荷構築戦略が用意されています。 この戦略を使用すると、積荷テンプレートの高さと重量に対して指定される最大値を使用できるし、または新しい値を入力して設定を上書きできます。 この戦略を使用するには、[**積荷構築ワークベンチ**] ページの [**設定**] クイック タブの [**積荷構築戦略**] フィールドで戦略を選択します。 また、アプリケーション オブジェクト ツリー (AOT) で新しいクラスを作成して、独自の積荷構築戦略を追加できます。



