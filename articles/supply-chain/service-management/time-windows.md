---
title: "時間枠"
description: "サービス注文明細行のスケジューリングを最適化するために時間枠を使用できます。"
author: YuyuScheller
manager: AnnBe
ms.date: 02/20/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: SMATimeAgreement
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Core, Operations
ms.custom: 
ms.assetid: 
ms.search.region: Global
ms.author: YuyuScheller
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 4ea10e4c0fbfd21538bba16d2b01deb3e4b3a10d
ms.openlocfilehash: b7268870aa9065e4e52d936e819107094bad3663
ms.contentlocale: ja-jp
ms.lasthandoff: 02/20/2018

---

# <a name="time-windows"></a>時間枠  

[!include [banner](../includes/banner.md)]

サービス注文明細行のスケジューリングを最適化するために時間枠を使用できます。 サービス注文を自動的に作成するようにシステムを設定できます。 時間枠で指定された条件に基づき、できる限り少ないのサービス注文として、できるだけ多くのサービス注文明細行を接続できます。

時間枠では、計算日からサービス注文明細行が移動できる範囲を指定します。 計算日は、サービス注文明細行が実施される予定の日付です。 **サービス注文の作成** ページで定義したサービス期間と間隔の設定に基づいています。 時間枠を定義するには、次の表の値を使用します。

| 方法 | 説明                                                                                                                                                                                                                                                                                           |
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 週   | サービス注文明細行が初期計算日と同じ週の任意のオープン日に移動できる日付。                                                                                                                                                                                    |
| 月  | サービス注文明細行を初期計算日と同じ月の任意のオープン日に移動できる日付。 たとえば、サービス注文明細行の計算日は、2017 年 2 月 15 日です。 サービス注文明細行は、2017 年 2 月 1 日から 2 月 28 日の間で任意の平日をスケジューリングできます。 |
| マニュアル | 初期計算日の前後にサービス注文明細行を移動できる最大日数を定義します。                                                                                                                                                                           |

サービス契約項目の時間枠を指定しない場合、そのサービス契約から派生したサービス注文明細行は、元々スケジュール設定された日付に実行する必要があります。

## <a name="related-topics"></a>関連トピック

[時間枠の作成](create-time-windows.md)


