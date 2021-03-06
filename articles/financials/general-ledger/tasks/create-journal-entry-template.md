--- 
title: "テンプレートを使用した仕訳入力の作成"
description: "転記済みの仕訳帳伝票は伝票テンプレートとして保存され、新しい仕訳伝票に適用できます。"
author: aprilolson
manager: AnnBe
ms.date: 02/17/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Operations
ms.search.region: Global
ms.author: aolson
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 055fe129b9fc9cf50e1d9e1a5b4cb77285f20c92
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="create-a-journal-entry-using-a-template"></a>テンプレートを使用した仕訳入力の作成

[!include [task guide banner](../../includes/task-guide-banner.md)]

転記済みの仕訳帳伝票は伝票テンプレートとして保存され、新しい仕訳伝票に適用できます。 この手順では、USMF というデモ会社を使用します。

1. [総勘定元帳] > [仕訳入力] > [一般仕訳帳] の順に移動します。 [新規] をクリックします。
    * この手順は、仕訳伝票の作成および転記によって開始されますが、以前に転記された仕訳伝票をテンプレートとして保存できます。  
2. [名前] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
3. 一覧で、目的のレコードを見つけ、選択します。
4. 一覧で、選択された行のリンクをクリックします。
5. [行] をクリックします。
6. 勘定タイプの勘定を入力します。
7. [説明] フィールドで値を入力します。
8. [借方] フィールドに、金額を入力します。
9. [新規] をクリックします。
10. 異なるタイプの勘定を入力します。
11. [説明] フィールドで値を入力します。
12. [借方] フィールドに、金額を入力します。
13. [新規] をクリックします。
14. [勘定] フィールドで、任意の値を指定します。
15. [説明] フィールドで値を入力します。
16. 伝票の収支を合わせるために [貸方] フィールドに金額を入力します。
17. [転記] をクリックします。
18. [機能] をクリックします。
19. [伝票テンプレートの保存] をクリックする
20. この手順は、パーセント テンプレート タイプとします。 [OK] をクリックします。
    * • 割合: 伝票の金額が比率係数に変換されるため、伝票テンプレートが選択されている場合に、全ての金額が適用可能となります。  • 金額: 実際の金額は保存され、適用されます。  
21. [一般仕訳帳] をクリックします。
22. [新規] をクリックします。
23. [名前] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
24. 一覧で、選択された行のリンクをクリックします。
25. [行] をクリックします。
26. [機能] をクリックします。
27. [伝票テンプレートの選択] をクリックします。
28. 先ほど作成したテンプレートを見つけます。 [OK] をクリックします。
    * [前のステップ] をクリックし、他のテンプレートが見つかる場合、適切なテンプレートを選択する必要があります。  
29. [金額] フィールドに、伝票に適用する金額を入力します。
    * 伝票テンプレートが [割合] タイプ場合にのみ、金額フィールドが表示されます。  
30. [OK] をクリックします。


