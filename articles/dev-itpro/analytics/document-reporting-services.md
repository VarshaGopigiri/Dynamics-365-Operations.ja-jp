---
title: "ドキュメントの Reporting Services の概要"
description: "この記事では、Microsoft Dynamics 365 for Finance and Operations で利用できる統合レポート ソリューションについて説明します。 このソリューションにより、サービス管理が簡略化され、開発者の生産性が向上し、ユーザーのレポート表示エクスペリエンスが強化されます。"
author: TJVass
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: sericks
ms.search.scope: Operations
ms.custom: 69191
ms.assetid: 57aaba22-4068-4c3f-9428-7fcd99632295
ms.search.region: Global
ms.author: tjvass
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 83c969cab9c01673f74eac1bddf2fc00fb90f32b
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="document-reporting-services-overview"></a>ドキュメントの Reporting Services の概要

[!include [banner](../includes/banner.md)]

この記事では、Microsoft Dynamics 365 for Finance and Operations で利用できる統合レポート ソリューションについて説明します。 このソリューションにより、サービス管理が簡略化され、開発者の生産性が向上し、ユーザーのレポート表示エクスペリエンスが強化されます。

<a name="document-reporting-services"></a>ドキュメントの Reporting Services
---------------------------

Document Reporting Services は、Microsoft SQL Server Reporting Services (SSRS) に基づいています。 現在のバージョンの Microsoft Dynamics 365 for Finance and Operations では、これらのサービスは Microsoft Azure 計算サービスでホストされます。 1 ボックス環境で開発している場合は、サービスも Azure コンピューティング エミュレーターでローカルに実行されます。

### <a name="service-deployment--local-vs-cloud"></a>サービスの展開 - ローカルとクラウド

1 ボックス環境では、開発者は Microsoft Visual Studio 2015 を使用して、エンド ツー エンドでレポートを作成、変更、およびプレビューできます。 アプリケーションのメタデータ ストアにレポートを追加するために、別のプロセスは必要ありません。 レポートの変更は、他のソリューションの更新と一緒にパッケージ化され、ローカル環境での開発が完了した後にクラウドに展開されます。 

[![document-reporting-services-topology](./media/document-reporting-services-topology.png)](./media/document-reporting-services-topology.png)

### <a name="viewing-reports-in-dynamics-365-for-finance-and-operations"></a>Dynamics 365 for Finance and Operations でのプロジェクトの表示

Finance and Operations がエンドユーザーに提供する拡張レポート表示エクスペリエンスは、Microsoft Visual Studio のレポート プレビュー エクスペリエンスと同じです。 Visual Studio で個別のデザインのプレビューは以後使用しません。 代わりに、Ctrl+F5 を押すだけで、Internet Explorer ウィンドウでレポートを作成してプレビューできます。 レポートはクライアントに表示されるとおりに表示されます。 ユーザーのパラメーターの経験さえ同じです。 次のスクリーン ショットは、Visual Studio から開いたレポート プレビューの例を示しています。 

[![レポート プレビューの例](./media/2_report.png)](./media/2_report.png)

## <a name="service-administration-prerequisites"></a>サービス管理の前提条件
次のテーブルは、Microsoft Dynamics AX 2012 のサービス管理の前提条件と現在のバージョンの Finance and Operations を比較しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>AX 2012</th>
<th>Dynamics 365 for Finance and Operations の現在のバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>レポートの開発環境には、次の前提条件があります。
<ul>
<li>SSRS がインストールされている必要があります。</li>
<li>SSRS は、Reporting Services 構成マネージャーを使用して構成する必要があります。</li>
<li>Finance and Operations の SSRS 拡張機能をインストールする必要があります。</li>
</ul></td>
<td>Reporting Services は、アプリケーション サーバーとともに Azure コンピューティング エミュレーターで実行されます。 したがって、SSRS サービス管理の前提条件はありません。 レポートがローカル レポート作成サービスに配置された後は、クライアントからアクセスできます。</td>
</tr>
</tbody>
</table>

## <a name="developing-application-reports"></a>アプリケーションのレポートの開発
レポート ソリューションを完全に Visual Studio 2015 で作成および検証できるので、Finance and Operations の現在のバージョンでレポートを作成するプロセスは AX 2012 で行うよりも簡単です。 次のテーブルは、Finance and Operations がどのようにしてクエリに基づく自動設計レポートを追加するための基本手順を簡素化するかを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>AX 2012</th>
<th>Dynamics 365 for Finance and Operations の現在のバージョン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li>Microsoft Dynamics 365 for Finance and Operations クライアントで、アプリケーション オブジェクト ツリー (AOT) にクエリを作成します。</li>
<li>Visual Studio で、レポート プロジェクトを作成してクエリを追加します。</li>
<li>Visual Studioモデル エディターのレポートを編集します。</li>
<li>モデル エディタ ツールバーを使用して Visual Studio でレポート デザインをプレビューします。</li>
<li>Visual Studio を使用して、レポートを AOT に追加します。</li>
<li>クライアントの AOT を使用してレポートのメニュー項目を作成し、メニュー項目をメニューに追加します。</li>
<li>AOT を使用してレポートをレポート サーバーに展開します。</li>
<li>クライアントのレポートを確認します。</li>
</ol></td>
<td><ol>
<li>Visual Studio で、レポート プロジェクトおよびクエリを作成します。</li>
<li>Visual Studio のレポートを編集します。</li>
<li>Visual Studio で、メニュー項目にレポートを追加し、スタートアップ オブジェクトとしてメニュー項目を設定します。</li>
<li>AOT を使用してレポートをレポート サーバーに展開します。</li>
<li>Ctrl+F5 キーを押し、Finance and Operations クライアントでレポートを確認します。 <strong>注記:</strong> モデル エディタからのレポート デザインの個別のプレビューはありません。</li>
<li>ソリューション全体が完了したら、ソリューション全体を 1 つのパッケージにしてクラウドに配置します。</li>
</ol></td>
</tr>
</tbody>
</table>






