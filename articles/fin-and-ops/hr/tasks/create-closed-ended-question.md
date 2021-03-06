--- 
title: "選択式の質問の作成"
description: "選択式の質問には、回答者が選択できるためのオプションが用意されます。"
author: kherr75
manager: AnnBe
ms.date: 06/10/2016
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
ms.openlocfilehash: fdfac92b80774adb8376d5c2e945d063173188c8
ms.contentlocale: ja-jp
ms.lasthandoff: 04/13/2018

---
# <a name="create-a-closed-ended-question"></a>選択式の質問の作成

[!include [task guide banner](../../includes/task-guide-banner.md)]

選択式の質問には、回答者が選択できるためのオプションが用意されます。 最初に、回答と回答グループを作成する必要があり、その後回答グループを使用する質問を作成します。 この手順の作成に使用するデモ データの会社は USMF です。


## <a name="create-an-answer-group"></a>回答グループの作成
1. [アンケート] > [設計] > [回答グループ] の順に移動します。
2. [新規] をクリックします。
3. [回答グループ] フィールドに値を入力します。
4. [説明] フィールドに値を入力します。
    * 回答グループが質問に使用されるたびに、必要に応じて別の順序で回答をランダムに設定するランダム化機能を使用します。  
5. [回答] をクリックします。
6. [新規] をクリックします。
    * ランダム化機能が回答グループに対して選択されている場合を除いて、番号順序は回答が表示される順序を制御します。  
    * アンケートの採点に対して回答するために、ポイントは支給できます。  
7. [点数] フィールドに数値を入力します。
    * 正解な回答をマークし、選択した回答が正しいものであることを表示できます。 これは、アンケートの採点に使用できます。  
8. [回答] フィールドに値を入力します。
    * 回答グループに対して選択できる回答オプションを作成し続けます。  
9. [新規] をクリックします。
10. [点数] フィールドに数値を入力します。
11. [回答] フィールドに値を入力します。
12. [新規] をクリックします。
13. [点数] フィールドに数値を入力します。
14. [回答] フィールドに値を入力します。
15. [新規] をクリックします。
16. [点数] フィールドに数値を入力します。
17. [回答] フィールドに値を入力します。
18. [新規] をクリックします。
19. [点数] フィールドに数値を入力します。
20. [回答] フィールドに値を入力します。
21. ページを閉じます。
22. ページを閉じます。

## <a name="create-the-question"></a>質問の作成
1. [アンケート] > [設計] > [質問] の順に移動します。
2. [新規] をクリックします。
3. [タイプ] フィールドを使用して、関連の質問をグループ化します。
    * 選択式の質問の場合は、チェック ボックス、代替ボタン、またはコンボ ボックスの入力タイプを使用できます。  
4. [入力タイプ] フィールドで、オプションを選択します。
5. [回答グループ] フィールドで、値を入力または選択します。
6. [テキスト] フィールドに値を入力します。


