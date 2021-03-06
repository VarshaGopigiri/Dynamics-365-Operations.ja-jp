---
title: "Sharepoint からのデータのインポートの構成"
description: "このトピックでは、Microsoft SharePoint からデータをインポートする方法について説明します。"
author: NickSelin
manager: AnnBe
ms.date: 05/21/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Application User, Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Core, Operations
ms.custom: 220314
ms.assetid: 2685df16-5ec8-4fd7-9495-c0f653e82567
ms.search.region: Global
ms.author: nselin
ms.search.validFrom: 2018-04-01
ms.dyn365.ops.version: Release 8.0
ms.translationtype: HT
ms.sourcegitcommit: 2fc887668171175d436b9eb281a35c1c9d089591
ms.openlocfilehash: 4285db9c71208bce45d64933e692a25ef3f46b26
ms.contentlocale: ja-jp
ms.lasthandoff: 05/25/2018

---
# <a name="configure-data-import-from-sharepoint"></a>Sharepoint からのデータのインポートの構成

[!include[banner](../includes/banner.md)]

電子申告 (ER) フレームワークを使用して受信ファイルからデータをインポートするには、インポート処理をサポートする ER 形式をコンフィギュレーションし、データ ソースとしてその形式を使用する**宛先**タイプのモデル マッピングを実行する必要があります。 データをインポートするには、インポートするファイルに移動する必要があります。 受信ファイルは、ユーザーにより手動で選択できます。 Microsoft Sharepoint からのデータのインポートをサポートするための新しい ER 機能を使用すると、このプロセスを無人プロセスとして構成できます。 ER コンフィギュレーションを使用して、Microsoft SharePoint フォルダーに格納されているファイルからデータのインポートを実行できます。 このトピックでは、SharePoint から Microsoft Dynamics 365 for Finance and Operations へのインポートを完了する方法について説明します。 例では、業務データとして仕入先トランザクションを使用します。

## <a name="prerequisites"></a>前提条件
このトピックの例を完了するには、次のアクセスが必要です:

- 次のロールのいずれか 1 つのために Finance and Operations にアクセスします:

    - 電子申告開発者
    - 電子申告機能コンサルタント
    - システム管理者

- Finance and Operations で使用するようにコンフィギュレーションされた Microsoft SharePoint Server のインスタンスへのアクセス
- 1099 支払の ER 形式およびモデル コンフィギュレーション

### <a name="create-required-er-configurations"></a>必須な ER コンフィギュレーションの作成
**7.5.4.3 IT サービス/ソリューション コンポーネントの取得/開発 (10677)** 業務プロセスの一部である **Microsoft Excel ファイルからの ER インポート データ**タスク ガイドを再生します。 これらのタスク ガイドでは、デザインのプロセスおよび外部の Microsoft Excel ファイルから仕入先トランザクションを対話型でインポートする ER コンフィギュレーションの使用について説明します。 詳細については、[Microsoft Excel で受信ドキュメントを解析する](parse-incoming-documents-excel.md) を参照してください。 最後に、次のものがあります。

- ER コンフィギュレーション

    - ER モデル構成、**1099 支払モデル**
    - ER 形式コンフィギュレーション、**Excel から仕入先のトランザクションをインポートするための形式**

[![SharePoint からデータをインポートするための ER コンフィギュレーション](./media/GERImportFromSharePoint-01-Configurations.PNG)](./media/GERImportFromSharePoint-01-Configurations.PNG)

- データのインポートに対する受信ファイルのサンプル:

    - Excel ファイル **1099import-data.xlsx** と、Finance and Operations にインポートする必要がある仕入先トランザクション

[![SharePoint からインポートするための Microsoft Excel ファイルのサンプル](./media/GERImportFromSharePoint-02-Excel.PNG)](./media/GERImportFromSharePoint-02-Excel.PNG)

> [!NOTE]
> 仕入先トランザクションをインポートするための形式が既定のモデル マッピングとして選択されます。 したがって、**1099 支払モデル**のモデル マッピングを実行し、そのモデル マッピングが**宛先**タイプの場合、モデル マッピングは外部ファイルからデータをインポートするこの形式を実行します。 続いてそのデータを使用して、アプリケーション テーブルを更新します。

## <a name="configure-document-management-parameters"></a>ドキュメント管理パラメーターのコンフィギュレーション
1. **ドキュメント管理パラメーター**ページで、現在サインインしている会社により使用される SharePoint Server インスタンスへのアクセスをコンフィギュレーションします。 この例では、会社は USMF です。
2. アクセス権があることを確認するために、SharePoint Server インスタンスへの接続をテストします。

[![ドキュメント管理設定 – SharePoint サーバー](./media/GERImportFromSharePoint-03-SharePointSetup.png)](./media/GERImportFromSharePoint-03-SharePointSetup.png)

3. コンフィギュレーション済の SharePoint サイトを開き、受信ファイルが格納されるフォルダーを作成します。

    - ファイルのインポート ソース (メイン)
    - ファイルのインポート ソース (代替)

[![ドキュメント管理設定 – SharePoint サーバー](./media/GERImportFromSharePoint-04-SharePointFolder1.png)](./media/GERImportFromSharePoint-04-SharePointFolder1.png)

[![ドキュメント管理設定 – SharePoint サーバー](./media/GERImportFromSharePoint-05-SharePointFolder2.png)](./media/GERImportFromSharePoint-05-SharePointFolder2.png)

4. Finance and Operations では、**ドキュメント タイプ**ページで、作成した SharePoint フォルダーにアクセスするために使用される次のドキュメント タイプを作成します。

    - SP メイン
    - SP 代替

5. ドキュメント タイプについては、**グループ**フィールドに**ファイル**を入力し、**場所**フィールドに **SharePoint** を入力します。 SharePoint フォルダのアドレスを入力します。

    - **SP メイン**ドキュメント タイプ用: ファイルのインポート ソース (メイン)
    - **SP 代替**ドキュメント タイプ用: ファイルのインポート ソース (代替)

[![SharePoint 設定 – 新しいドキュメント タイプ](./media/GERImportFromSharePoint-06-SharePointDocumentTypesSetup.png)](./media/GERImportFromSharePoint-06-SharePointDocumentTypesSetup.png)

## <a name="configure-er-sources-for-the-er-format"></a>ER 形式の ER ソースをコンフィギュレーションします。
1. **組織管理** > **電子申告** > **電子申告ソース**の順にクリックします。
2. **電子申告ソース**ページで、コンフィギュレーション済の ER 形式を使用してデータ インポートのソース ファイルをコンフィギュレーションします。
3. .Xlsx 拡張子のファイルのみがインポートされるように、ファイル名マスクを定義します。 ファイル名マスクはオプションであり、定義された場合にのみ使用されます。 ER 形式ごとにマスクを 1 つだけ定義できます。
4. 以前に作成した両方の SharePoint フォルダーを選択します。

[![ER ファイル ソースの設定](./media/GERImportFromSharePoint-07-FormatSourceSetup.PNG)](./media/GERImportFromSharePoint-07-FormatSourceSetup.PNG)

> [!NOTE]
>ER *ソース*は、アプリケーションの会社ごとに個別に定義されます。 対照的に、ER *コンフィギュレーション*は会社間で共有されます。

> [!NOTE]
> ER 形式の ER ソース設定を削除すると、接続されているすべてのファイルの状態 (以下を参照) も削除されます。

## <a name="review-the-files-states-for-the-er-format"></a>ER 形式のファイルの状態を確認します。
1. **電子申告ソース**ページで、**ソースのファイル状態**を選択して現在の ER 形式のコンフィギュレーション済ファイル ソースの内容を確認します。
2. **ファイル**セクションで、ファイルの一覧を確認します。 このリストは、次のものを表します。

    - 該当するソース ファイルは、ファイル名マスク (ファイル名マスクが定義されている場合) に基づいており 、データのインポートの準備が整っています。 これらのファイルについては、**インポート フォーマットのソース ログ**セクションは空白になります。
    - 以前にインポートされたファイル。 これらの各ファイルについては、**インポート フォーマットのソース ログ**セクションで、このファイルのインポートの履歴を確認できます。

**組織管理** \> **電子申告** \> **ソースのファイルの状態**の順に選択することにより、**ソースのファイルの状態**ページを開くこともできます。 この場合、ページではすべての ER 形式のファイル ソースに関する情報、つまりファイル ソースが現在サインインしている会社でコンフィギュレーションされたという情報が提供されます。

## <a name="import-data-from-excel-files-that-are-in-a-sharepoint-folder"></a>SharePoint フォルダーにある Excel ファイルからのデータをインポートします。
1. SharePoint では、仕入先トランザクションを含む Microsoft Excel ファイル **1099import data.xlsx** を、以前に作成した**ファイルのインポート ソース (メイン)** SharePoint フォルダにアップロードします。

[![SharePoint コンテンツ – インポート用 Microsoft Excel ファイル](./media/GERImportFromSharePoint-08-UploadFile.png)](./media/GERImportFromSharePoint-08-UploadFile.png)

2. Finance and Operations では、**ソースのファイルの状態**ページで、**更新**を選択してページを更新します。 このフォームで表示される SharePoint にアップロードされた Excel ファイルのステータスが**準備完了**となることに注意してください。 次のステータスは、現在サポートされています。

    - **準備完了** - SharePoint フォルダで新しいファイルごとに自動的に割り当てられます。 このステータスは、ファイルがインポートの準備ができていることを意味します。
    - **インポート中** - 他のプロセス (それらの多くが同時に実行されている場合) による使用を防ぐためにインポート プロセスによってファイルがロックされるときに、ER レポートによって自動的に割り当てられます。
    - **インポート済** - ファイルのインポートが正常に完了するときに、ER レポートによって自動的に割り当てられます。 このステータスは、インポートされたファイルがコンフィギュレーション済ファイル ソース (SharePoint フォルダ) から削除されたことを意味します。
    - **失敗** - ファイルのインポートがエラーまたは例外で完了するときに、ER レポートによって自動的に割り当てられます。
    - **保留中** - このフォーム上のユーザーによって手動で割り当てられます。 このステータスは、ファイルが現在インポートされないことを意味します。 このステータスは、いくつかのファイルのインポートを延期するために使用されます。

[![選択したソースの ER ファイル状態のページ](./media/GERImportFromSharePoint-09-FileStatesForm.png)](./media/GERImportFromSharePoint-09-FileStatesForm.png)

## <a name="import-data-from-sharepoint-files"></a>SharePoint ファイルからデータをインポート
1. ER コンフィギュレーション ツリーを開き、**1099 支払モデル**を選択し、ER モデル コンポーネントの一覧を展開します。
2. 選択した ER モデル構成のモデルのマッピングの一覧を開くためのモデル マッピングの名前を選択します。

[![選択したソースの ER ファイル状態のページ](./media/GERImportFromSharePoint-10-SelectModelMapping.PNG)](./media/GERImportFromSharePoint-10-SelectModelMapping.PNG)

3. **実行**を選択し、選択したモデル マッピングを実行します。 ER 形式のファイル ソースをコンフィギュレーションしたため、必要な**ファイル ソース**オプションの設定を変更できます。 このオプションの設定を維持すると、コンフィギュレーション済ソース (この例では SharePoint フォルダ) から .xslx ファイルがインポートされます。

    この例では、1 つだけファイルをインポートしています。 ただし、複数のファイルがある場合、SharePoint フォルダに追加された順序でインポートするよう選択されます。 ER 形式の各実行で、単一の選択されたファイルをインポートします。

[![ER モデル マッピングの実行](./media/GERImportFromSharePoint-11-RunModelMapping.PNG)](./media/GERImportFromSharePoint-11-RunModelMapping.PNG)

4. モデル マッピングはバッチ モードで無人で実行できます。 この場合、バッチがこの ER 形式を実行するたびに、単一のファイルがコンフィギュレーションされたファイル ソースからインポートされます。 このバッチの実行を実装するには、次のコードを使用します。

    ```
    ERObjectsFactory::createMappingDestinationRunByImportFormatMappingId().run()
    ```

    SharePoint フォルダからファイルが正常にインポートされない場合、そのフォルダーから削除されます。

5. **V-00001** などの伝票 ID を入力し、**OK** を選択します。

[![ER モデル マッピングの実行](./media/GERImportFromSharePoint-12-ModelMappingRunFinished.PNG)](./media/GERImportFromSharePoint-12-ModelMappingRunFinished.PNG)

6. **ソースのファイルの状態**ページで、**更新**を選択してページを更新します。

[![選択したソースの ER ファイル状態のページ](./media/GERImportFromSharePoint-13-FileStatesForm.PNG)](./media/GERImportFromSharePoint-13-FileStatesForm.PNG)

7. **ファイル**セクションで、ファイルの一覧を確認します。 **インポート フォーマットのソース ログ**セクションでは、Excel ファイルのインポートの履歴を提供します。 このファイルが正常にインポートされなかったため、SharePoint フォルダで**削除**としてマークされます。
8. **ファイルのインポート ソース (メイン)** SharePoint フォルダを確認します。 正常にインポートされた Excel ファイルは、このフォルダーから削除されました。
9. Finance and Operations で、**買掛金管理** \> **定期処理のタスク** \> **税金 1099** \> **1099 の仕入先決済**の順に選択します。
10. **開始日**および**終了日**フィールドに、適切な値を入力します。 **手動 1099 トランザクション**を選択します。

    伝票 **V-00001** として SharePoint 上の Excel ファイルからインポートされた仕入先トランザクションが、ページに表示されます。

[![1099 仕入先トランザクション ページ](./media/GERImportFromSharePoint-14-ImportedTransactions.PNG)](./media/GERImportFromSharePoint-14-ImportedTransactions.PNG)

## <a name="prepare-an-excel-file-for-import"></a>インポート用 Excel ファイルの準備
1. 以前に使用した Excel ファイルを開きます。 行 3 列 1で、アプリケーションに存在しない仕入先コードを追加します。 行に追加の false 仕入先情報を追加します。

[![SharePoint からインポートするための Microsoft Excel ファイルのサンプル](./media/GERImportFromSharePoint-15-Excel.PNG)](./media/GERImportFromSharePoint-15-Excel.PNG)

2. 仕入先トランザクションを含む更新済 Excel ファイルを**ファイルのインポート ソース (メイン)** SharePoint フォルダにアップロードします。
3. Finance and Operations で、ER コンフィギュレーション ツリーを開き、**1099 支払モデル**を選択し、ER モデル コンポーネントの一覧を展開します。
4. データのインポート処理中に不適切な仕入先コードがエラーと見なされるよう、モデル マッピングを更新するモデル マッピングの名前を選択します。
5. **デザイナー** をクリックします。
6. **検証**タブで、アプリケーションでインポートされた仕入先勘定が存在するかどうかを評価するようコンフィギュレーションされた、検証ルールの検証後のアクションを変更する必要があります。 **後検証アクション**フィールドの値を**実行停止**に更新し、変更内容を保存し、ページを閉じます。

[![ER モデル マッピング デザイナーのページ](./media/GERImportFromSharePoint-16-UpdateModelMapping.PNG)](./media/GERImportFromSharePoint-16-UpdateModelMapping.PNG)

7. 変更内容を保存し、ER モデル マッピング デザイナーを閉じます。
8. **実行**を選択し、変更した ER モデル マッピングを実行します。
9. **V-00002** などの伝票 ID を入力し、**OK** を選択します。

    SharePoint フォルダ ファイルに存在していることを示す通知には、正しくない仕入先勘定が含まれインポートできないという情報ログが含まれることに注意してください。

[![ER モデル マッピングの実行](./media/GERImportFromSharePoint-17-ModelMappingRunFinished.PNG)](./media/GERImportFromSharePoint-17-ModelMappingRunFinished.PNG)

10. **ソースのファイルの状態**ページで**更新**を選択し、次に**ファイル**セクションでファイルの一覧を確認します。

[![選択したソースの ER ファイル状態のページ](./media/GERImportFromSharePoint-18-FileStatesForm.PNG)](./media/GERImportFromSharePoint-18-FileStatesForm.PNG)

**インポート フォーマットのソース ログ**セクションでは、インポート プロセスが失敗したこと、およびファイルがまだ SharePoint フォルダーの中にあることを示します (**削除済**チェック ボックスが選択されていません)。 適切な仕入先コードを追加し、**インポート フォーマットのソース ログ**セクションでファイルのステータスを**失敗**から**準備完了**に変更することにより SharePoint でこのファイルを修正する場合、もう一度ファイルをインポートできます。

11. **ファイルのインポート ソース (メイン)** SharePoint フォルダを確認します。 インポートされなかった Excel ファイルがまだこのフォルダ内にあることを通知します。
12. Finance and Operations で、**買掛金勘定** \> **定期処理のタスク** \> **税金 1099** \> **1099 の仕入先決済**の順に選択し、**開始日**および**終了日**フィールドで適切な値を入力し、**手動 1099 トランザクション**を選択します。

    伝票 V-00001 のトランザクションのみが使用可能です。 Excel ファイルで最後にインポートされたトランザクションのエラーが見つかった場合でも、伝票 V-00002 のトランザクションは存在しません。

