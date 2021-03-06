---
title: "継続的ビルドとテストの自動化を使用した配置"
description: "このトピックでは、継続的なビルドとテストの自動化をサポートする開発者トポロジを配置する方法について説明します。"
author: RobinARH
manager: AnnBe
ms.date: 02/22/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 13171
ms.assetid: 
ms.search.region: Global
ms.author: shailesn
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 6bcb77cd142f2d251902744f0e80f32c74947b5f
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="deployment-with-continuous-build-and-test-automation"></a>継続的ビルドとテストの自動化を使用した配置

[!include [banner](../includes/banner.md)]

このトピックでは、継続的なビルドとテストの自動化をサポートする開発者トポロジを配置する方法について説明します。

前提条件: クラウド VM 展開には Visual Studio Team Services (VSTS) アカウントが必要です。

## <a name="workflow"></a>ワークフロー
Lifecycle Services (LCS) で VSTS サブスクリプションを設定した後、開発者トポロジの配置をトリガーして開発者およびビルド VM の設定をすることができます。 この配置では、開発者用 VM は VSTS プロジェクトに対して開発するためにワークスペース マッピングで構成されます。 ビルド VM は、モジュール VSTS プロジェクトを構築し、検証用の外部エンドポイントを使用して自動テストを実行するために、ビルド エージェント/コントローラーを使用して自動構成されます。 カスタム テスト コードの記述またはビルド インフラストラクチャと統合する自動テスト コードを生成する方法については、[テストと検証](testing-validation.md) を参照してください。 一般的なワークフローまたは使用シナリオを次に示します。 

[![build12](./media/build12-1024x693.jpg)](./media/build12.jpg)

## <a name="set-up-visual-studio-team-services-vsts"></a>Visual Studio Team Services (VSTS) の設定
組織の必要な VSTS 機能を比較します。<https://www.visualstudio.com/products/visual-studio-team-services-feature-matrix-vs>

-   **TFVC 対 GIT**: RTW では、LCS に接続された VSTS プロジェクトで構成できるソース コントロール リポジトリとして TFVC のみをサポートしています。 Git はサポートされていません。
-   **現在のビルドの中断:** 既にビルド定義が作成されている既存の VSTS プロジェクトにビルド エージェントを展開している場合、ビルドをキューに入れるための有効なトリガーがないことを確認してください。 また、ビルド プールに対して、スケジュールされた/キューに格納されたビルドがないことを確認してください。 

    [![BuildTriggers](./media/buildtriggers.jpg)](./media/buildtriggers.jpg)

-   **無料の VSTS アカウントには、ビルド エージェントが 1 つだけ用意されています**。 アカウントは複数のビルド エージェントに対してプロビジョニングされていないので、フリーの VSTS アカウントを使用して、別のビルド エージェントで新しいビルド VM を配置することは失敗します。


複数のビルド エージェントを使用するには、Azure 請求 [[アカウントの請求を設定する](/vsts/billing/set-up-billing-for-your-account-vs)] で VSTS アカウントを設定します。 

[![VSTS1](./media/vsts1-300x155.jpg)](./media/vsts1.jpg)

-   アカウントが Azure サブスクリプションとリンクされた後。 さらにビルド エージェントを繰り入れるため、Azure 管理ポータルで指示に従います - [ロード テストの購入](/vsts/billing/buy-load-testing-vs)


[![VSTS2](./media/vsts2-300x151.jpg)](./media/vsts2.jpg) 

> [!NOTE]
> 支払済オプションで、「プライベート エージェント」を増やしてください。 

[![VSTS3](./media/vsts3-300x191.jpg)](./media/vsts3.jpg)

-   **ビルド エージェント プールのロールとアクセス許可:**<https://msdn.microsoft.com/library/vs/alm/build/agents/admin#agent-pools>

ビルド エージェントが追加されたら、ユーザー (LCS から VM を配置構築) を「エージェント プール管理者」ロールにします。 

[![VSTS4](./media/vsts4.jpg)](./media/vsts4.jpg)

-   **管理エージェント:** 複数のエージェントがコンフィギュレーションされていて、1 つを削除する場合は、エージェントを選択し、ステータス列の右側にある削除ボタンを使用します。

    [![build14](./media/build14.jpg)](./media/build14.jpg)

-   **既定のプールの削除:** 何らかの理由でデフォルト プールを削除した場合は、「既定」という名前の新しいプールを作成しないでください。 代わりに、別の名前で新しい管理グループを作成し、配置の際に LCS の「詳細設定」のカスタマイズから管理グループ名を渡します。
-   **個人用アクセス トークン:** このトークンは、アップグレードおよび配置を含む Lifecycle Services (LCS) のバックグラウンド アクションで使用されます。 ユーザーが LCS からアクションを起動すると、LCS はユーザーが VSTS に追加されることを期待しています。 ユーザーは、ユーザーの代わりに VSTS への LCS アクセスを認可する必要があります。 プロジェクトのユーザーが VSTS で承認されるまで、アクション センターに以下のメッセージが表示されます。 

[![LCS の VSTS 設定\_5 月 27 日](./media/vsts-setup-in-lcs_may27-300x216.jpg)](./media/vsts-setup-in-lcs_may27.jpg)

## <a name="deploy-developer-topology-from-lcs"></a>LCS から開発者トポロジを配置する
LCS では、開発トポロジ環境を配置するオプションが提供されます。 このオプションでは、Visual Studio Team System (VSTS) プロジェクトに接続されたクラウド内に、開発者を配置して VM をビルドすることができます。

### <a name="vsts-credential-setup-and-linking-to-lcs-project"></a>VSTS 資格情報の設定と LCS プロジェクトへのリンク

1. [https://lcs.dynamics.com/](https://lcs.dynamics.com/)で LCS ポータルにログインして、VSTS および LCS プロジェクトに接続します。
2. 作業しているプロジェクトを選択します。
3. **プロジェクト設定**タイルをクリックします。
4. **Visual Studio Team Services** を選択し、モジュール プロジェクトのソース コードが保管されている VSTS URL を入力します。
5. VSTS リンクを指定して、承認し、**既定のプロジェクトを選択** をクリックします。
   > [!NOTE]
   > 現在のところ、VSTF をソース コントロールとしてサポートしていますが、Git をサポートしていません。 

[![VSTS](./media/vsts-1024x792.jpg)](./media/vsts.jpg)

### <a name="check-in-migrated-or-new-module-code-into-vsts"></a>VSTS に移行または新しいモジュールコードをチェックイン

コードの移行プロセスまたは開発活動の一環として、モデル ソース ファイルと関連するテスト モデル ソース ファイルを VSTS にチェックインすることをお勧めします。 LCS 移行サービスを使用してコードを移行した場合、自動的に行われます。 VSTS にコードをチェックインせずに直接チェックインする場合は、VSTS フォルダ構造の特定のガイドラインに従う必要があります。 これは、適切なビルド定義の設定に役立ちます。 すべてのモジュールをルート フォルダー**メタデータ**に追加する必要があります。 各モジュールにはフォルダーが 2 つ必要です。 1 つのフォルダーには、すべてのモデルが含まれています。 他のフォルダーには、そのモジュールの記述子 XML が含まれている必要があります。 

![VSTS フォルダー構造](media/build-trunk-main-metadata.png)

### <a name="deploy-developer-topology-developer-and-build-vm"></a>開発者トポロジの配置 (開発者とビルド VM)

1. LCS ポータルで、VSTS に接続されているプロジェクトを選択します。
2. **環境**ウィンドウで、**+** をクリックして新しい環境を配置します。

   ![Azure の設定](media/azure-settings.png)

3. **環境のトポロジの選択**ウィンドウで、**Azure** を選択します。

   ![環境のトポロジの選択](media/select-environment-topology.png)

4. DEV/TEST 環境の展開に進みます。
   -   LCS プロジェクトのタイプによっては、以下に説明する配置ステップの一部が異なる場合があります。

5. **環境の配置**ウィンドウで、配置のための環境名を入力し、**開発者** VM のインスタンスの番号を選択します。
   > [!NOTE]
   > 1 つのビルド VM および 1 つの開発者向け VM のみを展開することができます。 開発者 VM を導入しない場合、インスタンスの数をゼロに設定します。 

   複数の開発者 VM が必要な場合、開発者 VM ごとに新しい環境を展開します。

   [![配置](./media/deploy-1024x669.jpg)](./media/deploy.jpg)

6. **詳細設定**をクリックし、**Visual Studio Team Services** を選択します。
   1.  ビルド エージェント名: VSTS ビルド エージェントのフレンドリ名
   2.  ビルド エージェント プール: ビルド マシンの配置に使用するビルド エージェント プール名を指定します。 VSTS に少なくとも 1 つのエージェント プールが含まれていることを確認します。 既定では、既定のプールがあります。 既定のプールを削除した場合は、ビルド配置は失敗します。
   3.  分岐名: ビルド VM の既定のソース コード同期場所になる VSTS ソース コード ブランチを指定します。 既定の分岐は、「メイン」です。

   ![設定](media/settings.jpg)

7. 設定が確認されたら、**次へ**をクリックして展開を開始します。 展開の進捗状況は **環境** の下に表示されます。
8. 配置が完了したら、リモート デスクトップを使用して、開発者とビルド VMを表示することができます。

## <a name="use-a-developer-vm-environment"></a>開発者 VM 環境の使用
開発者 VM が配置されると、ソース管理 (VSTS) からのコードの同期に使用されるワークスペースで開発者 VM が自動構成されます。 この開発者 VM には Microsoft Dynamics 365 for Finance and Operations が配置されているため、テスト VM として使用することもできます。

### <a name="configure-visual-studio-to-connect-to-vsts"></a>VSTS に接続するように Visual Studio をコンフィギュレーションする

開発者 VM で初めて Visual Studio を開くときは、自分の資格情報を使用して VSTS に接続します。

1.  **チーム エクスプローラー**を開き、**チーム プロジェクトの選択**を開きます。
2.  VSTS URL を入力し、**OK** をクリックします。 VSTS ユーザー名とパスワードを求められます。
3.  VSTS にログインした後、開発に使用する**既定のワークスペース**。

    ![ワークスペースの管理](media/manage-workspaces.png)

## <a name="test-integration-with-the-build"></a>ビルドとのテスト統合
テストと検証のためのビルド プロセスの一部としてテストを統合するには、2 つの方法があります。

-   単位とコンポーネントのレベル テストに基づく SysTest フレームワーク。
-   自動化されたテストの実行の XML を記録するタスク レコーダーから、コードを生成します。

これら 2 つの方法の詳細については、[テストと検証](testing-validation.md) を参照してください。テストおよび検証の戦略についてはこの記事を確認してください。

## <a name="use-the-build-vm-environment"></a>ビルド VM 環境の使用
LCS を通じて開発者トポロジにビルド VM が配置されると、それは事前に構成され、ビルドを開始する準備ができます。 Visual Studio IDE または VSTS インターフェイスから、いつでも既定の構成を変更することができます。 ビルド VM では、簡単なビルドのセットアップのために、モジュール ソース コードがビルド コンピューターに同期されます。 ビルド マシンは、ビルド エージェント、ビルド コントローラー、ビルド プロセス テンプレート、ビルド定義のデフォルト設定で自動構成されています。 ビルドに成功したら、ビルド定義と統合されているテストが実行されます。

### <a name="review-a-pre-configured-customizable-build-environment"></a>定義済みのカスタマイズ可能なビルド環境を確認

ビルド VM には、TFS 2015 の一部としてリリースされた vNext ビルド エージェントが含まれています。 ビルド VM を配置するときは、既定では VSTS プロジェクトと接続して同期するようにビルド エージェントが構成されます。 ビルド VM 構成の一部として、以下に示すようにデフォルトのビルド定義も作成および構成されます。 

[![Build1](./media/build1-1024x488.jpg)](./media/build1.jpg) 

既定のビルド定義には、以下で説明するように、特定の操作を実行する複数のタスクが含まれています。

1.  ビルドに渡す事前定義済の変数パラメータをコンフィギュレーションします。 ビルド実行ごとにクリーンなデータベースを設定するには、**DatabaseBackupToRestore**変数のデータベース バックアップ ファイルの名前を指定します。 パッケージ フォルダーは、すべてのビルド時にクリーン パッケージ フォルダーのコピーで復元されます。

    [![build2](./media/build2-1024x678.jpg)](./media/build2.jpg)

2.  以下のように、「トランク/メイン」ブランチにあるすべてのモジュールを検出して構築するためにソリューションをビルドします。

    [![Build3](./media/build3-1024x456.jpg)](./media/build3.jpg)

3.  「レポートの展開」タスクを使用して、レポートを生成し、ビルド VM に展開します。
4.  「データベース同期」タスクを使用して、データベースをビルド VM 上のローカル SQL に同期させます。
5.  ビルドが成功した後、サンドボックス/ステージング環境を更新するために使用できる配置可能なパッケージを作成します。

    [![Build4](./media/build4-1024x462.jpg)](./media/build4.jpg)

6.  「ビルド コンポーネントのコピーと発行」は、配置可能パッケージを VSTS コンポーネントの場所にアップロードします。

    [![build5](./media/build5-1024x439.jpg)](./media/build5.jpg)

7.  テストの実行については、3 つの既定のタスク「テスト設定」、「テストの実行」、および「テストの終了」があります。

    [![build7](./media/build7-1024x457.jpg)](./media/build7.jpg)

8.  既定のビルドでは毎日午後 5 時に開始される予定です。 チームの必要性に従って、各チェックインでトリガーを「継続」に変更することができます。

    [![build8](./media/build8-1024x491.jpg)](./media/build8.jpg)

既定の構成に変更を加えて、そのビルド VM がビルドをトリガーできるようにすることができます。

## <a name="start-a-build-and-verify-the-build-and-test-execution-results"></a>ビルドを開始し、ビルドとテストの実行結果を確認します。
既定のビルド構成を確認した後は、Visual Studio IDE または VSTS Web インターフェイスからビルドを手動でトリガーできます。

1.  ブラウザーを開き、VSTS URL に接続します。
2.  資格情報を使用してをログインします。
3.  ホーム ページの**最近のプロジェクトとソリューション**で、プロジェクトを選択します。
4.  上部リンク オプションから、**ビルド**を選択します。
5.  左側のパネルで、既定のビルド定義インスタンスを選択します。
6.  右クリックし、**キュー ビルド** を選択して VSTS ソース管理に既にチェックインしているモジュールおよびテスト モジュールのビルドをトリガーします。

[![image045](./media/image045.png)](./media/image045.png) 

次の例に示すように、ビルドの成功または失敗が表示されます。 すべてのビルドを表示します。 

[![build9](./media/build9-1024x443.jpg)](./media/build9.jpg) 

特定の完了したビルドとビューの成功/失敗の詳細を選択します。 

[![build10](./media/build10-1024x446.jpg)](./media/build10.jpg) テストリンクをクリックして、テスト実行の失敗を視覚化します。 

[![build11](./media/build11-1024x455.jpg)](./media/build11.jpg)

