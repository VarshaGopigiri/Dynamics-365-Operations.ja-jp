--- 
title: "貸与品目の作成"
description: "貸与品目は、会社が作業者に貸与する電話やコンピューターを含む現物品目を追跡するのに役立つレコードです。"
author: kherr75
manager: AnnBe
ms.date: 11/01/2017
ms.topic: business-process
ms.prod: 
ms.service: dynamics-365-talent
ms.technology: 
audience: Application User
ms.reviewer: rschloma
ms.search.scope: Operations, Talent
ms.search.region: Global
ms.author: kherr
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: a8b5a5af5108744406a3d2fb84d7151baea2481b
ms.openlocfilehash: 429b33366ab9ab705a0f31cb9659f58b41689152
ms.contentlocale: ja-jp
ms.lasthandoff: 04/13/2018

---
# <a name="create-loan-items"></a>貸与品目の作成

[!include [task guide banner](../../includes/task-guide-banner.md)]

貸与品目は、会社が作業者に貸与する電話やコンピューターを含む現物品目を追跡するのに役立つレコードです。 個々の現物品目は、対応する貸与品目が必要です。 各貸与品目のレコードに、貸与中の品目、貸与の責任者、および貸与可能な日数を記述する必要があります。 キー、アクセス カード、制服などの複数の貸与品目を同時に作成できます。 この手順の作成に使用するデモ データの会社は USMF です。


## <a name="create-loan-types"></a>貸与タイプの作成
1. [人事管理] > [作業者] > [貸与品目] > [貸与タイプ] の順に移動します。
2. [新規] をクリックします。
3. [貸与タイプ] フィールドに値を入力します。
4. [説明] フィールドに値を入力します。
5. この貸与タイプに割り当てられた品目を延滞できる日数を入力します。 
6. [保存] をクリックします。
7. ページを閉じます。
8. ページを更新します。

## <a name="create-loan-items"></a>貸与品目の作成
1. [人事管理] > [作業者] > [貸与品目] > [貸与品目] の順に移動します。
2. [貸与品目の作成] をクリックします。
3. [数量] フィールドで、数値を入力します。
4. [説明] フィールドに値を入力します。
5. [貸与タイプ] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
6. 一覧で、目的のレコードを見つけ、選択します。
7. 一覧で、選択された行のリンクをクリックします。
8. 品目を貸与できる日数を入力します。
    * [貸与設備] ページの [返却予定] フィールドの既定値は、現在の日付にこの数を加算して計算されます。  
9. [担当者] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
10. [選択] をクリックします。
11. [開始値] フィールドに数値を入力します。
12. [間隔] フィールドに数値を入力します。
13. [形式] フィールドに値を入力します。
    * たとえば、貸与品目の開始番号が 10 の場合、[形式] フィールドには 2 つの数値記号を入力します。  
14. [OK] をクリックします。
15. ページを更新します。


