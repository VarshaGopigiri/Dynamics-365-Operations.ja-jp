---
title: "AX 2012 からのアップグレード - 切替テスト (模擬切替)"
description: "このトピックでは、AX 2012 環境をオフにしてから Dynamics 365 for Finance and Operations をオンにするまでの切替えプロセスをテストする方法について説明します。"
author: robadawy
manager: AnnBe
ms.date: 03/22/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: margoc
ms.search.scope: Operations
ms.search.region: Global
ms.author: robadawy
ms.search.validFrom: 2017-06-16
ms.dyn365.ops.version: Platform update 8
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 347052563f7e962645a94791569d376038f15f66
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="upgrade-from-ax-2012---cutover-testing-mock-cutover"></a>AX 2012 からのアップグレード - 切替テスト (模擬切替)

[!include [banner](../includes/banner.md)]

[!include [upgrade banner](../includes/upgrade-banner.md)]

*切替*という用語は、新しいシステムを稼働させる最後のプロセスに使用します。 この切替プロセスは、Microsoft Dynamics AX 2012 をオフにした後、Microsoft Dynamics 365 for Finance and Operations をオンにする前に実行されるタスクで構成されています。 アップグレード切替テスト (切替モック) の目的は、切替プロセスを練習することで、実際の切替中に関係するすべての人がスムーズに作業できるようにすることです。

切替中には、3 つの主要なワーク ストリームがあります。

- **技術的なワーク ストリーム** – このワーク ストリームには、データ アップグレードの実行プロセスが含まれています。 業務では、許可されているダウンタイムの金額に制限が適用されます。 ダウンタイムの間は、AX 2012 または Finance and Operations のいずれも利用できません。 このワーク ストリームでは、業務でのダウンタイム制限を満たすために、データ アップグレード手順をチューニングする必要があります。
- **機能的なワーク ストリーム** – このワーク ストリームには、データのアップグレードが完了した後に実行されるコンフィギュレーション タスクが含まれます。 機能的なワークストリームと技術的なワークストリームの両方が業務のダウンタイム制限内に収まる必要があるため、これらのタスクをすべて文書化および定量化し、リソースを割り当てる必要があります。
- **AX 2012 ロールバック** - このワークストリームには AX 2012 環境へのロールバックが含まれています。 ロールバックする必要はありませんが、必要な場合に備えてテスト済みのプロセスがあることが非常に重要です。

次の図は、実稼動環境で発生するような、切替中の全体的なプロセスを示しています。

![切替プロセス](./media/cutover_1.png)

モック カットオーバー プロセスは、サンドボックス環境での基本的なデータ アップグレードの検証と非常によく似ています。 そのプロセスを熟知していて、そのプロセスを既に実行済みであると仮定します。 切替モックは、次の点で異なります。

- データのアップグレード プロセスは本番環境で実行されますが、このアプローチは高速です。
- Finance and Operations の実稼働環境でのアクセスが制限されているために、Application Object Server (AOS) のサンドボックス インスタンスで以前に実行されていた一部のタスクは、Microsoft サービス エンジニアリング (DSE) チームによって実行されるようになりました。 これらのタスクには、データ アップグレード プロセスの実行が含まれます。
- 次のタスクを追加しました。
    - スモーク テストを実行します。
    - アプリケーションの設定タスクを完了します。 このステップは、使用する機能に応じて大規模になる場合があります。 このステップでは、機能チームは新しいアプリケーションの機能を構成して、アップグレードされたシステムで使用できるようにします。
    - ユーザーがシステムに戻れるようにします。 アップグレードが完了して、システムを再度使用できることをユーザーに通知します。

> [!NOTE]
> この記事では、*サンドボックス* という用語を使用して SQL Azure データベースに接続されている標準またはプレミア承認テスト (レベル 2 または 3)、またはより高度な環境を示します。

## <a name="technical-workstream"></a>技術的なワーク ストリーム

技術的なワーク ストリームに含まれるさまざまな技術チームのメンバー: データベース管理者 (DBA)、AX 2012 のシステム管理者、サーバー管理者、AX 2012 および Finance and Operations に精通している開発者。 このトピックでは、どのタスクがどのロールを含めるかについて説明します。

切替テスト中には、技術チームは、データ アップグレード プロセスのパフォーマンスと信頼性のテストに焦点を当てて、ビジネスのダウンタイム制限を満たすようにします。 ハードウェアとソフトウェアの多くの要素がこのプロセスに関連しています。 これらの要素の一部はオンプレミスですが、他の要素は Microsoft クラウドに含まれています。 加えて、カスタム アプリケーション コードと標準コードの多くの要素が含まれています。 このテストの結果は、環境の切替プロセスを信頼する必要があります。

### <a name="technical-workstream-process"></a>技術的なワーク ストリーム プロセス

> [!NOTE]
> 技術的なワークストリームについては、切替テストのプロセスは、実際/稼働の切替プロセスの高レベルの手順と同じです。

1.  Microsoft Lifecycle Services (LCS) を通じて **その他のタイプ** サービス要求を送信し、実稼働環境をアップグレードするという目的を DSE に通知します。
2.  AX 2012 AOS のインスタンスをオフにします。
3.  AX 2012 データベースのバックアップを作成し、元のデータベースのコピーに対して Transact-SQL (T-SQL) スクリプトを実行します。
4.  SQLPackage.exe という名前の無料の SQL Server ツールを使用して、コピーされたデータベースを bacpac ファイルにエクスポートします。 このツールでは、SQL データベースにインポートできる特別な種類のデータベース バックアップを提供します。
5.  bacpac ファイルを AOS マシンにアップロードします。
6.  サンドボックス環境で bacpac ファイルを Application Object Server (AOS) 仮想マシンにダウンロードし、SQLPackage.exe を使用してインポートします。 
7.  データベースがアップグレード準備完了であることを Microsoft DSE チームに通知し、サンドボックスから実稼働環境にインポートされたデータベースをコピーします。
    - DSE チームは、インポートされたデータベースに対して適切なデータ アップグレードを実行します。
    - データ アップグレードが完了すると、DSE チームにより通知されます。この時点で、ログインして、ポスト アップグレードに必要な機能構成タスクを完了し、エンド ユーザーが新しいシステムに戻ることができます。

次のセクションでは、このプロセスと [AX 2012 からのアップグレード - サンド ボックス環境でのデータ アップグレード](upgrade-data-sandbox.md) で説明されている、コア データのアップグレード プロセスとの違い、および実行する必要のある検証について説明します。

### <a name="1-submit-a-cutover-request"></a>1. 切り替え要求を送信する

**その他のタイプ** サービス要求を送信します。 Microsoft solution architect と協力して十分の通知期間 (2、3 週間前) があることを確認します。 これが切替モックであることをサービス要求で示します。
    - 既に実稼働環境をカスタマイズして配置したことを確認します。モック データベースのアップグレードは実稼働環境で発生します。
    - 切替モックは、米国太平洋標準時で月曜日から木曜日の営業時間中に実行されます。
    - 切替モックは DSE チームの空き状況に左右されますので、事前に計画してください。

詳細については、以下を参照してください。 
- [サービス要求を送信する](../lifecycle-services/submit-request-dynamics-service-engineering-team.md)
- [研修](../../fin-and-ops/imp-lifecycle/onboard.md)

### <a name="2-turn-off-the-ax-2012-aos-instances"></a>2. AX 2012 AOS インスタンスをオフにする

このタスクには、AX 2012 のシステム管理者とサーバー管理者が含まれます。

次の領域を検証する必要があります。

- **切替の時点で実行中のバッチ ジョブ** – 既に実行を開始している実行時間の長いバッチ ジョブは、システムの停止を防止します。 希望する時点で AOS インスタンスを停止できるように、事前に計画してください。 AX 2012 をオフにする前にバッチが完了するよう、バッチをスケジュールする必要があります。

- **システムの統合** – AX 2012 環境と統合されている他のシステムをお持ちかもしれません。 AX 2012 をオフにするための計画には、これらのシステムを考慮する必要があります。 たとえば、AX 2012 自体をオフにする前に、統合システムをしばらくオフにして、残りのインフライト トランザクションを完了する必要があります。 統合システムの要件は、企業間で広く異なります。 したがって、専門家チームはこのシナリオを個別に計画する必要があります。

 ### <a name="3-create-a-backup-of-the-ax-2012-database-and-run-the-t-sql-script-to-prepare-the-database"></a>3. AX 2012 データベースのバックアップを作成し、T SQL スクリプトを実行して、データベースを準備する 

このタスクには、DBA が含まれます。 バックアップは、ロールバックが必要な場合に使用されます。 また、一定の期間保持され、切替時にシステム状態を示す基準点としても使用されます。

次の領域を検証する必要があります。
- バックアップ プロセスに要する時間を正確に把握します。
- 使用されるバックアップオプション (圧縮と非圧縮など) を調整し、可能な限り高速なバックアップを保証します。

バックアップを作成した後、元のデータベースのコピーに対して T-SQL スクリプトを実行します。 (Go-Live カットオーバーの間に、元のデータベースに対して T-SQL スクリプトを実行します)。 

このスクリプトは、ユーザーを削除、AX 2012 RTM モデル ストアに関連するステップを削除、スキーマをクリーン アップ、ビューを削除、および tempDB への参照を削除によってデータベースを準備します。 環境で機能するスクリプトを変更することが必要な場合があります。 

このスクリプトは、Sandbox データ アップグレード トピックの「[T SQL スクリプトを実行して、データベースを準備する](upgrade-data-sandbox.md#run-the-t-sql-script-to-prepare-the-database)」セクションにあります。 


### <a name="4-export-the-database-to-a-bacpac-file"></a>4. データベースを bacpac ファイルにエクスポートする

このタスクには、DBA が含まれます。 このタスクの出力は、新しいシステムの Microsoft Azure にアップロードされるエクスポート ファイルです。 サンドボックス データのアップグレード トピックの[コピーしたデータベースをエクスポート](./upgrade-data-sandbox.md#export-the-copied-database-to-a-bacpac-file)セクションで説明されているサンドボックス環境でのデータのアップグレード テストを実行している場合、インポート プロセスをよく知っている必要があります。

次の領域を検証する必要があります。
- バックアッププロセスの具体的なタイミングを取得します。
- 可能な限り高速のエクスペリエンスを保証するために、エクスポート プロセスを最適化します。 最適化には、次のタスクが必要です。
    - CPU、ディスク I/O、メモリなどのエクスポート中にシステム リソースを測定します。
    - リソースのボトルネックが見つかった場合は、それらを軽減するための計画を作成します。 通常、より多くの必要なリソースを割り当てることでこれらのボトルネックが軽減されます。


### <a name="5-upload-the-bacpac-file-to-azure-storage-or-the-lcs-asset-library"></a>5. Azure ストレージまたは LCS 資産ライブラリに bacpac ファイルをアップロードする

このタスクには、DBA またはサーバー管理者が関与します。 このタスクの間に、bacpac ファイルは Azure に移動されます。

作成した bacpac ファイルは、Azure でホストされたサンドボックス環境の AOS 仮想マシン (VM) にコピーする必要があります。 これを引当するためのいくつかの理由があります。
   1. レベル 2 (またはそれ以上) サンドボックス環境により使用される Azure SQL データベース インスタンスには、環境自体の外からのアクセスを防ぐファイアウォール ルールがあります。
   2. Bacpac インポートのパフォーマンスは、Azure SQL データベース インスタンスとし同じ Azure データセンター コンピューターからインポートした場合、何倍も向上します。

Bacpac ファイルをサンドボックス AOS VM に移動する方法を選択することができます。 Microsoft Azure ストレージを使用することをお勧めします。Azure ストレージを使用するには、ユーザー自身のサブスクリプション (Dynamics 365 サブスクリプション自体に含まれていません) で独自の Azure ストレージ アカウントを取得する必要があります。 Azure ストレージ間でファイルを移動するのに役立つ無料のツールがあります。コマンド ラインからは[Azcopy](/azure/storage/common/storage-use-azcopy) を、GUI 操作からは [Microsoft Azure ストレージ エクスプローラー](http://azure.microsoft.com/en-us/features/storage-explorer/)を使用できます。 これらのツールのいずれかを使用して、オンプレミス環境から Azure ストレージにバックアップをアップロードします。 サンドボックス AOS VM にダウンロードすることができます。

もう 1 つの (無料) オプションは、LCS 資産ライブラリを使用することですが、アップロードやダウンロードは Azure ストレージよりも時間がかかる場合があります。 このオプションを使用するには、次のようにします。 
1. LCS でプロジェクトにログインし、アセット ライブラリに移動します。
2. データベース バックアップ タブを選択します。 
3. bacpac ファイルをアップロードします。 

その VM から LCS にログインして LCS アセット ライブラリからダウンロードすることにより、後から bacpac をサンドボックス AOS VM にダウンロードすることができます。

次の領域を検証する必要があります。
- 複数回測定することにより、アップロード プロセスの具体的なタイミングを取得します。 アップロード時間は、インターネット接続の速度と、自分の場所に関連する Azure データセンターの地理的な場所に基づいて異なります。

### <a name="6-download-and-import-the-bacpac-file-to-the-azure-sql-database"></a>6. bacpac ファイルをダウンロードして Azure SQL データベースにインポートする

このタスクには、DBA が含まれます。 このタスクの結果は、アップグレードする準備が整った SQL Azure データベースです。 サンドボックス データのアップグレード トピックの [bacpac ファイルをインポート](./upgrade-data-sandbox.md#import-the-bacpac-file-into-sql-database)セクションで説明されているサンドボックス環境でのデータのアップグレード テストを実行している場合、インポート プロセスをよく知っている必要があります。

SQL データベース インスタンスへのアクセスを制限するファイアウォール規則があるため、サンドボックス環境の AOS 仮想マシン (VM) でこのタスクを直接実行します。 ただし、AOS コンピューターを使用すると、アクセス許可を取得できます。 パフォーマンス上の理由から、bacpac ファイルを AOS コンピューターの D ドライブに配置することをお勧めします。 Azure 仮想マシンでは、D ドライブは通常、他の利用可能なディスクよりも高いパフォーマンスを持つ物理ディスクです。

次の領域を検証する必要があります。

- インポート プロセスの具体的なタイミングを取得します。
- 可能な限り高速のエクスペリエンスを保証するために、エクスポート プロセスを最適化します。 最適化作業には、エクスポート中のシステム リソースの測定が含まれます。 次にいくつか例を挙げます。
   - **AOS コンピューター:** CPU、ディスク I/O、メモリ
   - **Azure SQL データベース インスタンス:** SQL データベース スループット (DTU)。 sys.dm_resource_stats システム ビューでは、AOS コンピューターの Microsoft SQL Server Management Studio から Azure SQL DTU を監視できます。
   
- リソースのボトルネックが見つかった場合は、それらを軽減するための計画を作成します。 通常、より多くの必要なリソースを割り当てることでこれらのボトルネックが軽減されます。 
  
  > [重要] リソースのボトルネックが発生した場合には、標準またはプレミア パフォーマンス テストなどの上位の階層に属しているサンド ボックスで、このプロセスの実行が必要な場合があります。

### <a name="7-request-the-dse-team-to-start-the-data-upgrade-process"></a>7. データ アップグレード プロセスを開始する DSE チームを要求する

データベースのインポートが完了したら、DSE チームにデータベースのアップグレード準備が完了したことを通知します。 データベースがインポートされた場所 (環境名) を含めます。
DSE チームは、このタスクを実行し、古いデータベース構造が新しいシステムのスキーマに変換されます。 データベースの同期プロセスも、このタスクの一部として実行されます。 この操作は SQL でコストがかかる操作であるため、クラスター化されたインデックスがテーブルで変更された場合など、状況によってはデータベースの同期にかなりの時間がかかる場合があります。

まず、開発およびサンドボックス環境で、分析とデバッグのプロセスの実行を完了することを強くお勧めします。 サンド ボックス環境では、デバッグと分析のオプションがさらに制限されます。 目標は、切替テストを実行するときに対処する必要のある問題がほとんど、あるいはまったくないことです。

次の領域を検証する必要があります。
- インポート プロセスの具体的なタイミングを取得します。
- 最速のエクスペリエンスを保証するために、プロセスを最適化します。 最適化には、次のタスクが必要です。
    - ReleaseUpdateScriptsExecution テーブルを使用して、個々のアップグレード スクリプトのパフォーマンスを監視します。
    - パフォーマンスを最適化するためにスクリプトを調整します。 このタスクでは、スクリプトの X++ コードをカスタマイズして、データセット用に最適化する必要があります。
    - Microsoft Dynamics Lifecycle Services (LCS) の監視または Management Studio の sys.dm_resources_stats システム ビューを使用して Azure SQL DTU を監視します。 リソースがすべて使用されている場合は、より高いデータベースレベルを Microsoft DSE チームに要求する必要があります。

アップグレードが完了すると、Microsoft DSE チームから通知されます。 この時点で環境のスモーク テストを完了しエンド ユーザが新しいシステムに入る前に必要な機能コンフィギュレーション タスクを実行できます。

## <a name="functional-workstream"></a>機能的なワーク ストリーム

データのアップグレード後に、新しい環境でいくつかのコンフィギュレーション タスクが必要になります。 このワーク ストリームの目的は、すべてのコンフィギュレーション タスクを文書化および定量化し、リソースを各タスクに割り当てることで、ダウンタイム期間中にこれらのタスクを機能的なワーク ストリームとともに実行できるようにすることです。

通常、機能的なタスクでは、特定のシステム パラメータの値または他のコンフィギュレーション データの値の変更が含まれます。 これらのタスクは、機能テストのパス全体を通して識別されます。これは、切替テストとは別のアクティビティです。 このタイプのタスクが特定された場合、機能のリソースおよび開発者と共に確認する必要があります。

より大きな変更を行うには、新しいカスタム データ アップグレード スクリプトを作成して、データのアップグレード プロセス中にデータを更新する必要があります。 ただし、機能のリソースは、データのアップグレード後に新しいシステムを使用して、より小さな変更を手動で実行できます。

新しいデータのアップグレード スクリプトを持つ、より大規模な変更をテストする必要があります。 したがって、MajorVersionDataUpgrade.zip パッケージの 1 つ以上の追加の繰り返しを実行する必要があります。 手動のデータ入力のコストに対して、パッケージを再度実行するコストを比較検討することが重要です。

手動による変更のたびに、切替計画ドキュメントにタスクを追加する必要があります。 このタスクでは、次の詳細を示す必要があります。

-   タスクとは何か、また必要な作業は何か。
-   そのタスクを実行するのは誰か。
-   時間はどのくらいかかるか。

### <a name="add-users-and-perform-functionl-tests"></a>ユーザーの追加、および機能テストの実行
環境を完全に構成したときは、ユーザーを追加し、適切なテストを実行します。 

## <a name="roll-back-to-ax-2012"></a>AX 2012 にロールバックする

このタスクの目的は、AX 2012 をオフにしたときのバックアップを使用してデータベースを復元し、AX 2012 を再度オンにすることです。 統合システムの状態も復元する必要があります。 ただし、統合システムは企業間で異なるため、特定の状況に応じてこのシナリオを個別に計画する必要があります。 ロールバックする必要はありませんが、必要な場合に備えてテスト済みのプロセスがあることが非常に重要です。

