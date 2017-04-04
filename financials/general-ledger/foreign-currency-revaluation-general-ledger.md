---
title: "総勘定元帳の外貨再評価"
description: "このトピックでは、総勘定元帳の外貨の再評価プロセスに次の概要を提供します]設定した場合、プロセスは、プロセスの計算、再評価のトランザクションを取り消す方法を必要に応じて実行します。"
author: twheeloc
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
ms.search.form: CurrencyLedgerGainLossAccount
audience: Application User
ms.search.scope: AX 7.0.0, Operations, Core
ms.custom: 62153
ms.assetid: 842e8561-560f-4cc6-8668-70cca60b1ba3
ms.search.region: Global
ms.author: kweekley
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: 9ef99caf4570969d2b920cec8b53669ce2094965
ms.openlocfilehash: 5d6d13fe44eef7766b4dcaf274c3522bce3da816
ms.lasthandoff: 03/31/2017


---

# <a name="foreign-currency-revaluation-for-general-ledger"></a>総勘定元帳の外貨再評価

このトピックでは、総勘定元帳の外貨の再評価プロセスに次の概要を提供します]設定した場合、プロセスは、プロセスの計算、再評価のトランザクションを取り消す方法を必要に応じて実行します。 

最終期間の一部として、会計公準に外貨の総勘定元帳勘定の残高が異なる為替レート タイプ (現在、履歴、平均など) を使用して再評価する必要があります。 たとえば、1 つの会計公準では、現在の為替レート、過去の為替レートの固定資産、および月次平均の損益勘定で再評価される必要があります。 総勘定元帳の外貨再評価を、貸借対照表および損益勘定の再評価として使用できます。 

> [!NOTE]
> 外貨の再評価、売掛金勘定(AR)と買掛金(AP)にも使用できます。 これらのモジュールを使用して、未処理トランザクションは、これらのモジュールの外貨の再評価を使用して再評価されます。 AR および AP の外貨再評価に未実現利益または損失を反映するように総勘定元帳に会計入力を subledgers と総勘定元帳調整を行うことができるようになります。作成します。 AR および AP の外貨再評価によって総勘定元帳の勘定項目が作成されるため、売掛金勘定および買掛金勘定の主勘定は、総勘定元帳の外貨再評価から除外されます。 

再評価プロセスを実行すると、外貨で転記された各主勘定の残高が再評価されます。 再評価プロセス中に作成されるトランザクションは、システムによって生成されます。 二つのトランザクションは、関連する、会計通貨の一つとレポート通貨の単位で作成されたかもしがあります。 再評価された各帳簿入力は損失および主要な勘定の未実現に転記されます。

## <a name="prepare-to-run-foreign-currency-revaluation"></a>外貨再評価の実行の準備
再評価プロセスを実行する前に、次の設定が必要です。

-   [**主勘定**] ページ:
-   総勘定元帳で主勘定を再評価する必要がある場合は、[**外貨再評価**] を選択します。 主勘定 (補助元帳で再評価された場合は、AR や AP など) を再評価するべきでない場合は、このオプションをオフにします。
-   主勘定に再評価が設定されている場合は、[**為替レート タイプ**] と入力します。 この為替レート タイプは、主勘定の再評価に使用されます。 別のフィールド、[**財務報告為替レート タイプ**] は、財務報告に使用できます。 2 つのフィールドは同期していないため、異なる為替レートタイプを再評価および財務報告に使用することができます。

-   [**元帳**] ページ:
-   [**為替レート タイプ**] を指定します。 為替レート タイプが主勘定で定義されていない場合、この為替レート タイプが外貨再評価で使用されます。
-   通貨再評価の実現利益、実現損失、未実現利益および未実現損失の勘定を指定します。 実現利益と実現損失の勘定は、AR および AP トランザクションに使用され、未実現利益と未実現損失の勘定が、未処理トランザクションの再評価および一般会計の主勘定に使用されます。

-   [**通貨の再評価勘定**] ページ:
-   各通貨および会社ごとに異なる通貨再評価勘定を選択します。 勘定が定義されていない場合は、**元帳**ページの勘定が使用されます。

## <a name="process-foreign-currency-revaluation"></a>外貨再評価の処理
設定が完了したら、[**外貨再評価**] ページを使用して、主勘定の残高を再評価します。 リアル タイムでプロセスを実行したり、バッチを使用して実行されるようにスケジュールしたりできます。 

[**外貨再評価**] ページでは、前の再評価がリバースされている場合、条件が定義されているリンクを再評価に対して作成された伝票に実行されたときに含める各再評価プロセスの履歴、およびレコードが表示されます。 再評価プロセスを実行するには、[**外貨再評価**] ボタンを選択します。 

[**開始日**] と [**終了日**] 値では、再評価された外貨残高勘定を計算する日付間隔を定義します。 損益勘定を再評価すると、日付範囲内に行われるすべてのトランザクションの合計が再評価されます。 貸借対照表勘定を再評価すると、開始日は無視されます。 代わりに、再評価される残高は、会計年度の初めから終了日までに決定されます。 

**レートの日付**為替レートを決定する日付を定義するのに使用できます。 たとえば、1年1月1日の日付範囲から1年1月31日間の残高を再計算できますが2.月1日に対して定義される為替レートを使用します。 

再評価する主勘定を選択します: すべて、貸借対照表、または損益。 再評価用にマークされた主要な勘定のみ (主要な勘定のページで再評価されます。 さらに主要な勘定範囲を制限する場合は、レコード**含める**主要な勘定範囲を定義するタブまたは個々の主要な勘定を使用します。 

再評価プロセスは、一つ以上の法人の実行できます。 参照は、にアクセスできる法人のみが表示されます。 [再評価プロセスを実行する法人を選択します。 

再評価は、1 つ以上の外貨に対して実行できます。 参照は、主要な勘定のタイプに関連した日付範囲内 (貸借対照表、損益または利益が転記された)、された再評価によって、法人を含むすべての通貨。 会計通貨が一覧に含まれますが、会計通貨を選択するかを再評価されません。 

**設定の転記前のプレビュー** **総勘定元帳の再評価の結果を確認することを望んだらに**はい。 総勘定元帳のプレビューARは、APの外貨のシミュレーションでは、再評価。 AR、APのシミュレーションはレポートですが、総勘定元帳に再評価プロセスを実行しないで転記できるプレビューがあります。 プレビューの結果は、金額の計算方法の履歴を保持するために Microsoft Excel にエクスポートできます。 再評価の結果をプレビューする場合は、バッチ処理は使用できません。 プレビューから、ユーザーが [**転記**] ボタンを使用してすべての法人の結果を転記するオプションがあります。 法人の結果に問題がある場合、ユーザーには [**転記する法人を選択**] ボタンを使用して法人のサブセットを転記するオプションもあります。 

外貨の再評価プロセスが完了したら実行したそれぞれの履歴を追跡するには、レコードが作成されます。  別のレコードは、法人および転記階層に対して作成されます。

## <a name="calculate-unrealized-gainloss"></a>未実現利益/損失の計算
未実現利益/損失トランザクションは、総勘定元帳再評価と AR および AP 再評価プロセス間で異なる方法で作成されます。 AR および AP では、以前の再評価は完全に取り消され (トランザクションがまだ決済されていないと仮定して)、新しい為替レートに基づく未実現損益の新しい再評価取引が作成されます。 これは、AR と AP で個々のトランザクションを再評価するためです。 総勘定元帳で、前の再評価が振りされません。 この場合、トランザクションは主要な勘定の残高との差分に対して作成されます以前の再評価が、レートの日付の為替レートに基づいて新しい値は、必要があります。 

**例**次の残高は、主要な勘定110110になります。

|            |                    |                        |                       |
|------------|--------------------|------------------------|-----------------------|
| **日付**   | **勘定科目** | **トランザクション金額** | **会計金額** |
| 1 月 20 日 | 110110 (現金)      | 500 EUR (借方)        | 1000 USD (借方)      |

重要な勘定は1年1月31日に再評価されます。  未実現利益/損失は次のように計算されます。

|                                             |                                            |                                  |                                    |                             |
|---------------------------------------------|--------------------------------------------|----------------------------------|------------------------------------|-----------------------------|
| **トランザクション通貨での期首残高** | **会計通貨での現在の残高** | **再評価の為替レート** | **新しい会計通貨の金額** | **未実現利益/損失**    |
| 500 EUR                                     | 1000 USD                                   | 166.6667                         | 833.33 EUR (500 x 1.666667)        | 166.67 損失 (833.33 – 1000) |

次の勘定項目が作成されます。

|            |                          |           |            |
|------------|--------------------------|-----------|------------|
| **日付**   | **勘定科目**       | **デビット** | **クレジット** |
| 1 月 31 日 | 110110 (現金)            |           | 166.67     |
| 1 月 31 日 | 801400 (未実現損失) | 166.67    |            |

新しいトランザクションが2年に対して転記されません。  重要な勘定は2年1月28日に再評価されます。

|                                             |                                            |                                  |                                    |                             |
|---------------------------------------------|--------------------------------------------|----------------------------------|------------------------------------|-----------------------------|
| **トランザクション通貨での期首残高** | **会計通貨での現在の残高** | **再評価の為替レート** | **新しい会計通貨の金額** | **未実現利益/損失**    |
| 500 EUR                                     | 833.33 USD (1000 - 166.67)                 | 250.0000                         | 1250 USD (500 x 2.5)               | 416.67 利益 (1250 – 833.33) |

次の勘定項目が作成されます。

|             |                          |           |            |
|-------------|--------------------------|-----------|------------|
| **日付**    | **勘定科目**       | **デビット** | **クレジット** |
| 2 月 28 日 | 110110 (現金)            | 416.67    |            |
| 2 月 28 日 | 801600 (未実現利益) |           | 416.67     |

## <a name="reverse-foreign-currency-revaluation"></a>外貨再評価の取り消し
再評価のトランザクションを取り消す必要がある場合は、[**外貨再評価**] ページで [**トランザクションの取消**] を選択します。 再評価が発生したか、または取り消されたかの履歴監査証跡を維持するために、新しい外貨再評価履歴レコードが作成されます。 

再評価の古いの注文の結果を取り消すか、再評価された主要な勘定の正しい残高を確認する現在の再評価を取り消す必要があります。 取消を制御する再評価時に主要な勘定を頻度再評価方法がないため、発生し、古い形式。 たとえば、現金主要な勘定を各季に再評価することもできます。他のメイン フォーカスはすべてに説明します。

