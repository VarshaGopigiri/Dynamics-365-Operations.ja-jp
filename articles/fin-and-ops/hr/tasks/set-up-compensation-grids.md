--- 
title: "報酬グリッドの設定"
description: "[報酬] グリッドは、固定報酬プランの支払構造を定義または維持するために使用します。"
author: kherr75
manager: AnnBe
ms.date: 03/02/2016
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
ms.openlocfilehash: d507224004bdf319f9bf13ba07ed07ef29cc85dc
ms.contentlocale: ja-jp
ms.lasthandoff: 04/13/2018

---
# <a name="set-up-compensation-grids"></a>報酬グリッドの設定

[!include [task guide banner](../../includes/task-guide-banner.md)]

[報酬] グリッドは、固定報酬プランの支払構造を定義または維持するために使用します。 [報酬] グリッドは、複数のプラン間で共有または新しい報酬プランの作成時にコピーすることができます。  報酬グリッドを作成する前に、[レベル] と [基準] ポイントを設定する必要があります。 この例では、[レベル] と [基準] ポイントのデモ データを使用して、報酬グリッドの新しい [等級] タイプを作成します。 この手順の作成に使用するデモ データの会社は USMF です。


## <a name="set-up-information-about-the-compensation-grid"></a>報酬グリッドに関する情報の設定
1. [人事管理] > [報酬] > [固定報酬] > [報酬グリッド] の順に移動します。
2. [新規] をクリックします。
3. [グリッド] フィールドに値を入力します。
4. [説明] フィールドに値を入力します。
5. [タイプ] フィールドで、オプションを選択します。
6. [参照設定] フィールドで、値を入力または選択します。
7. [通貨] フィールドで値を入力または選択します。
8. [通貨] フィールドに値を入力します。
9. [有効日] フィールドに日付を入力します。

## <a name="add-levels-to-the-compensation-structure"></a>報酬構造にレベルを追加
1. [報酬構造] をクリックします。
2. 一覧で、選択された行をマークします。
3. [レベル] フィールドで、値を入力または選択します。
4. [新規] をクリックします。
5. 一覧で、選択された行をマークします。
6. [レベル] フィールドで、値を入力または選択します。
7. [新規] をクリックします。
8. 一覧で、選択された行をマークします。
9. [レベル] フィールドで、値を入力または選択します。
10. [新規] をクリックします。
11. 一覧で、選択された行をマークします。
12. [レベル] フィールドで、値を入力または選択します。
13. [新規] をクリックします。
14. 一覧で、選択された行をマークします。
15. [レベル] フィールドで、値を入力または選択します。

## <a name="fill-in-the-compensation-structure-with-values"></a>値を含む報酬構造の入力
1. 一覧で、選択された行をマークします。
    * この時点で、報酬の値は、テーブルの各フィールドに手動で入力できます。または、複数のフィールドに簡単に入力して、基本的な計算を実行するのに、[一括変更] 機能を使用できます。  
2. [一括変更] をクリックします。
    * このグリッドでは、まず最初のレベルの平均支給額をテーブルのすべてのフィールドに適用します。 これは、報酬マトリックスの基準になります。  
3. [調整のタイプ] フィールドでオプションを選択します。
4. [調整金額] フィールドで、数値を入力します。
5. 一覧で、すべての行のマークを設定または解除します。
6. [グリッドに適用] をクリックします。
    * ここで、一定の割合または金額で、後続の各レベルの金額を増加させるために一括変更機能を使用します。 この例では、各段階の平均間で 12.5% の分散があります。  
7. [調整のタイプ] フィールドでオプションを選択します。
8. [調整金額] フィールドで、数値を入力します。
9. 一覧で、目的のレコードを見つけ、選択します。
10. 一覧で、目的のレコードを見つけ、選択します。
11. 一覧で、目的のレコードを見つけ、選択します。
12. 一覧で、目的のレコードを見つけ、選択します。
13. [グリッドに適用] をクリックします。
14. 一覧で、目的のレコードを見つけ、選択します。
15. 一覧で、目的のレコードを見つけ、選択します。
16. 一覧で、目的のレコードを見つけ、選択します。
17. [グリッドに適用] をクリックします。
18. 一覧で、目的のレコードを見つけ、選択します。
19. 一覧で、目的のレコードを見つけ、選択します。
20. [グリッドに適用] をクリックします。
21. 一覧で、目的のレコードを見つけ、選択します。
22. [グリッドに適用] をクリックします。
    * ここで、各レベルの最小基準点と最大基準点を調整するために、一括変更機能を使用します。 この例では、50% 分散を使用し、最小基準点は -20%、 最大基準点は +20% 調整されます。  
23. [調整金額] フィールドで、数値を入力します。
24. [基準点] フィールドで、値を入力または選択します。
25. 一覧で、すべての行のマークを設定または解除します。
26. [グリッドに適用] をクリックします。
27. [調整金額] フィールドで、数値を入力します。
28. [基準点] フィールドで、値を入力または選択します。
29. 一覧で、すべての行のマークを設定または解除します。
30. [グリッドに適用] をクリックします。


