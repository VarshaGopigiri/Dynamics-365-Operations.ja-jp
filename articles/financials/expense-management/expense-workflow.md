---
title: "経費ワークフロー"
description: "このトピックでは、Microsoft Dynamics 365 for Finance and Operations でワークフロー システムを使用する方法を説明し、経費管理で経費精算書の確認プロセスを設定します。"
author: saraschi2
manager: AnnBe
ms.date: 09/13/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: WorkflowtableListPageRnr
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Core, Operations
ms.search.region: Global
ms.author: saraschi
ms.search.validFrom:
- month/year of release that feature was introduced in
- in format yyyy-mm-dd
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: a0739304723d19b910388893d08e8c36a1f49d13
ms.openlocfilehash: 6ee607f723659a5b6ecd655ba4fdfca35a4c582d
ms.contentlocale: ja-jp
ms.lasthandoff: 03/26/2018

---

# <a name="expense-workflow"></a>経費ワークフロー

[!include [banner](../includes/banner.md)]

Microsoft Dynamics 365 for Finance and Operations でワークフロー システムを使用でき、経費管理で経費精算書の確認プロセスを設定します。 以下の条件を使用するワークフローを設定して、経費精算書を誰が承認するかを決定できます。

- 従業員の報告階層と定義済みの承認制限
- 中間承認者および最終承認者をサポートする複数レベルの承認
- 財務分析コードとプロジェクトの責任
- 特定のユーザーまたはユーザー グループに割り当て

ワークフローの承認は、経費精算書、出張命令書、現金前貸し要求、付加価値税 (VAT) の払い戻しに作成できます。

**例**

経費精算書の経費管理ワークフローの例を次に示します。

1. 従業員が経費精算書を作成して、保存します。
2. 従業員は承認のために経費精算書を提出します。 承認者はワークフローの設定時に定義したルールに基づいて識別します。
3. 承認者が、承認を受ける準備ができた経費精算書の通知を受け取ります。 承認者は経費精算書をレビューし、次の条件が満たされていることを確認します:

    - 経費に経費ポリシーの違反がない。 経費がポリシーに違反した場合、承認者は有効な業務上の理由が経費精算書に記載されているか確認します。
    - 電子レシートが経費計算書に添付されている。

4. 承認者は経費精算書を承認します。
5. 経費精算書が、転記のために買掛金勘定コーディネーターに割り当てられます。
6. 次の手順のいずれかが行われるかは、自動転記がコンフィギュレーションされているかどうかによって異なります。

    - 自動転記を構成すると、経費報告書は支払処理され、経費精算書の状態が更新されます。
    - 自動転記が構成されていない場合、買掛金勘定コーディネーターがすべての元のレシートが提出済みで、レシートが経費精算書の経費に対応していることを確認します。 経費精算書に入力されたすべての税コードが正しいかどうかも確認する必要があります。

これらの条件を確認したら、経費報告書は転記されます。

経費精算書を転記すると、経費精算書の支払が承認され、従業員に払い戻しが行われます。

