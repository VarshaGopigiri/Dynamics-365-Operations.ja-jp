---
title: "要素の利用状況"
description: "この記事では、アプリケーションでの要素の使用方法を決定するために、Microsoft Visual studio ツールに追加されたコマンドについて説明します。"
author: RobinARH
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 4984
ms.assetid: e9590e78-6aae-4c3a-b50b-786351cfc0ff
ms.search.region: Global
ms.author: robadawy
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 94c169529cedc5bb1e3d4bc186eea5942cec6f1f
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="element-usage"></a>要素の利用状況

[!include [banner](../includes/banner.md)]

この記事では、アプリケーションでの要素の使用方法を決定するために、Microsoft Visual studio ツールに追加されたコマンドについて説明します。 

一般的なアプリケーション内の要素数が多いため、Microsoft Visual Studio Tools にコマンドは追加され要素の使用方法を簡単に判断できます。

## <a name="finding-where-elements-are-used"></a>要素が使用されている場所を検索

ビルド操作中に、要素の使用方法を示すために使用できる相互参照情報が生成されます。 要素を右クリックしてから **参照の検索** をクリックし、要素が使用される場所の一覧を表示することができます。 リスト内の品目のいずれかをクリックすると、要素のデザイナーが開きます。 [![23\_DevoToolsConcept](./media/23_devotoolsconcept.png)](./media/23_devotoolsconcept.png)

## <a name="viewing-a-reference-diagram"></a>参照ダイアグラムの表示

テーブルなどの上位レベルの要素を右クリックすると、**参照の表示**コマンドを使用できます。 このコマンドは、現在の要素に関連する要素を示すグラフィックを作成します。 グラフィック内の項目を右クリックしてから **定義に移動** をクリックし、これらの要素に移動することができます。 [![24\_DevoToolsConcept](./media/24_devotoolsconcept.png)](./media/24_devotoolsconcept.png)

## <a name="additional-resources"></a>その他のリソース

[開発ツールの概要](development-tools-overview.md)

[要素デザイナー](element-designers.md)




