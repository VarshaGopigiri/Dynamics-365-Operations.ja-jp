---
title: "倉庫内の現物在庫の移動"
description: "この手順では、倉庫内の場所間で行われる品目の移動を登録する在庫振替仕訳帳を作成して転記するプロセスを説明します。"
author: MarkusFogelberg
manager: AnnBe
ms.date: 03/02/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Distribution
ms.author: mafoge
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: bfba69731a4897906d08ff9fb9ce69e79121efeb
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="transfer-physical-inventory-within-the-warehouse"></a>倉庫内の現物在庫の移動

[!include [task guide banner](../../includes/task-guide-banner.md)]

この手順では、倉庫内の場所間で行われる品目の移動を登録する在庫振替仕訳帳を作成して転記するプロセスを説明します。 これを開始する前に、在庫振替用の在庫仕訳帳名を設定してある必要があります。 この手順を確認するには、示されているサンプル値を使用してデモ データの会社 USMF を使用するか、製品と場所を設定済みの場合に独自のデータを使用することができます。 通常、これらのタスクを実施するのは、倉庫の従業員です。


## <a name="create-an-inventory-transfer-journal"></a>在庫振替仕訳帳の作成
1. [移動] に移動します。
2. [新規] をクリックします。
3. [名前] フィールドで値を入力または選択します。
4. [OK] をクリックします。
    * 仕訳帳明細行ごとに、分析コードの [開始] および [終了] を指定するオプションがあります。 これらは、この仕訳帳タイプでは必須です。 各種ルールを使用して複数の場所に品目を移動できます。 この例では、同じ倉庫内のライセンス プレートにより制御される場所からライセンス プレートにより制御されない場所に品目を移動します。   

## <a name="create-journal-lines"></a>仕訳帳明細行の作成
1. [新規] をクリックします。
2. [品目番号] フィールドで、値を入力または選択します。
    * USMF を使用すると、'A0001' を選択できます。  
3. [移動元サイト] フィールドで値を入力または選択します。
    * USMF を使用すると、'2' を選択できます。  
4. [移動先サイト] フィールドで値を入力または選択します。
    * USMF を使用すると、'2' を選択できます。  
5. [移動元倉庫] フィールドで値を入力または選択します。
    * USMF を使用すると、'24' を選択できます。  
6. [移動先倉庫] フィールドで値を入力または選択します。
    * USMF を使用すると、'24' を選択できます。  
7. [移動元場所] フィールドで値を入力または選択します。
    * USMF を使用すると、'FL-001' を選択できます。  
8. [移動先場所] フィールドで値を入力または選択します。
    * USMF を使用すると、'BULK-001' を選択できます。  
9. [数量] フィールドに数値を入力します。
10. [在庫分析コード] タブをクリックします。
11. [ライセンス プレート] フィールドで値を入力または選択します。
    * USMF を使用すると、'24' を選択できます。  
12. [保存] をクリックします。

## <a name="post-the-inventory-transfer-journal"></a>在庫振替仕訳帳の転記
1. [転記] をクリックします。
2. [OK] をクリックします。

## <a name="view-inventory-transactions"></a>在庫トランザクションの表示
1. [在庫] をクリックします。
2. [トランザクション] をクリックします。
    * ここで、仕訳帳の転記時に作成されたトランザクションを確認できます。  

