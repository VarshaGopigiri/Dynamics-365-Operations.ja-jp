---
title: "Finance and Operations でのワークフロー サブシステムの更新"
description: "この記事では、Microsoft Dynamics 365 for Finance and Operations のワークフロー システムについて説明します。 Microsoft Dynamics AX 2012 以降に実装された変更について説明し、ワークフロー システムに関する詳細へのリンクも示します。"
author: sericks007
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 13511
ms.assetid: 0e3aa2cd-2327-45ba-bf38-0ef543fa8f67
ms.search.region: Global
ms.author: tjvass
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: ee633df3582f2466318eeee8f742f09f79fc921b
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="workflow-subsystem-updates-in-finance-and-operations"></a>Finance and Operations でのワークフロー サブシステムの更新

[!include [banner](../includes/banner.md)]

この記事では、Microsoft Dynamics 365 for Finance and Operations のワークフロー システムについて説明します。 Microsoft Dynamics AX 2012 以降に実装された変更について説明し、ワークフロー システムに関する詳細へのリンクも示します。 

Microsoft Dynamics AX 2012 を使用していれば、Finance and Operations のワークフロー システムは既におなじみのものです。 Microsoft Dynamics AX 2012 のワークフロー サブシステムの詳細については、次のトピックを参照してください。

| このテーマについて学ぶには | このトピックを参照                                             |
|-----------------------------|------------------------------------------------------------|
| ワークフロー システム         | <http://technet.microsoft.com/en-us/library/dd309672.aspx> |
| モジュールごとのワークフロー タイプ    | <http://technet.microsoft.com/EN-US/library/dd362043.aspx> |
| ワークフロー要素           | <http://technet.microsoft.com/en-us/library/dd309626.aspx> |
| ワークフロー アクション            | <http://technet.microsoft.com/EN-US/library/dd362144.aspx> |
| ワークフローの参加者       | <http://technet.microsoft.com/EN-US/library/dd309598.aspx> |
| ワークフローの例           | <http://technet.microsoft.com/en-us/library/dd309636.aspx> |
| ワークフローの開発       | <http://msdn.microsoft.com/EN-US/library/cc967389.aspx>    |
| ワークフローの実装     | <http://msdn.microsoft.com/en-us/library/cc585061.aspx>    |

## <a name="primary-changes-to-the-workflow-system"></a>ワークフロー システムの主な変更
Finance and Operations で実装された基本変更を次に示します。

-   新しいアプリケーション状態機械機能との統合により、ワークフロー イベントを基になるエンティティの状態機械での状態遷移に関連付けできます。 このバインディングにより、ビジネス ロジックをステート マシン内で集中化することが可能になり、また、ワークフロー システムをそのステート マシンの宣言コンシューマーにすることが可能になります。 ワークフロー メタデータは、特定のワークフロー イベントが発生したときに実行される状態遷移を参照できます。 したがって、追加のコードを記述することなく、ワークフロー内で状態遷移を行うことができます。
-   ワークフロー エディターは、1 回クリックしてダウンロードするプログラムになりました。 エディターは、サービスを使用して、Finance and Operations と通信します。 したがって、Finance and Operations は、Dynamics AX 2012 の豊富なグラフィカルなワークフロー設計操作を引き継ぐことができます。
-   ワークフロー開発ウィザードは Microsoft Visual Studio にポート済みです。


<a name="additional-resources"></a>その他のリソース
--------

[開発者向け技術概念ガイド](../dev-tools/developer-home-page.md)




