--- 
title: "発注書の作成時に購買リリース注文を作成"
description: "この手順では、発注書を作成するときに購買契約書を使用する方法を示します。"
author: mkirknel
manager: AnnBe
ms.date: 11/14/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: bis
ms.search.scope: Operations
ms.search.region: Global
ms.author: mkirknel
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: f01d88149074b37517d00f03d8f55e1199a5198f
ms.openlocfilehash: 9f7407ca1d42eb24b5a6df90f659bc850ced414b
ms.contentlocale: ja-jp
ms.lasthandoff: 07/27/2017

---
# <a name="create-a-purchase-release-order-when-creating-the-purchase-order"></a>発注書の作成時に購買リリース注文を作成

[!include[task guide banner](../../includes/task-guide-banner.md)]

この手順では、発注書を作成するときに購買契約書を使用する方法を示します。 発注書ヘッダーには一般的な条件をコピーする必要があるので、発注書を作成するときに購買契約書を適用する必要があります。 通常、これらのタスクを実施するのは、購買担当者です。 このガイドの前提条件として、仕入先および品目の製品数量が確約された有効購買契約書が必要です。 同じ手順は、他のタイプの確約のある購買契約書が存在する場合に使用できます。 デモ データの会社 USMF でこのガイドを実行できます。 USMF を使用する場合、最初に「購買契約の作成」ガイドを実行して、このガイドに必要な前提条件を設定することができます。


## <a name="create-a-purchase-order"></a>発注書の作成
1. 発注書準備ワークスペースを開きます。
2. [新しい発注書] をクリックします。
3. [仕入先] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
4. 一覧で、目的のレコードを見つけ、選択します。
5. 一覧で、選択された行のリンクをクリックします。
6. [一般] セクションの展開を切り替えます。
7. [購買契約] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
    * 利用可能な仕入先とのすべての契約がここに表示されます。 使用する有効な契約を検索します。  
8. 一覧で、選択された行のリンクをクリックします。
9. [はい] をクリックします。
10. [OK] をクリックします。

## <a name="add-a-line"></a>明細行の追加
1. [品目番号] フィールドに値を入力します。
    * 確約に特定の在庫または場所分析コードがある場合、契約を使用する購買注文明細行に同じ値を入力する必要があります。  
2. [サイト] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
    * サイトは、注文または仕入先の既定値から、既に設定されいる場合があります。 その場合、この手順を省略します。  
3. 一覧で、目的のレコードを見つけ、選択します。
4. 一覧で、選択された行のリンクをクリックします。
5. [数量] フィールドに数値を入力します。
    * 価格が確約からコピーされたことを確認します。  

## <a name="look-up-the-commitment"></a>確約の検索
1. [明細行の更新] をクリックします。
2. [添付済] をクリックします。
    * ここで購買契約書の詳細を取得できます。 たとえば、価格の確認や、価格や割引が変更されたものであるかの確認ができます。これはつまり、発注書の価格や割引を確約と異なる値に変更した場合に、システムはリンクを削除して購買注文明細行が確約を満たさないものとします。 また、[最大値の適用] オプションが選択されていることを確認できます。これは、確約の数量が、確約を履行するすべての購買の合計を超えることができないことを意味します。  
3. ページを閉じます。

## <a name="look-up-the-purchase-agreement"></a>購買契約書の検索
1. アクション ウィンドウで、[一般] をクリックします。
2. [購買契約書] をクリックします。
3. ページを閉じます。
4. ページを閉じます。

