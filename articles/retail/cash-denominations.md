---
title: "POS の現金貨幣単位をコンフィギュレーションします。"
description: "紙幣および硬貨の現金貨幣単位は、POS 内で店舗のレジ担当者、店員およびマネージャーにより使用されるバック オフィスで定義できます。"
author: jblucher
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
ms.search.form: RetailStoreTable, RetailStoreCashDeclarationTable
audience: Application User
ms.reviewer: josaw
ms.search.scope: Core, Operations, Retail
ms.custom: 16231
ms.assetid: f28a827c-3a50-4d5e-83eb-e5a768db70a1
ms.search.region: global
ms.search.industry: Retail
ms.author: jeffbl
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0, Retail July 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 2771a31b5a4d418a27de0ebe1945d1fed2d8d6d6
ms.openlocfilehash: afe7c359f284fde10ada377fb19add9819a8dd21
ms.contentlocale: ja-jp
ms.lasthandoff: 11/03/2017

---

# <a name="configure-cash-denominations-for-pos"></a>POS の現金貨幣単位をコンフィギュレーションします。

[!include [banner](includes/banner.md)]

紙幣および硬貨の現金貨幣単位は、POS 内で店舗のレジ担当者、店員およびマネージャーにより使用されるバック オフィスで定義できます。 これらの貨幣単位は、営業終了時の支払/入金申告、または売上の簡単な支払/入金の現金計算をする助けとして使用できます。

## <a name="define-denominations"></a>貨幣単位の定義
貨幣単位は店舗ごとに **設定** > **店舗プロパティからの現金申告オプション** ページで設定されます。 

![現金貨幣単位](./media/image1-denomination.png)

貨幣単位を定義する方法:
1. [新規] をクリックします。
1. 種類 (硬貨または紙幣) を指定します。
1. 金額 (値) を指定します。

![現金貨幣単位](./media/image2-denomination.png)

## <a name="configure-the-functionality-profile"></a>機能プロファイルのコンフィギュレーション
POS での現金による支払の際、ユーザーは、顧客によって支払われた金額をすばやく入力するため紙幣の通貨単位を使用できます。 機能プロファイルで、POSで貨幣単位を表示するための 2 つのオプションをコンフィギュレーションできます。

**合計金額以上**: 既定では、POS は未払い金額より多い紙幣の通貨単位のみを表示し、ワンタッチの支払/入金をできるようにします。 たとえば、請求額が $7.50 の場合、POS は次の通貨単位を表示します: $10、$20、$50、および $100。 これらの金額のいずれかにタッチすると、自動的にその金額に対する売上の支払/入金をします。 $1 および $5 紙幣、これらの金額は、請求額よりも少ないため表示されません。

**すべての貨幣単位**: 請求額に関係なく、POS で常にすべての紙幣の貨幣単位を表示するため、このオプションを選択します。 つまり、ユーザーは請求額に達する紙幣の組み合わせを使用できます。 たとえば、請求額が $25.00 の場合は、ユーザーは $20 よび $5 を選択して販売を完了できます。

