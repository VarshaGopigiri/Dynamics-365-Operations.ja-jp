---
title: "Power BI Desktop を使用して分析レポートを作成する"
description: "このトピックでは、ローカルの Entity Store データベースを使用して Power BI レポートを作成するプロセスについて説明します。"
author: MilindaV2
manager: AnnBe
ms.date: 12/18/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
ms.search.form: BIMeasurementDeployManagementEntityStore
audience: Developer, IT Pro
ms.reviewer: sericks
ms.search.scope: Core, Operations
ms.custom: 265864
ms.assetid: e253a57a-979b-4ca5-8e09-2bfce97395a5
ms.search.region: Global
ms.author: milindav
ms.search.validFrom: 2016-05-31
ms.dyn365.ops.version: Platform update 1
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: f794fc3d7cd767cfef1f2645577dfa686638b490
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="author-analytical-reports-by-using-power-bi-desktop"></a>Power BI Desktop を使用して分析レポートを作成する

[!include [banner](../includes/banner.md)]

ユーザーが power user またはビジネス アナリストである場合は、自分の組織のために多くのレポートを作成している可能性があります。 他のユーザーと共有する前に、データの書式設定と関連付けによって、Microsoft Excel でこれらのレポートを作成する場合があります。 レポートへの変更が必要な場合、組織内のユーザーから連絡が来る可能性があります。 このソリューションを使用すると、リッチでインタラクティブなレポートを簡単に作成できます。 レポート ライターは、 Microsoft Power BI デスクトップをレポート ツールとして使用できます。 その後、作成したレポートを PowerBI.com に公開できます。Power BI Desktop について詳しくは、「[Power BI Desktop で魅力的なレポートとビジュアライゼーションを作成する](https://powerbi.microsoft.com/en-us/desktop)」をご覧ください。

## <a name="accessing-the-local-entity-store-by-using-directquery"></a>DirectQuery を使用してローカル エンティティ ストアへのアクセス
Microsoft Dynamics 365 for Finance and Operations では、データ エンティティで公開されるオープン データ プロトコル (OData) のエンドポイントを使用して Microsoft Power BI レポートを作成できます。 このアプローチの限界にもかかわらず、エンティティ格納は従来のソリューションでもエンティティ格納をサポートしています。 ただし、DirectQuery は、解析ソリューションのソース データに推奨されるメソッドになりました。 DirectQuery の利点および制限の詳細については、[Power BI Desktop で DirectQuery の使用](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-use-directquery/) を参照してください。

Power BI デスクトップを使用すると、ローカルのエンティティ格納データベースに直接接続することによって、開発またはテスト環境でレポートを作成できます。 レポートに問題がなければ、管理者は、ユーザーがそれを実稼働環境に移行する支援をすることができます。 このセクションの残りの部分では、このプロセスについて説明します。

### <a name="step-1-populate-the-local-entity-store-database"></a>手順 1: ローカル エンティティ格納データベースに入力する
この例では、ローカルのエンティティ ストアで Retail 分析ソリューションが消費する集計モデルをステージングします。 Retail アプリケーションが使用するモデルは、RetailCube 集計測定で定義されています。 

1. Finance and Operations クライアントで**エンティティ格納**ページを開きます。 (**システム管理** > **設定** > **エンティティ格納**の順に選択します。) 
2. **RetailCube** 集計測定を選択し、**更新** を選択します。 
3. バック グラウンドで実行されるジョブ名を入力し、**OK** を選択します。

次の図は、集計モデルの更新頻度を設定するために使用する管理者ダイアログ ボックスを示しています。

![更新ダイアログ ボックスのコンフィギュレーション](media/Configure-refresh.png)

データをステージングするジョブの進行状況を監視するには、バッチ ジョブ監視ページを使用します。 (**システム管理** > **データベース** > **バッチ ジョブ**の順に選択します。) デモ データを使用している場合、ジョブは 1 分ほどかかります。 データがエンティティ格納に格納された後、レポートを作成できます。 

### <a name="step-2-connect-to-the-local-entity-store-database"></a>手順 2: ローカル エンティティ格納データベースに接続する
1. Power BI デスクトップを起動します。 Power BI デスクトップのアップデートがある場合は、それらをダウンロードし、適用する必要があります。 
2. Power BI **ようこそ**ページで、**データの取得**をクリックします。 

    または、Power BI デスクトップが開始すると、**データの取得** > **SQL Server** を選択します。 

    ![Power BI デスクトップ内でデータ メニューを取得します](media/Power-BI-Desktop-Get-Data.png)

3. **SQL Server データベース** ダイアログ ボックスに **.** と入力します。 サーバー名として、および **AxDW** をデータベースとして。 その後、**DirectQuery** オプションを選択します。 

    次の図は、Power BI デスクトップがローカルのエンティティ格納データベースにアクセスするための設定を示しています。

    ![ローカル エンティティ格納データベースにアクセスするための設定](media/Connect-to-SQL-Database.png)

    > [!NOTE]
    > **インポート** オプションは現在サポートされていません。

4. **OK**を選択します。 

    **ナビゲーター** ダイアログ ボックスが表示されます。 このダイアログ ボックスを使用して、レポートの対象となるテーブルとビューをエンティティ格納から選択します。 

5. 検索ボックスで、**Retail** と入力して RetailCube 集計測定に関連するエンティティについてフィルター処理します。
6. ナビゲーターに表示された **RetailCube_RetailTransDetailsView** テーブルを選択し、**読み込み** を選択します。 

レポートを作成できるようになりました。 測定およびフィールドはキャンバスにドラッグして、データおよび傾向を対話的に参照することができます。

次の図は、ローカルの Entity Store データベースをソースとして使用する基本レポートを示しています。

![Power BI デスクトップ レポート](media/Power-BI-Desktop-Report.png)

Power BI デスクトップでも、計算の作成がサポートされ、複数の集計測定のデータを組み合わせることができます。 数分で、ローカルの開発環境でデータを使用することにより分析レポートを作成することができます。 レポートに問題がなければ、それを実稼働環境に移行できます。これにより、ユーザーは、そのレポートを使用して、実稼働データにかかわることができます。

## <a name="validating-reports-in-a-demo-environment"></a>デモ環境でのレポートの検証

レポートにはデベロッパー環境のデモまたはテスト データが表示されます。 デモ環境にレポートを統合する場合は、引き続きこのレポートを PowerBI.com アカウントに公開し、Finance and Operations クライアントに固定することができます。 

