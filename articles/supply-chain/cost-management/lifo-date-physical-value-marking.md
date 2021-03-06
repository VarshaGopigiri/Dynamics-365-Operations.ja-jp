---
title: "現物価格とマーキングを使用した LIFO 日付"
description: "後入れ先出し日付 (LIFO 日付) は、LIFO 原則に基づく在庫モデルです。 在庫からの出庫は、在庫トランザクションの日付に基づいて在庫への最後の入庫を対象として決済されます。 払出より前の入庫が存在しない場合、LIFO 日付を使用することで、払出の日付より後に発生する入庫を対象に払出が決済されます。 同じ日付の複数の払出は、最終払出、最後の受入の順に決済される場合があります。"
author: AndersGirke
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: InventJournalLossProfit, InventMarking, InventModelGroup, SalesTable
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Core, Operations, Retail
ms.custom: 51592
ms.assetid: d9f13274-3268-444f-85c8-b686fd39286d
ms.search.region: Global
ms.search.industry: Retail
ms.author: yuyus
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 2771a31b5a4d418a27de0ebe1945d1fed2d8d6d6
ms.openlocfilehash: 0b94d3f23c929c45a67894bd08706144c9226491
ms.contentlocale: ja-jp
ms.lasthandoff: 11/03/2017

---

# <a name="lifo-date-with-physical-value-and-marking"></a>現物価格とマーキングを使用した LIFO 日付

[!include [banner](../includes/banner.md)]

[!include [retail name](../includes/retail-name.md)]

後入れ先出し日付 (LIFO 日付) は、LIFO 原則に基づく在庫モデルです。 在庫からの出庫は、在庫トランザクションの日付に基づいて在庫への最後の入庫を対象として決済されます。 払出より前の入庫が存在しない場合、LIFO 日付を使用することで、払出の日付より後に発生する入庫を対象に払出が決済されます。 同じ日付の複数の払出は、最終払出、最後の受入の順に決済される場合があります。 

後入れ先出し日付 (LIFO 日付) の在庫モデルを使用すると、払出より前の入庫が存在しない場合、払出の日付より後に発生する入庫を対象に払出が決済されます。 同じ日付の複数の払出は、最終払出、最後の受入の順に決済される場合があります。 LIFO 日付を使用する場合、LIFO 日付ルールを使用する必要はありません。 代わりに、特定の品目の受入が特定の払出を対象に決済されるように、在庫トランザクションをマークすることもできます。 

LIFO 日付在庫モデルを使用する場合は、在庫原価計算を定期的に行うことをお勧めします。 

次の例では、3 つの異なる構成で LIFO 日付を使用した場合の影響について説明します。

-   **現物価格を含める**オプションを指定しない LIFO 日付
-   **現物価格を含める**オプションを指定した LIFO 日付
-   マーキングのある LIFO 日付

## <a name="lifo-date-without-the-include-physical-value-option"></a>[現物価格を含める] オプションを指定しない LIFO 日付
この例では、品目モデル グループが現物価格を含むようにマークされていません。 次の図は、これらのトランザクションについて説明しています。

-   1a。 原価がそれぞれ USD 10.00 の数量 1 に対する在庫現物入庫
-   1b. 原価がそれぞれ USD 10.00 の数量 1 に対する在庫財務入庫
-   2a. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫現物入庫
-   2b. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫財務入庫
-   3a. 原価がそれぞれ USD 25.00 の数量 1 に対する在庫現物入庫
-   4a。 原価価格がそれぞれ USD 15.00 の数量が 1 に対する在庫現物払出 (財務更新済トランザクションの移動平均)
-   4b。 原価価格がそれぞれ USD 15.00 の数量が 1 に対する在庫財務払出 (財務更新済トランザクションの移動平均)
-   5a。 原価がそれぞれ USD 30.00 の数量 1 に対する在庫現物入庫
-   5b。 原価がそれぞれ USD 30.00 の数量 1 に対する在庫財務入庫
-   6. 在庫決算が行われました。 LIFO 日付法に基づいて、最後の財務更新済払出が最後の財務更新済入庫に対して日付によって決済されます。 USD 5.00 の調整が払出トランザクションに対して実行されます。 これらのトランザクションは相互に決済されます。

新しい移動平均原価価格は、USD 15.00 での財務更新済トランザクションの平均を反映しています。 

次の図は、**現物価格を含める**オプションを使用しない場合の LIFO 日付在庫モデルの影響について説明しています。 ![[現物価格を含める] がオンの場合の LIFO 日付](./media/lifodatewithoutincludephysicalvalue.gif) 

**図の説明**

- 在庫トランザクションは、縦の矢印で表されています。
- 在庫への入庫は、タイムラインの上の縦の矢印で表されています。
- 在庫からの払出は、タイムラインの下の縦の矢印で表されています。
- 各縦矢印の上 (または下) には、在庫トランザクションの値が Quantity@Unitprice の形式で指定されています。
- かっこで囲まれた在庫トランザクションの値は、在庫トランザクションが在庫に現物転記されることを示します。
- かっこで囲まれていない在庫トランザクションの値は、在庫トランザクションが在庫に財務転記されることを示します。
- 個々の新しい入庫トランザクションまたは払出トランザクションは、新しいラベルで示されます。
- 各縦矢印には、*1a* のような連続した ID のラベルが付いています。 ID は、タイムラインでの在庫トランザクション転記の順序を示しています。
- 在庫原価計算は、赤い縦の点線と*在庫原価計算*のラベルで示されています。
- 在庫原価計算によって実行される決済は、入庫から払出へと斜めに向かう赤い点線矢印で表されます。

## <a name="lifo-date-with-the-include-physical-value-option"></a>[現物価格を含める] オプションを使用した LIFO 日付
**品目モデル グループ** ページで、品目の**現物価格を含める**チェック ボックスをオンにすることができます。 この場合、システムは現物入庫トランザクションと財務入庫トランザクションの両方を使用して移動平均原価価格を計算します。 該当する場合は、現物更新済払出トランザクションに対する調整も行われます。 **現物価格を含める**チェック ボックスがオフの場合、LIFO 日付在庫モデルを使用した在庫原価計算では、財務更新済のトランザクションに対してのみ決済が行われます。 

この例では、品目モデル グループが現物価格を含むようにマークされています。 

次の図は、これらのトランザクションについて説明しています。

-   1a。 原価がそれぞれ USD 10.00 の数量 1 に対する在庫現物入庫
-   1b. 原価がそれぞれ USD 10.00 の数量 1 に対する在庫財務入庫
-   2a. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫現物入庫
-   2b. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫財務入庫
-   3a. 原価がそれぞれ USD 25.00 の数量 1 に対する在庫現物入庫
-   4a。 原価価格がそれぞれ USD 18.33 の数量 1 に対する在庫現物払出 (財務更新済トランザクションの移動平均)
-   4b。 原価価格がそれぞれ USD 18.33 の数量 1 に対する在庫財務払出 (財務更新済トランザクションの移動平均)
-   5a。 原価がそれぞれ USD 30.00 の数量 1 に対する在庫現物入庫
-   5b。 原価がそれぞれ USD 30.00 の数量 1 に対する在庫財務入庫
-   6. 在庫決算が行われました。 LIFO 日付法に基づき、日付によって、最後の更新済払出が最後の更新済入庫に対して調整または決済されます。 財務入庫トランザクションが現物更新済トランザクションに対して調整されるので、これらのトランザクションは相互には決済されません。 代わりに、USD 6.67 の調整だけが払出トランザクションに対して行われます。

新しい移動平均原価価格は、USD 20.00 での財務更新済トランザクションの平均を反映しています。 

次の図は、**現物価格を含める**オプションを使用した LIFO 在庫モデルの影響について説明しています。 ![[現物価格を含める] がオンの場合の LIFO 日付](./media/lifodatewithincludephysicalvalue.gif) 

**図の説明**

- 在庫トランザクションは、縦の矢印で表されています。
- 在庫への入庫は、タイムラインの上の縦の矢印で表されています。
- 在庫からの払出は、タイムラインの下の縦の矢印で表されています。
- 各縦矢印の上 (または下) には、在庫トランザクションの値が Quantity@Unitprice の形式で指定されています。
- かっこで囲まれた在庫トランザクションの値は、在庫トランザクションが在庫に現物転記されることを示します。
- かっこで囲まれていない在庫トランザクションの値は、在庫トランザクションが在庫に財務転記されることを示します。
- 個々の新しい入庫トランザクションまたは払出トランザクションは、新しいラベルで示されます。
- 各縦矢印には、*1a* のような連続した ID のラベルが付いています。 ID は、タイムラインでの在庫トランザクション転記の順序を示しています。
- 在庫原価計算は、赤い縦の点線と*在庫原価計算*のラベルで示されています。
- 在庫原価計算によって実行される決済は、入庫から払出へと斜めに向かう赤い点線矢印で表されます。

## <a name="lifo-date-with-marking"></a>マーキングを使用した LIFO 日付
マーキングの処理を使用することで、払出トランザクションを入庫トランザクションにリンクまたはマークできます。 マーキングは、トランザクションが転記される前でも後でも可能です。 トランザクションを転記するとき、または在庫原価計算を実行するときに、在庫の原価を正確にする必要がある場合は、マーキングを使用できます。 

たとえば、顧客サービス部門が重要な顧客から急ぎの注文を受けたとします。 急ぎの注文なので、顧客の要求に対応するには、その品目に対する支払を高くする必要があります。 この販売注文請求書の利ざや、つまり、売却済商品の原価 (COGS) に在庫品目の原価が確実に反映されるようにする必要があります。 

発注書を転記するとき、在庫は USD 120.00 の原価で入庫されます。 梱包明細または請求書を転記する前に販売注文文書を発注書に対してマークすると、COGS は、品目の現在の移動平均原価ではなく USD 120.00 になります。 マーキングが発生する前に販売注文梱包明細または請求書が転記されると、COGS は移動平均原価価格で転記されます。 

在庫原価計算を実行する前でも、これら 2 つのトランザクションは相互にマークできます。 

たとえば、受入トランザクションは払出トランザクションにマークされています。 その場合、品目の品目モデル グループに対して定義されている評価方法は無視され、システムがこれらのトランザクションを相互に決済します。 

トランザクションが転記される前に払出トランザクションを入庫にマークするには、以下を実行します。 **販売注文の詳細**ページの販売注文明細行から、これを行うことができます。 **マーキング** ページで未処理入庫トランザクションを表示できます。 

トランザクションが転記された後に払出トランザクションを入庫にマークすることもできます。 転記済在庫調整仕訳帳からの在庫品目の未処理入庫トランザクションについて、払出トランザクションに一致またはマークできます。 

次の図は、これらのトランザクションについて説明しています。

-   1a。 原価がそれぞれ USD 10.00 の数量 1 に対する在庫現物入庫
-   1b. 原価がそれぞれ USD 10.00 の数量 1 に対する在庫財務入庫
-   2a. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫現物入庫
-   2b. 原価がそれぞれ USD 20.00 の数量 1 に対する在庫財務入庫
-   3a. 原価がそれぞれ USD 25.00 の数量 1 に対する在庫現物入庫
-   4a. 原価がそれぞれ USD 30.00 の数量 1 に対する在庫現物入庫
-   4b. 原価がそれぞれ USD 30.00 の数量 1 に対する在庫財務入庫
-   5a。 原価価格がそれぞれ USD 21.25 の数量が 1 に対する在庫現物払出 (財務および現物更新済トランザクションの移動平均)
-   5b。 トランザクションが転記される前に、数量 1 に対する在庫財務払出を、在庫入庫 2b にマークします。 このトランザクションは、原価価格がそれぞれ USD 20.00 で転記されます。
-   6a。 原価価格がそれぞれ USD 21.25 の数量 1 に対する在庫現物払出
-   7. 在庫決算が行われました。 財務更新済の 先入れ先出し (FIFO) トランザクションが既存の入庫にマークされているため、これらのトランザクションは相互に決済され、調整は行われません。

新しい移動平均原価価格は、USD 27.50 での財務および現物更新済トランザクションの平均を反映しています。 

次の図は、払出と入庫の間でマーキングを使用するときの LIFO 在庫モデルの影響を示しています。 ![[マーキング] が有効な場合の LIFO 日付](./media/lifodatewithmarking.gif) 

**図の説明**

- 在庫トランザクションは、縦の矢印で表されています。
- 在庫への入庫は、タイムラインの上の縦の矢印で表されています。
- 在庫からの払出は、タイムラインの下の縦の矢印で表されています。
- 各縦矢印の上 (または下) には、在庫トランザクションの値が Quantity@Unitprice の形式で指定されています。
- かっこで囲まれた在庫トランザクションの値は、在庫トランザクションが在庫に現物転記されることを示します。
- かっこで囲まれていない在庫トランザクションの値は、在庫トランザクションが在庫に財務転記されることを示します。
- 個々の新しい入庫トランザクションまたは払出トランザクションは、新しいラベルで示されます。
- 各縦矢印には、*1a* のような連続した ID のラベルが付いています。 ID は、タイムラインでの在庫トランザクション転記の順序を示しています。
- 在庫原価計算は、赤い縦の点線と*在庫原価計算*のラベルで示されています。
- 在庫原価計算によって実行される決済は、入庫から払出へと斜めに向かう赤い点線矢印で表されます。





