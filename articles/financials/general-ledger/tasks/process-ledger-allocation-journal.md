--- 
title: "元帳配賦仕訳帳の処理"
description: "[配賦要求の処理] ページを使用して、[総勘定元帳] に転記する前に確認および承認したり、[総勘定元帳] に直接転記することが可能な配賦仕訳帳を作成します。"
author: aprilolson
manager: AnnBe
ms.date: 11/10/2016
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
ms.openlocfilehash: 7d299657758b1e1322aef07bfe8c71f7bf00b0ca
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="process-ledger-allocation-journal"></a>元帳配賦仕訳帳の処理

[!include [task guide banner](../../includes/task-guide-banner.md)]

[配賦要求の処理] ページを使用して、[総勘定元帳] に転記する前に確認および承認したり、[総勘定元帳] に直接転記することが可能な配賦仕訳帳を作成します。 配賦仕訳帳を作成するためには、少なくとも 1 つの有効な [元帳配賦ルール] が必要です。 このタスクでは、USMF というデモ会社を使用します。

1. [総勘定元帳] > [配賦] > [配賦要求の処理] の順に移動します。
2. [ルール] フィールドで、ドロップダウン ボタンをクリックしてルックアップを開きます。
3. 一覧で、目的のレコードを見つけ、選択します。
4. 一覧で、選択された行のリンクをクリックします。
5. [現在の日付] フィールドに日付を入力します。
    * [元帳] がルールの [データ ソース] である場合、[現在の日付] はとても重要です。 この日付けによって、どの元帳残高を配賦に含めるかを制御します。     [ゼロ ソース] フィールドで [停止] を選択します。 この操作により配賦プロセスを停止し、配賦元の金額ゼロが選択されたことを示すメッセージを表示します。  
6. [提案オプション] フィールドで、「提案のみ」を選択します。
    * [提案のみ] を選択し、[総勘定元帳] に配賦を転記する前に、[配賦仕訳帳] の結果を確認し、また必要に応じて承認します。  
7. [GL 転記日付] フィールドに日付を入力します。
8. [OK] をクリックします。
9. [総勘定元帳] > [配賦] > [配賦仕訳帳] の順に移動します。
10. [行] をクリックします。
11. [転記] をクリックします。
12. [転記] をクリックします。


