---
title: "テーブルへのリレーションの追加"
description: "このトピックでは、テーブルにリレーションを追加する方法について説明します。"
author: ivanv-microsoft
manager: AnnBe
ms.date: 07/10/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 268724
ms.assetid: 
ms.search.region: Global
ms.author: ivanv
ms.search.validFrom: 2017-07-01
ms.dyn365.ops.version: Platform update 4
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 2a97a1d85f99306b0ef35333e0cb4674d60ee4cc
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="add-a-relation-to-a-table"></a>テーブルへのリレーションの追加

[!include [banner](../includes/banner.md)]

複数のテーブルにあるデータとの高機能かつ安全な相互作用を可能にするには、2 つのテーブル間のリンクを記述するリレーションを定義して参照整合性を保証する必要があります。 関係を定義することにより、入力されたデータの検証および関連情報のルックアップ機能を有効にできます。 

テーブルを拡張することにより新しいリレーションを追加することができます。

次の例では、新しいフィールド **MyInventLocationId** が InventTable テーブルに追加されます。 このフィールドは、倉庫が含まれる InventLocation テーブルへの参照です。

1. 新しい拡張モデルで、InventTable テーブルの拡張機能を作成します。
1. 通常のテーブルにリレーションを作成するのと同じように、新しいリレーションを作成します。
1. **関連テーブル**、**関係タイプ**、**カーディナリティ** プロパティと、関係に適用される他のプロパティを指定します。
1. 同じ値を持つ InventTable テーブルと InventLocation テーブルからフィールドを指定してリンクを追加します。 この場合、フィールドは InventTable テーブルでは **MyInventLocationId** であり、InventLocation テーブルでは **InventLocationId** となります。

次の図は、新しいリレーションを示しています。

![新しい関係](media/AddRelationToExistingTable.jpg)

