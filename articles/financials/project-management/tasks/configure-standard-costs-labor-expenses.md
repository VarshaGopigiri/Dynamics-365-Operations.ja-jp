--- 
title: "労務および経費の標準原価のコンフィギュレーション"
description: "この手順では、労働者の標準原価とプロジェクトの経費を設定する方法を示します。"
author: KimANelson
manager: AnnBe
ms.date: 02/13/2017
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Service industries
ms.author: knelson
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 432b5b195b29fb03786cb0560e277735b531b7d7
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="configure-standard-costs-for-labor-and-expenses"></a>労務および経費の標準原価のコンフィギュレーション

[!include [task guide banner](../../includes/task-guide-banner.md)]

この手順では、労働者の標準原価とプロジェクトの経費を設定する方法を示します。 このタスクでは、USSI データ セットを使用します。

1. [プロジェクト管理および会計] > [設定] > [価格] > [原価価格 (時間)] の順に移動します。
2. [新規] をクリックします。
3. [有効日] フィールドに日付を入力します。
4. [原価価格] フィールドに番号を入力します。
    * プロジェクト カテゴリの標準原価価格を設定したり、作業者番号、プロジェクト番号、カテゴリ、日付、またはそれらの組み合わせによって原価価格を設定したりすることができます。 適用される原価価格は、詳細度が最も高い原価価格です。  
5. [保存] をクリックします。
6. ページを閉じます。
7. [プロジェクト管理および会計] > [設定] > [価格] > [販売価格 (時間)] の順に移動します。
8. [新規] をクリックします。
9. [有効日] フィールドに日付を入力します。
10. [有効] フィールドで、オプションを選択します。
11. [価格決定] フィールドに、数を入力します。
    * 時間トランザクションまたはプロジェクト カテゴリに対して標準販売価格を設定できます。 また、作業者番号別、プロジェクト番号別、カテゴリ別、トランザクション日別、あるいはこれらを任意に組み合わせて販売価格を設定することができます。 作業者が時間仕訳帳にトランザクションを入力したときに適用される実際の販売価格が、最も詳細な販売価格です。 たとえば、一般的な販売価格と作業者固有の販売価格の両方が設定されている場合、作業者固有の販売価格が使用されます。  
12. [保存] をクリックします。
13. ページを閉じます。
14. [プロジェクト管理および会計] > [設定] > [価格] > [原価価格 (経費)] の順に移動します。
15. [新規] をクリックします。
16. [有効日] フィールドに日付を入力します。
17. [原価価格] フィールドに番号を入力します。
    * 複数のフィールドに入力することができますが、これがレコードを保存するために必要な最小値です。  
18. [保存] をクリックします。
19. ページを閉じます。
20. [プロジェクト管理および会計] > [設定] > [価格] > [販売価格 (経費)] の順に移動します。
21. [新規] をクリックします。
22. [有効日] フィールドに日付を入力します。
23. [有効] フィールドで、オプションを選択します。
24. [価格決定] フィールドに、数を入力します。
    * 作業者が経費仕訳帳にトランザクションを入力するときに適用される実際の販売価格は、最高レベルの詳細を持つ販売価格です。 たとえば、一般的および作業者固有の販売価格の両方が設定されている場合、作業者固有の販売価格が使用されます。  
25. [保存] をクリックします。


