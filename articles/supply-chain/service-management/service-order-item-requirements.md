---
title: "サービス注文品目の要件"
description: "サービス注文に特定の品目を引き当てる必要がある場合、その在庫品目要求を作成できます。"
author: YuyuScheller
manager: AnnBe
ms.date: 05/01/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: ProjSalesItemReq
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Core, Operations
ms.custom: 
ms.assetid: 
ms.search.region: Global
ms.author: YuyuScheller
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: efcb77ff883b29a4bbaba27551e02311742afbbd
ms.openlocfilehash: 880d41a5b3d8c9200a0a1f4b13af2d6d24d30766
ms.contentlocale: ja-jp
ms.lasthandoff: 05/08/2018

---

# <a name="service-order-item-requirements"></a>サービス注文品目の要件   

[!include [banner](../includes/banner.md)]


顧客に提供するサービスを追跡および管理するサービス注文を作成できます。 サービス注文に特定の品目を引き当てる必要がある場合、その在庫品目要求を作成できます。 品目要求を在庫からすぐ消費したり、その品目の製造オーダーを開始できます。

品目トランザクションではなく在庫品目要求を使用することによって、品目が実際に使用される直前の配送を計画したり、発注書を作成したり、品目を売買契約の枠組みに含めたり、在庫品目要求を生産計画に含めたりすることができます。

サービス注文に関する要求はプロジェクトを通じて処理します。 サービス注文に対して在庫品目要求を作成するには、サービス注文をプロジェクトに関連付ける必要があります。

サービス注文に対して作成された在庫品目要求は、個々のサービス注文の**プロジェクト**から、または**販売注文**フォームを使用して表示できます。

## <a name="view-an-item-requirement-from-a-service-order"></a>サービス注文からの在庫品目要求の表示

1.  **サービス管理** \> **共通** \> **サービス注文** \> **サービス注文**の順にクリックします。

2.  **派遣**をクリックし、**在庫品目要求**をクリックして**在庫品目要求**フォームを開きます。

3.  **プロジェクト**タブをクリックし、**サービス注文**フィールドで在庫品目要求のサービス注文を確認します。

## <a name="delete-service-orders-with-item-requirements"></a>在庫品目要求を含むサービス注文の削除

サービス注文に対して在庫品目要求が作成されている場合は、サービス注文を削除できません。 サービス注文を削除する前に、在庫品目要求を削除する必要があります。

1.  **サービス管理** \> **共通** \> **サービス注文** \> **サービス注文**の順にクリックします。

2.  **派遣**をクリックし、**在庫品目要求**をクリックして**在庫品目要求**フォームを開きます。 このフォームに、サービス注文に対して作成されている在庫品目要求が一覧表示されます。

3.  削除する品目要求を選択し、**削除**をクリックします。

- または -

1.  **プロジェクト管理および会計** \> **共通** \> **プロジェクト** \> **すべてのプロジェクト**の順にクリックします。

2.  在庫品目要求が作成されているサービス注文を含むプロジェクトを開きます。

3.  **プロジェクト**フォームの右ウィンドウで、**在庫品目要求**をクリックします。 **在庫品目要求**フォームは、選択したプロジェクトに関連付けられている在庫品目要求を一覧表示します。

4.  削除する品目要求を選択し、**削除**をクリックします。

## <a name="see-also"></a>参照

[在庫品目要求 (フォーム)](https://technet.microsoft.com/en-us/library/aa552021\(v=ax.60\))


