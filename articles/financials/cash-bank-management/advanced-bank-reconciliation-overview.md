---
title: "詳細な口座調整の概要"
description: "この記事は、高度な口座調整プロセスのフローについて説明します。 高度な口座調整機能では、銀行トランザクション内で自動的に調整できる口座取引明細書をインポートできます。"
author: twheeloc
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: BankReconciliationMatchRule
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Core, Operations
ms.custom: 22104
ms.assetid: b0705653-1fa6-4d94-9728-bcf9fb387ad1
ms.search.region: Global
ms.author: leguo
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: a0739304723d19b910388893d08e8c36a1f49d13
ms.openlocfilehash: ff59250b836a73986848109ce48f843fed1d71a9
ms.contentlocale: ja-jp
ms.lasthandoff: 03/26/2018

---

# <a name="advanced-bank-reconciliation-overview"></a>詳細な口座調整の概要

[!include [banner](../includes/banner.md)]

この記事は、高度な口座調整プロセスのフローについて説明します。 高度な口座調整機能では、銀行トランザクション内で自動的に調整できる口座取引明細書をインポートできます。

詳細な口座調整機能により、口座取引明細書のインポートをすることができます。 インポートした口座取引明細書は、次に自動的に銀行トランザクション内から調整されます。 詳細な口座調整のフローを次に示します。

1.  口座取引明細書のインポートを設定します。
    -   データ エンティティ フレームワークを使用して口座取引明細書をインポートします。
    -   ISO20022、BAI2、MT940、の 3 つの一般的な口座取引明細書の形式が組み込まれています。
    -   機能は、任意の形式に拡張できます。

2.  詳細な口座調整に使用する番号順序を設定して、口座調整の照合ルールを定義します。
    -   調整の照合ルールは、調整プロセス中に口座取引明細行および Microsoft Dynamics 365 for Finance and Operations 銀行トランザクション明細行をフィルター処理するために使用される一連の基準です。 業務内容によって、1 つ以上の照合ルールを設定して、調整プロセスを自動化また最適化できます。

3.  Finance and Operations の銀行トランザクションを使用して、口座取引明細書を調整します。
    -   口座調整仕訳の自動照合と作成を実行します。
    -   口座取引明細書と Finance and Operations の銀行トランザクションを並べて表示します。
    -   口座取引明細書には表示されるが Finance and Operations には表示されない場合、Finance and Operations に銀行のトランザクションを自動的に転記します。
    -   調整明細書を生成します。






