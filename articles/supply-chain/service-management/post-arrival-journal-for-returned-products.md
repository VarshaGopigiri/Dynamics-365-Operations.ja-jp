---
title: "返品された製品の着荷仕訳を転記"
description: "返品された製品の着荷仕訳を転記します。"
author: YuyuScheller
manager: AnnBe
ms.date: 05/01/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: WMSArrivalOverview
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
ms.openlocfilehash: cbe60846f0a16b5061349d9960c49bb5310bd6f9
ms.contentlocale: ja-jp
ms.lasthandoff: 05/08/2018

---


# <a name="post-arrival-journal-for-returned-products"></a>返品された製品の着荷仕訳を転記 

[!include [banner](../includes/banner.md)]


返品を処理するには、まず返品数量を確認し、着荷仕訳帳の数量フィールドを更新します。 次に、廃棄コードを選択するか、返品品目の検査が必要であることを示します。 これらの手順を完了したら、返品注文の着荷仕訳帳を転記できます。

1.  **在庫管理** \> **定期処理** \> **着荷の概要**の順にクリックします。

2.  **設定名**フィルターで、**返品注文**を選択します。

3.  入庫の一覧が長い場合は、**範囲**領域のフィールドを使用して一覧を絞り込みます。

4.  転記する返品注文の明細行を検索し、**着荷に関する選択**ボックスをオンにして、**着荷開始**をクリックします。

5.  **仕訳帳** \> **入庫の着荷の表示**をクリックして、**在庫場所仕訳帳**フォームを開きます。
    

    > [!TIP]
    > <P>詳細情報を表示するには、仕訳帳を選択し、<STRONG>明細行</STRONG>をクリックします。</P>


6.  必要な更新を行い、**転記**をクリックします。

仕訳帳が転記された後、返品品目は在庫に登録され、品目が倉庫に到着したことが**返品注文**フォームに示されます。

## <a name="see-also"></a>参照

[在庫場所仕訳帳 (フォーム)](https://technet.microsoft.com/en-us/library/aa584822\(v=ax.60\))

  



