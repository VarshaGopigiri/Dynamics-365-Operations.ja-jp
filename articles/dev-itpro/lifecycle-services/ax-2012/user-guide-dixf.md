---
title: "データのインポート/エクスポート フレームワークのユーザー ガイド (AX 2012)"
description: "このトピックでは、Dynamics AX でデータ インポート/エクスポート フレームワーク (DIXF) を使用する方法について説明します。"
author: kfend
manager: AnnBe
ms.date: 10/27/2017
ms.topic: article
ms.prod: dynamics-ax-2012
ms.service: 
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: AX 2012
ms.custom: 18121
ms.assetid: 393101f6-54b0-4198-a31c-3ff3125f33da
ms.search.region: Global
ms.author: kfend
ms.search.validFrom: 
ms.dyn365.ops.version: 2012
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 6e453743048625e18bcefafbae45da33048e317e
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="data-importexport-framework-user-guide-ax-2012"></a>データのインポート/エクスポート フレームワークのユーザー ガイド (AX 2012)

[!include [banner](../../includes/banner.md)]

さまざまなバージョンのデータのインポート/エクスポート フレームワークを利用できます。 使用するバージョンは、ご使用の環境で実行する Microsoft Dynamics AX のバージョンによって異なります。

-   Microsoft Dynamics AX 2012 R3 で、そのリリースに含まれるデータのインポート/エクスポート フレームワークのバージョンを使用します。
-   Microsoft Dynamics AX 2012 R2 で、Microsoft Dynamics AX 2012 R2 の累積更新 7 で利用できるデータのインポート/エクスポート フレームワークのバージョンを使用します。
-   AX 2012 または Microsoft Dynamics AX 2012 Feature Pack で、[Lifecycle Services のダウンロード可能ツール (旧 InformationSource)](lcs-downloadable-tools-formerly-informationsource.md) から使用可能なデータのインポート/エクスポート フレームワークのバージョンを使用します。

| **メモ**                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 累積的な更新 7 のデータのインポート/エクスポート フレームワークおよび and Microsoft Dynamics AX 2012 R3 には、LCS からダウンロードできるバージョンでは使用できない機能が含まれています。 詳細については、[データのインポート/エクスポート フレームワークを使用する移行データ (DIXF, DMF)](migrate-data-dixf.md) を参照してください。 |

## <a name="architecture"></a>アーキテクチャ
次の図は、データ インポート/エクスポート フレームワークのアーキテクチャを示しています。 

![データ移行フレームワークのアーキテクチャ図](./media/dmfarchitecture.png) 

データのインポート/エクスポート フレームワークは、対象のテーブルが置かれている Microsoft Dynamics AX データベースに各エンティティのステージング テーブルを作成します。 移行中のデータは、まずステージング テーブルに移動されます。 そこでは、データを検証し、必要なクリーンアップまたは変換を実行できます。 その後、データをターゲット テーブルに移動またはエクスポートすることができます。

## <a name="the-importexport-process"></a>プロセスをインポート/エクスポート
次の図は、Microsoft Dynamics AX でデータをインポートまたはエクスポートするために必要な手順を示しています。 ![データ移行フレームワークのコンフィギュレーション図](./media/dmfconfiguration.png)
1.  エクスポートまたはインポートするデータのソースを特定し、そのデータのソース データ形式を作成します。 エクスポートについては、ソースは **AX** です。 インポートについては、次のソースのいずれかを使用できます。
    -   **AX** - 別の Microsoft Dynamics AX インスタンスからデータをインポートします。
    -   **ODBC** – Microsoft SQL Server または Microsoft Access などの別のデータベースからデータをインポートします。
    -   **ファイル** – 固定長からデータをインポートまたはテキスト ファイル、XML ファイルまたは Microsoft Excel ファイルの区切り。

    ソース データ フォーマットを作成する方法の詳細については、[データのインポート/エクスポート フレームワークを使用する移行データ (DIXF、DMF)](migrate-data-dixf.md) を参照してください。
2.  データに関連付けるエンティティを決定します。 このエンティティは、エクスポート データのソースまたはインポート データのターゲットのいずれかです。 既存のエンティティを使用、またはカスタム エンティティを作成することができます。 利用可能なエンティティの一覧については、[データのインポート/エクスポート フレームワークのエンティティ (DIXF、DMF)](entities-dixf.md) を参照してください。 カスタム エンティティを作成する方法の詳細については、[データのインポート/エクスポート フレームワークのカスタム ターゲット エンティティを作成する (DIXF、DMF)](create-custom-target-entity-dixf.md) を参照してください。
3.  どのエンティティをインポートまたはエクスポートするかを決定し、すべてのエンティティを処理グループに入れます。 処理グループは、順番に処理する必要があるか、論理的にグループ化できる一連のエンティティです。 処理グループ内のエンティティは、一緒にエクスポートされるか、ソースからステージングに、次にステージングからターゲットにインポートされます。 処理グループでは、各エンティティをソース データの形式とも関連付けます。 処理グループを作成する方法の詳細については、[データのインポート/エクスポート フレームワークを使用する移行データ (DIXF、DMF)](migrate-data-dixf.md) を参照してください。
4.  データのエクスポートまたはインポートするには、処理グループのオプションを使用します。 インスポートについては、必要に応じて、データをクリーンアップまたは変換できるステージング テーブルに、データをまず移動します。 データが正確で表示され、参照データが正しくマップされていることを検証する必要があります。 次に、ステージング テーブルからターゲット テーブルにデータを移行します。 エンティティが対象のテーブルに正確に表示されることを検証する必要があります。

    | **重要**                                                                                                                                            |
    |----------------------------------------------------------------------------------------------------------------------------------------------------------|
    | ステージング データにはビジネス情報が含まれる場合があります。 したがって、移行が完了した後でステージング データを削除することを強くお勧めします。 |

    エクスポートについては、必要に応じて、データをクリーンアップまたは変換できるステージング テーブルに、ソースからデータも移動します。 次に、Microsoft Dynamics AX またはファイルのいずれかに、データをエクスポートします。 最初のオプションは、別の Microsoft Dynamics AX インスタンスにインポートできるように、データの .dat ファイルと .def ファイルを作成します。 2 番目のオプションは、データのフラット ファイルを作成します。





