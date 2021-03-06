--- 
title: "コール センター注文の作成"
description: "この手順では、顧客の検索、新しい注文の作成、製品の検索、および顧客から支払を回収する方法について説明します。"
author: josaw1
manager: AnnBe
ms.date: 11/14/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
audience: Application User
ms.reviewer: josaw
ms.search.scope: Operations, Retail
ms.search.region: Global
ms.search.industry: Retail
ms.author: josaw
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: ea07d8e91c94d9fdad4c2d05533981e254420188
ms.openlocfilehash: b2e986df1e089ef2a394d0e9d9236d39f2726c77
ms.contentlocale: ja-jp
ms.lasthandoff: 02/07/2018

---
# <a name="create-call-center-orders"></a>コール センター注文の作成

[!include [task guide banner](../includes/task-guide-banner.md)]

この手順では、顧客の検索、新しい注文の作成、製品の検索、および顧客から支払を回収する方法について説明します。 この手順では、デモ データの会社 USRT を使用して、販売注文の担当者を対象としています。 前提条件: 手順を完了するユーザーが、コール センター ユーザーとして設定され、Fabrikam Semi-Annual Catalog が少なくとも 1 つのソースコードと共に公開されています。

1. [小売りとコマース] > [顧客] > [顧客サービス] に移動します。
2. [検索文字列] フィールドで、顧客を検索するための検索条件を入力します。
    * この手順の例では、「開発者」を入力し、タブをクリックします。  
3. [検索] をクリックします。
    * デモ データに開発者という名前の顧客が一人だけあるため、それが自動的に選択されます。  
4. [新しい販売注文] をクリックします。
5. [販売注文ヘッダー] セクションを展開または折りたたみます。
6. カタログのソース コードを選択します。
    * 有効なソース・コードがない場合、ソース フィールドを閉じ、この手順を省略できます。  
7. [明細行の追加] をクリックします。
8. [品目番号] フィールドで、品目の検索用語を入力します。
    * このサンプルの手順については、品目番号の一部の「8111」を入力し、タブをクリックします。品目の検索ウィンドウがポップアップ表示されます。  
9. 販売注文に追加する製品を選択します。
10. 販売数量を入力します。
11. [作成] をクリックします。
12. 顧客支払を取得するために、[完了] をクリックします。
13. [追加] をクリックします。
    * [追加] リンクは、[支払] タブにあります。[支払] タブが折りたたまれている場合、展開します。  
14. 支払方法を選択します。
    * この手順では、支払方法は現金を選択します。  
15. ページを閉じます。
16. 金額を入力します。
    * この手順では、販売注文の概要ページに表示される注文の残高と同じ金額を、金額フィールドの左側に入力します。 全額支払われるように注文を行うことができます。  
17. [OK] をクリックします。
18. [送信] をクリックします。


