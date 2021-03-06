--- 
title: "ISO20022 口座振替コンフィギュレーションのインポート"
description: "この手順では、仕入先支払の電子レポートのコンフィギュレーションをインポートする方法を示します。"
author: mrolecki
manager: AnnBe
ms.date: 10/24/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: shylaw
ms.search.scope: Operations
ms.search.region: Global
ms.author: mrolecki
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 71c0175178203006e297466c4a37cd3e6319b6ea
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="import-iso20022-credit-transfer-configuration"></a>ISO20022 口座振替コンフィギュレーションのインポート

[!include [task guide banner](../../includes/task-guide-banner.md)]

この手順では、仕入先支払の電子レポートのコンフィギュレーションをインポートする方法を示します。 ドイツの ISO 20022 口座振替形式が例として使用されます。 この手順は、使用可能なその他の電子申告フォーマットに使用できます。 

このタスクはデモ データの会社 DEMF を使用して作成されましたが、どのデモ データの会社を使用してもこのタスクを完了できます。

これは、5 つのうち 1 つ目のタスクで、電子レポートのコンフィギュレーションを使用する仕入先支払処理を一緒に説明しています。 この手順は、Dynamics 365 for Operations、バージョン 1611 に追加された機能です。

1. [組織管理] > [ワークスペース] > [電子申告] の順に移動します。
2. 使用できるコンフィギュレーション プロバイダーの一覧で、[Microsoft] を選択します。
3. [有効に設定] をクリックします。
4. [リポジトリ] をクリックします。
5. [開く] をクリックします。
6. [フィルターの表示] をクリックします。
7. [コンフィギュレーション名] フィールドで "次の値で始まる" フィルター演算子を使用して、値 "ISO20022 口座振替 (DE)" でフィルターを適用します。
    * または、一覧からコンフィギュレーションを見つけ、選択し、インポート タスクに移動することもできます。  
8. [インポート] をクリックします。
    * インポートのボタンを使用できない場合は、そのコンフィギュレーションは既にインポートされています。  
9. [はい] をクリックします。


