---
title: "ローカル エージェントの更新"
description: "このトピックでは、ローカル エージェントを更新する方法について説明します。"
author: sarvanisathish
manager: AnnBe
ms.date: 03/05/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Operations
ms.custom: 60373
ms.assetid: 
ms.search.region: Global
ms.author: sarvanis
ms.search.validFrom: 2017-12-05
ms.dyn365.ops.version: 7.3
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: de4e152e0f29d03f21fe02c4bdf23963fda012a3
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---
# <a name="update-the-local-agent"></a>ローカル エージェントの更新

[!include [banner](../includes/banner.md)]

このトピックでは、ローカル エージェントを更新する方法について説明します。 ローカル エージェントの最新バージョンはバージョン 2.0.0で、2018 年 3 月にリリースされました。

| ローカル エージェントのバージョン | 能力 | 
|---------------------|------------|
| Null                | この初期バージョンでは、Platform update 8 が導入されています。 |
| 1.0.0               | このバージョンでは、展開が失敗した場合のために[再構成機能](../../dev-itpro/lifecycle-services/reconfigure-environment.md)が有効になります。 |
| 1.1.0               | このバージョンでは、正常に展開するために[再構成機能](../../dev-itpro/lifecycle-services/reconfigure-environment.md)が有効になり、複数モデルのパッケージ展開が可能になり、プラットフォーム更新プログラム 8 および 11 が展開されます。 | 
| 200               | このバージョンでは、サービス フローが可能になり、プラットフォーム更新プログラム 12 が展開されます。 |

## <a name="whats-new-in-local-agent-200"></a>Local agent 2.0.0 の新機能
- ローカル エージェント 2.0.0 はプラットフォーム更新プログラム 12 を展開できます。
- プラットフォーム更新 12 の配置の初回成功まで、[再構成機能](../../dev-itpro/lifecycle-services/reconfigure-environment.md)は有効になります。
- プラットフォーム更新 12 の配置の初回成功時は、[再構成機能](../../dev-itpro/lifecycle-services/reconfigure-environment.md)は無効になります。 配置が成功した後、定期的な更新エクスペリエンスを使用して環境を更新することができます。

> [!NOTE]
> ローカル エージェント 2.0.0 は、プラットフォーム更新プログラム 8 およびプラットフォーム更新プログラム 11 を展開**できません**。 プラットフォーム更新プログラムを展開するには、バージョン 1.1.0 が必要です。

## <a name="download-the-latest-local-agent-and-configuration-from-lcs"></a>LCS から最新のローカル エージェントおよびコンフィギュレーションをダウンロード

> [!NOTE]
> 現在の配置では、ローカル エージェントの以前のバージョンを要求する場合は、Microsoft Dynamics Lifecycle Services (LCS) の資産ライブラリからそれをダウンロードします。 ローカルエージェント v1.1.0 をダウンロードするには、**共用資産ライブラリ - >モデル** に移動し、[Dynamics 365 for Finance and Operations オンプレミス - ローカルエージェント v1.1.0] をクリックします。

> [!IMPORTANT]
> プラットフォーム更新プログラム 12 の展開および更新プログラム フローの完成には、バージョン 2.0.0 かそれ以降のバージョンが必要です。

1. LCS で、**プロジェクト設定** &gt; **オンプレミス コネクタ**を選択します。
2. 環境へのコネクタを選択し、**編集** を選択します。
3. ページの左側にあるメニューの、**ホスト インフラストラクチャ設定**を選択し、**エージェント インストーラーのダウンロード**を選択します。

    この時点で、ダウンロードする ZIP ファイルがブロックされていないことを確認する必要があります。

4. zip ファイルに移動し、右クリックして**プロパティ**を選択します。
5. **プロパティ** ダイアログ ボックスで、**ブロック解除**を選択してから**適用**を選択します。
6. **エージェントのコンフィギュレーション**タブで、**コンフィギュレーションのダウンロード**を選択し、localagent-config.json コンフィギュレーション ファイルをダウンロードします。

## <a name="update-the-local-agent"></a>ローカル エージェントの更新

1. ZIP ファイルと localagent-config.json ファイルを、**Orch1** 仮想マシン (VM) の **c:\\DynamicsAgent** などの、**Orchestrator** ノードの 1 つにコピーします。
2. エージェント インストーラを C:\\DynamicsAgent\\LocalAgent に解凍します。
3. localagent-config.json ファイルを \\DynamicsAgent\\LocalAgent にコピーします。
4. **コマンド プロンプト** ウィンドウで、C:\\DynamicsAgent\\LocalAgent に移動して、次のコマンドを実行します。

    ```
    LocalAgentCLI.exe Cleanup <path of localagent-config.json>
    ```

    > [!NOTE]
    > エージェントをクリーンアップするには、現在のエージェントのバイナリ ファイルを使用する必要があります。 現在のエージェントのバイナリ ファイルがない場合は、Service Fabric Explorer からローカル エージェント アプリケーションを削除できます。

5. クリーンアップ操作を終了するには、任意のキーを押します。
6. Service Fabric Explorer を調べ、**Orchestrator** ノードの **展開済みアプリケーション** セクションにアプリケーションがないことを確めて、ローカル エージェントが正常にクリーンアップされことを確認します。
7. ローカル エージェントが正常にクリーンアップされた後は、次のコマンドを実行します。

    ```
    LocalAgentCLI.exe Install <path of localagent-config.json>
    ```

8. ローカル エージェントが正常にインストールされると、LCS のオンプレミス コネクタに戻るようにします。
9. **設定の検証**タブで、**メッセージ エージェント**を選択して、新しいローカル エージェントへの LCS 接続をテストします。

