---
title: "連結と削除の概要"
description: "この記事は、連結および消去プロセスに関する一般情報を提供します。 これには、よく寄せられる質問への回答が含まれます。"
author: aprilolson
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: LedgerConsolidate
audience: Application User
ms.reviewer: robinr
ms.search.scope: Core, AX 7.0.0, Operations, UnifiedOperations
ms.custom: 13151
ms.assetid: 9d8f55cb-b2cf-4e01-89cf-0e21f5c8ae1f
ms.search.region: Global
ms.author: aolson
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: Human Translation
ms.sourcegitcommit: d421b161216d700f7819f1da8c0ca8ad089b5670
ms.openlocfilehash: c9568d1cac05db83d00108e8b16c03aa4c807cac
ms.contentlocale: ja-jp
ms.lasthandoff: 05/25/2017

---

# <a name="consolidation-and-elimination-overview"></a>連結と削除の概要

[!include[banner](../includes/banner.md)]


この記事は、連結および消去プロセスに関する一般情報を提供します。 これには、よく寄せられる質問への回答が含まれます。

データを連結する場合、複数の関連会社の財務結果は 1 つの連結した会社の結果にまとめられます。 関連会社は、さまざまなバージョンまたはシステムを使用している場合があり、完全に所有されていない場合や、さまざまな通貨を使用している場合があります。 データを連結するための複数のオプションがあります。

-   **オンラインで連結** – このオプションは、選択された勘定および分析コードで、毎日の残高を連結し、連結会社に保存します。
-   **財務報告** – このオプションは、トランザクションおよび残高の連結を有効にして、いつでも生成します。 階層が複数のレベルを作成し、複数のレポート通貨を表示します。
-   **インポートして連結** – このオプションは、連結会社に残高をインポートします。
-   **会社の残高のエクスポート** – このオプションは、会社の残高のエクスポート ファイルを提供します。 ファイルは、他のインスタンスまたはシステムにインポートできます。 財務報告は Microsoft Excel ファイルに残高をエクスポートするためにも使用できます。

削除はさまざまな方法で報告できます。

-   削除ルールがシステムで設定され、連結プロセス中または削除提案を通して処理されます。 このルールは、法人の設定で [**財務消去プロセスで使用**] が選択された会社すべてに転記できます。
-   手動で削除トランザクションを特定および転記するために、個別の会社が作成また使用されます。 この会社は、連結プロセスまたは財務報告に使用できます。
-   会社間活動を特定するために使用される勘定と財務分析コードは、財務報告の行定義と列定義でフィルター処理することができ、完全なドリルダウン機能が使用できます。 次に計算された列または行は、連結合計から勘定と財務分析コードを削除するために使用されます。

多くの連結のシナリオがあり、それぞれの方法は、さまざまな方法でシナリオを処理できます。

## <a name="frequently-asked-questions"></a>よく寄せられる質問
1.  データベースでの消去の転記を希望します。 どのようなオプションがありますか?

複数のオプションがあります。 [**オンラインで連結**] オプションを使用して、プロセス中または提案としての消去を含むことができます。 トランザクションが連結会社に転記されます。 消去を含む手動で作成した個別の会社を作成し、財務報告または連結プロセスでその会社を使用することもできます。

2.  複数のレポート通貨で、連結の結果が必要です。

[**財務報告**] オプションには、無制限のレポート通貨があります。 主勘定に設定された為替レート タイプおよび為替換算方法に基づいて、データはレポート生成時に換算されます。 ただし、レポート通貨に [**オンラインで連結**] オプションが 1 つしかないため、このオプションを使用する場合、レポート通貨それぞれに 1 つの連結会社が必要です。 [**財務報告**] オプションがお勧めの方法です。

3.  各会社のトランザクション レベルの詳細の表示を希望します。

[**財務報告**] オプションがソリューションです。できるだけ多くの会社で、レポート ツリー定義に含まれるトランザクション レベルの詳細が表示できるためです。

4.  予算計画または予算管理を使用していて、それを連結する必要があります。
[**財務報告**] オプションは、すべての予算計画または予算管理のデータを連結するソリューションです。

5.  弊社の関連会社は、世界中に拡大し、複数の勘定科目表があります。 弊社のデータを連結するのに最適な方法は何ですか?

複数の勘定科目表を処理する必要がある場合、複数のオプションがあります。 [**オンラインで連結**] オプションを使用 し、主勘定または連結勘定グループで定義された連結勘定のどちらを使用するかを次に選択します。 [**財務報告**] オプションを使用 し、行定義の財務分析コードに複数のリンクを追加し、勘定をマップすることができます。

6.  複数レベルの連結が必要です。 言い換えると、最初に英国ポンド (GBP) にすべての欧州関連会社を連結します。 次に、そのデータを取得して、連結された金額を米ドルに換算します。 どのようにしますか?

複数のレベルの連結が必要となり、さまざまな通貨が各レベルで使用されている場合は、[**オンラインで連結**] オプションを使用する必要があります。 会計通貨とレポート通貨が異なる複数の連結会社を作成する必要があります。 次に連結を複数回実行する必要があります。 [**財務報告**] オプションは、元の会社の各会計通貨から選択した通貨に常に換算します。

7.  別のシステムを使用する関連会社があります。 どのように連結すればいいでしょうか?

[**インポートして連結**] オプションを使用して、連結会社に残高を結び付けます。

8.  関連会社の一部は完全に所有されていません。 それらを連結するのに最適な方法は何ですか?

一部を所有している関連会社のために複数のオプションがあります。 [**財務報告**] オプションを使用して、レポート ツリー定義と所有権を定義できます。 計算された行または列を使用して、部分的に所有された金額を表すこともできます。 レポートの独自の行として少数株主持分を表示することもできます。 [**オンラインで連結**] オプションを使用することもできます。 [**法人**] タブには、[**所有権**] の列があり、親会社が所有する割合を定義することができます。

9.  当組織では事業単位で連結を表示する必要があります。または組織階層を使用することを希望します。

[**財務報告**] オプションがソリューションです。 法人がある組織階層、またはそれらの中にある財務分析コードは "財務報告" で報告できます。 法人および分析コード値の組み合わせによるレポート ツリー定義を使用して、独自の複数レベルの階層を作成することもできます。

10. システムには複数のインスタンスがあります。

[**会社の残高のエクスポート**] オプションを使用して、1 つのインスタンスからエクスポートし、次に他のインスタンスで [**インポートして連結**] オプションを使用してデータを連結できます。


詳細については、「[連結会社の通貨再評価](..\general-ledger\currency-revaluation-consolidation-company.md)」を参照してください。


