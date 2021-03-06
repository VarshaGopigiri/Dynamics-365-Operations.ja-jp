---
title: "生産出荷場所"
description: "このトピックでは、生産出荷場所を識別するために使用される階層について説明します。"
author: johanhoffmann
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: bis
ms.search.scope: Core, Operations
ms.custom: 221264
ms.assetid: dde49743-1541-4353-a030-63ca3069cd7d
ms.search.region: Global
ms.author: johanho
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Version 1611
ms.translationtype: HT
ms.sourcegitcommit: 2771a31b5a4d418a27de0ebe1945d1fed2d8d6d6
ms.openlocfilehash: b1d6d1270dcbdf3baff63b2ccf300d6195329b41
ms.contentlocale: ja-jp
ms.lasthandoff: 11/03/2017

---

# <a name="production-output-location"></a>生産出荷場所

[!include [banner](../includes/banner.md)]

このトピックでは、生産出荷場所を識別するために使用される階層について説明します。

生産出荷場所は、完成品が生産された後に最初に保管される場所です。 通常、この場所は完成品を生産する生産工程の近くにあります。 生産出荷場所は、出荷エリア、保管場所、下流生産プロセスの生産入庫場所などに移動する前に、品目の中間保管として使用されます。 

既定の生産出荷場所は、完成品が製造オーダーまたはバッチ オーダーで報告されたときに設定されます。 次の階層を使用して、この出荷場所を識別します。

1. 製造オーダーまたはバッチの注文ヘッダーで定義されている出荷場所を使用します。
2. そこに場所が見つからない場合は、本番ルートで定義されている最後の操作により使用されているリソースで定義されている出荷場所を使用します。
3. そこに場所が見つからない場合は、本番ルートで定義されている最後の操作のリソースにより使用されているリソース グループで定義されている出荷場所を使用します。
4. そこに場所が見つからない場合は、製造オーダーに定義されている倉庫で定義されている出荷場所を使用します。

既定の生産出荷場所は、高度な倉庫プロセスを使用して設定されている製品にのみ設定されます。 このタイプの品目が完了報告されると、[**商品の保存を完了**] または [**連産品および副産物の保存**] タイプの倉庫作業が作成されます。 このタイプの作業は、ピッキング場所として生産出荷場所を使用します。 プット アウェイの場所は、場所ディレクティブによって決定されます。

