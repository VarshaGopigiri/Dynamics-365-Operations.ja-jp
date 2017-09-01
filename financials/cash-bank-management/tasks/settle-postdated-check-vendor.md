--- 
title: "仕入先の先日付小切手の決済"
description: "銀行が期限切れの小切手をクリアして、その小切手トランザクションを精算してしまったときに、仕入先へ発行した先日付小切手を決済します。"
author: kweekley
manager: AnnBe
ms.date: 11/14/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Operations
ms.search.region: Global
ms.author: kweekley
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: f01d88149074b37517d00f03d8f55e1199a5198f
ms.openlocfilehash: 76c948ba99f9b4fa9200c2541c221c4ca86414e4
ms.contentlocale: ja-jp
ms.lasthandoff: 07/27/2017

---
# <a name="settle-a-postdated-check-for-a-vendor"></a>仕入先の先日付小切手の決済

[!include[task guide banner](../../includes/task-guide-banner.md)]

銀行が期限切れの小切手をクリアして、その小切手トランザクションを精算してしまったときに、仕入先へ発行した先日付小切手を決済します。 

これを始める前に、次の手順を完了します。

1) 先日付小切手の設定

2) 仕入先の先日付小切手の登録および転記



この手順のロールは会計登録者です。 この手順では、USMF というデモ会社を使用します。

1. [買掛金勘定] > [支払] > [仕入先の先日付小切手] へ移動します。
2. [決済] をクリックします。
3. [清算項目の決済] をクリックします。
    * 小切手トランザクションのための仕入先を決済します。  
4. ページを閉じます。
5. [総勘定元帳] > [総勘定元帳] > [仕訳入力] > [一般仕訳帳] の順に移動します。
6. [表示] フィールドで「すべて」を選択します。
7. [作成ユーザーのみ表示] チェック ボックスをオンまたはオフにします。
8. 一覧で、選択された行をマークします。
9. [行] をクリックします。
10. [伝票] をクリックします。
11. ページを閉じます。

