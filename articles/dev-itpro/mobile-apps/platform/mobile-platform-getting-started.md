---
title: "モバイル プラットフォームの概要"
description: "このトピックでは、モバイル プラットフォームでの開発方法について説明します。"
author: makhabaz
manager: AnnBe
ms.date: 07/01/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 255544
ms.assetid: f5aa0c60-25cc-4453-8df9-efab19b7e272
ms.search.region: Global
ms.author: makhabaz
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Platform update 9
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: bb3b6715efbd9eea40c96e8522dba70d9c9b4a30
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="getting-started-with-the-mobile-platform"></a>モバイル プラットフォームの概要

[!include [banner](../../includes/banner.md)]

開発環境を取得した後、開発を開始するために次の手順を実行します。

### <a name="get-the-fleet-management-mobile-forms"></a>フリーと管理モバイル フォームを取得する

**フリート管理** モジュール内に新しい専用のフォームを作成しました。 これらのフォームはモバイル アプリケーション専用に使用されており、Web クライアントからは使用されません。

1.  [フリート管理プロジェクトを含むファイルをダウンロードする](https://github.com/Microsoft/Dynamics365-for-Operations-mobile-FleetManagementSamples) (.axpp ファイル)。
2.  ZIP ファイルの内容を開発用コンピュータの一時的な場所に抽出します。
3.  Microsoft Visual Studio を使用して、プロジェクト (.axpp) ファイルをインポートします (**Finance and Operations** &gt; **プロジェクトのインポート**をクリックします)。
4.  プロジェクト ファイルをインポートした後は、プロジェクトまたはモジュールをビルドします。

### <a name="get-the-sample-workspace"></a>サンプル ワークスペースを取得します

引当管理のためのサンプルのワークスペースを提供します。 このワークスペースは、**フリート管理**モジュールに基づいています。

1.  [サンプル ワークスペースを含むファイルをダウンロードする](https://github.com/Microsoft/Dynamics365-for-Operations-mobile-FleetManagementSamples) (.xml ファイル)。
2.  非生産クライアントにログインします。 (Finance and Operations 管理者向けの Microsoft Dynamics 365 としてサインインする必要があります。)
3.  アドレス バーで、**&mode=mobile** を URL の末尾に追加してから Enter キーを押します。
4.  クライアントで、**設定** &gt; **モバイル アプリ**と移動します。 モバイル アプリ デザイナーは、Finance and Operations クライアントの横にドッキングして表示されます。
5.  **オーバーフロー** ボタン (**…**) をクリックし、**インポート**をクリックします。
6.  ページの下部に表示される**参照**ボタンをクリックします。
7.  表示されるファイル選択ダイアログ ボックスで、以前に zip ファイルから抽出した XML ファイルのいずれかを選択します。
8.  アプリがモバイル アプリ デザイナーに読み込まれた後、ページの下部にある**完了**をクリックします。
9.  **ワークスペースの公開**をクリックします。

### <a name="get-the-mobile-app"></a>モバイル アプリの取得

モバイル アプリは、最も一般的なモバイル オペレーティング システムで利用可能です。 アプリケーションにログインするためには、Dynamics 365 Unified Operations のインスタンスと、有効なユーザー資格情報が必要です。

-   Android (現在利用可能) - [Google Play ストア上の Microsoft Dynamics 365 Unified Operations](https://play.google.com/store/apps/details?id=com.microsoft.dynamics365.operations.mobile)
-   iPhone (現在利用可能) - [iTunes アプリ ストア 上の Microsoft Dynamics 365 Unified Operations](https://itunes.apple.com/us/app/dynamics-365-for-operations/id1180836730?mt=8)

完了です モバイル デバイスからアプリを起動してサンプル ワークスペースを表示します。

### <a name="additional-resources"></a>その他のリソース

[アーキテクチャ](mobile-platform-architecture.md) 

[クライアント APIs リファレンス](client-apis/client-apis-reference.md)

[サーバー APIs 参照](mobile-workspace-server-apis.md)

