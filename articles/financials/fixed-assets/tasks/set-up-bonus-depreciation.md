--- 
title: "特別償却の設定"
description: "この手順では、特別減価償却費を作成する方法およびそれを固定資産帳簿に関連付ける方法を説明します。"
author: saraschi2
manager: AnnBe
ms.date: 10/11/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Operations
ms.search.region: Global
ms.author: saraschi
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 7e6ebb13084626b477b6e0b24acdc09e2c0d3d6d
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="set-up-bonus-depreciation"></a>特別償却の設定

[!include [task guide banner](../../includes/task-guide-banner.md)]

この手順では、特別減価償却費を作成する方法およびそれを固定資産帳簿に関連付ける方法を説明します。 これは USMF の法人に対して経理担当ロールとデモ データを使用します。


## <a name="create-a-special-depreciation-allowance"></a>特別減価償却費の作成
1. [固定資産] > [設定] > [特別減価償却費] の順に移動します。
2. [新規] をクリックします。
3. [特別減価償却費] フィールドに値を入力します。
4. [説明] フィールドに値を入力します。
5. [割合] フィールドに数値を入力します。
    * 割合が表示されなかった場合は金額を設定します。  

## <a name="associate-a-special-depreciation-allowance-with-a-fixed-asset-group-book"></a>特別減価償却費を固定資産グループ帳簿と関連付ける
1. [固定資産] > [設定] > [固定資産グループ] の順に移動します。
2. 一覧で、特別減価償却費に関連する固定資産グループを選択します。
3. [帳簿] をクリックします。
4. 一覧で、特別減価償却費に関連する帳簿を選択します。
5. [特別減価償却費] をクリックします。
6. [新規] をクリックします。
7. [特別減価償却費] フィールドで、値を入力または選択します。
    * 割合または金額の既定値は特別減価償却費の設定によって決まります。  
8. [優先順位] フィールドに数値を入力します。


