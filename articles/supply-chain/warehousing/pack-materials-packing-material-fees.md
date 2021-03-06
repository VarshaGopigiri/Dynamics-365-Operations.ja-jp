---
title: "梱包材および費用"
description: "梱包材費用は、一定の間隔でリサイクル会社に支払われます。 梱包単位を構成する各材料について、重量単位あたりの金額が支払われます。 梱包材費用は計算および報告されますが、所轄官庁に支払う必要がある税とは見なされないため、元帳トランザクションは転記されません。"
author: MarkusFogelberg
manager: AnnBe
ms.date: 11/02/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: InventPackagingGroup, InventPackagingMaterialCode, InventPackagingMaterialFee, InventPackagingMaterialTrans, InventPackagingMaterialTransPurch, InventPackagingUnit
audience: Application User
ms.reviewer: bis
ms.search.scope: Core, Operations
ms.custom: 2194
ms.assetid: 040b65dc-43c9-4256-b69f-b2d6e736fbe9
ms.search.region: Global
ms.search.industry: Distribution
ms.author: mafoge
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 2771a31b5a4d418a27de0ebe1945d1fed2d8d6d6
ms.openlocfilehash: b131cdfa2f0e3b6a8f116464323d49eaa4584634
ms.contentlocale: ja-jp
ms.lasthandoff: 11/03/2017

---

# <a name="packing-materials-and-fees"></a>梱包材および費用

[!include [banner](../includes/banner.md)]

梱包材費用は、一定の間隔でリサイクル会社に支払われます。 梱包単位を構成する各材料について、重量単位あたりの金額が支払われます。 梱包材費用は計算および報告されますが、所轄官庁に支払う必要がある税とは見なされないため、元帳トランザクションは転記されません。

梱包材の重量および費用は、販売注文明細行と購買注文明細行の両方で計算されます。

1 つの品目、品目の梱包グループ、またはすべての品目に対して、梱包単位を 1 つ以上定義できます。 梱包単位は、梱包材と、梱包材重量、および梱包単位に含まれる品目数から構成されます。 梱包材コードが、定義された梱包材の各タイプに割り当てられます。 梱包材コードに基づいて、指定した期間の価格を指定できます。 梱包材費用はこの情報に基づいて計算されます。

| **メモ**                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------|
| 梱包材費用を支払っていない会社でも、この機能を使用して、梱包材の重量の統計を計算できます。 |

## <a name="setup-requirements-for-packing-material-fees"></a>梱包材費用の要件の設定
梱包材重量、梱包材費用、またはその両方を計算する前に、次の基本データを作成する必要があります。

-   梱包グループ – 品目に割り当てる梱包グループを作成します。
-   梱包材コード – 定義された梱包材のタイプごとの梱包材コードを作成します。
-   梱包単位 – 1 つの品目、梱包グループ、またはすべての品目の梱包単位を指定します。 各梱包単位について、含める梱包材を定義し、重量を割り当て、[梱包単位係数] フィールドに、在庫単位から換算率を入力します。
-   梱包材費用 – 梱包材コードごとの梱包材費用を指定します。 各梱包材タイプについて、有効期間、材料あたりの価格、通貨、および単位を定義します。

## <a name="packing-units-on-sales-order-lines"></a>販売注文明細行の梱包単位
販売注文明細行を作成する際には、システムは、品目の梱包単位が指定されているかどうかを確認します。 梱包単位が指定されている場合、販売注文明細行が、指定された梱包単位と梱包単位数量で更新されます。 梱包単位数量は、選択された梱包単位に含まれる品目の数で分割された注文済数量に基づきます。 梱包単位が指定されていない場合は、梱包単位および梱包単位数量を手動で販売注文明細行に入力できます。 販売注文明細行を転記する際に、梱包単位および梱包単位数量を変更することもできます。 この変更が関係してくるのは、販売注文明細行の一部のみを出荷または請求する場合です。 販売注文の請求時に、梱包材トランザクションが作成されます。 梱包材トランザクションには、販売注文明細行の梱包材重量が含まれます。 トランザクションの請求後にそのトランザクションを変更して、新しいトランザクションを作成することもできます。

## <a name="packing-units-on-purchase-order-lines"></a>購買注文明細行の梱包単位
購買注文明細行の梱包材トランザクションは自動的には作成されません。 **梱包材の購買トランザクションの作成**ページで、請求済購買注文明細行に対するトランザクションを手動で作成します。

## <a name="set-up-customer-packaging-material-fee-license-numbers"></a>顧客の梱包材費用ライセンス番号の設定
顧客が梱包材費用を支払う場合は、**顧客**ページで顧客の梱包材費用ライセンス番号を指定します。 ライセンス番号が顧客に割り当てられている場合、販売注文が請求されるときに梱包材費用は自動的に計算されます。 請求後は、レポートの計算および印刷を行う必要がないため、**梱包材トランザクション** ページの [**手数料計算**] チェック ボックスがオフになります。 梱包材重量を請求書に印刷し、顧客が費用を支払うことを顧客に通知するように選択できます。 

法人が梱包材費用を支払う場合、顧客のライセンス番号を指定しないでください。 請求後は、**梱包材トランザクション** ページの [**手数料計算**] チェック ボックスが選択されます。 これにより、レポートが作成されるときに費用が計算されることが示されます。 請求書に重量を印刷し、法人が費用を支払うことを示すように選択できます。

## <a name="print-packaging-material-weights-on-invoices"></a>請求書への梱包材重量の印刷
請求書に、梱包材重量を印刷し、だれが梱包材費用を支払うかを示すように選択できます。 重量は、梱包コードごとに集計されます。






