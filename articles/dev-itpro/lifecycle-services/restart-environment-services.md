---
title: "環境サービスの再開"
description: "このトピックでは、Microsoft Dynamics Lifecycle Services (LCS) を通じて展開される環境で個々のサービスを再起動する方法について説明します。こ"
author: kfend
manager: AnnBe
ms.date: 03/01/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Operations
ms.search.region: Global
ms.author: manado
ms.search.validFrom: 2018-03-05
ms.dyn365.ops.version: 7.3
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 080dc1dc52a7ad7f368c9075eb02e08c164b7ff7
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="restart-environment-services"></a>環境サービスの再開

[!include [banner](../includes/banner.md)]

Microsoft Dynamics Lifecycle Services (LCS) のサービスの再開機能を使用すると、Microsoft サブスクリプションで展開された階層 2、階層 3、階層 4、または階層 5 の標準承認テスト (サンドボックス) 環境に関連付けられた個々のサービスを再開することができます。 この機能を使用すると、次のサービスを再起動することができます。

- IIS
- DIXF
- LCS 診断
- バッチ
- レポート サーバー

プロジェクト所有者、組織管理者、または環境マネージャーとして LCS プロジェクトに追加されたすべてのユーザーは、この機能を使用するアクセス許可を持っています。

## <a name="restart-a-service"></a>サービスを再起動します

展開された環境で特定のサービスを再起動するには、次の手順を実行します。

1. LCS で、適切なプロジェクトを開き、サービスを再起動する環境を選択します。
2. **環境の詳細**ページで、**メンテナンス** &gt; **サービスのリセット**を選択します。
3. **サービスを再起動します**ダイアログ ボックスで、再起動するサービスを選択してから **OK** を選択します。

    **環境状態** 値は、サービスが再起動されると更新されます。

4. 更新された状態を表示するには、ページを更新します。

    > [!NOTE]
    > サービスの再起動には数秒しかかからないため、**環境の状態**の値はすでに**配置済み**にリセットされている可能性があります。 再起動が完了すると、エントリが **履歴** ページに追加されます。

