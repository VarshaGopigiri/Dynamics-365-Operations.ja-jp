---
title: "Retail SDK の拡張機能サンプル"
description: "Retail SDK には、拡張機能サンプルが含まれています。 これらのサンプルは、Retail をカスタマイズするさまざまな方法について学ぶ良い方法です。"
author: mugunthanm
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations, Retail
ms.custom: 89803
ms.assetid: 565d9e98-77eb-4495-987a-ad9e2de303cc
ms.search.region: Global
ms.search.industry: Retail
ms.author: mumani
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0, Retail July 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 63d392d65c3088e0f9e2c5587c499b2235e4828a
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="retail-sdk-extensibility-samples"></a>Retail SDK の拡張機能サンプル

[!include [banner](../../includes/banner.md)]

Retail SDK には、拡張機能サンプルが含まれています。 これらのサンプルは、Retail をカスタマイズするさまざまな方法について学ぶ良い方法です。  

Retail ソフトウェアの開発キット (SDK) には、機能拡張のサンプルが含まれています。 これらのプロジェクトを定型プロジェクトとして使用して、特定のカスタマイズを開始することができます。 たとえば、新しい commerce runtime (CRT) 拡張子を開始するには、CommerceRuntime サンプル プロジェクトのいずれかを新しいフォルダーにコピーし、プロジェクトのインポート パスを調整でき、それからプロジェクトで作業を開始できます。 ほとんどのサンプルでは、追加のステップ バイ ステップの手順は、Retail SDK\\ドキュメント フォルダーで使用可能です。 次のテーブルにサンプルの高レベルなリストを示します。
<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>サンプル名</strong></td>
<td><strong>説明</strong></td>
<td><strong>説明されているタスク</strong></td>
</tr>
<tr class="even">
<td>CrossLoyalty</td>
<td>この例には、AdventureWorks と Contoso の 2 つの小売業者が含まれています。 Contoso 小売業者は、AdventureWorks から顧客が獲得するロイヤルティ ポイントを受け付けます。 このサンプルでは、簡単な新しい CRT サービスを作成して、Retail Modern POS ボタンがクリックされたときにそのサービスを呼び出す方法を示します。 クロス ロイヤルティのシナリオをシミュレートします。 構成、CRT、Retail サーバー、Retail プロキシ、販売時点管理 (POS) (Modern POS と Cloud POS の両方) に変更があります。 この例では、最新の POS オフライン モードをサポートしています。</td>
<td><ul>
<li>新しい CRT と Retail サーバーの拡張機能、または新しいサービスを作成します。</li>
<li>個別のプロジェクトとして新しい工程を作成します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>EmailPreference</td>
<td>この例では、拡張プロパティを使用してエンティティを拡張する方法を示します。 拡張エンティティは、Microsoft Dynamics 365 for Retail とチャネル データベースの両方に保持され、POS クライアントは値へのアクセスを可能にします。 新しい値は、RetailRealtimeTransaction サービスを介して Retail に同期的に書き込まれます。 拡張機能プロパティは自動的にフローするため、CRT または Retail サーバーに必要なカスタマイズはありません。 ページ、テーブル、Real-time Service (RTS) クライアント、Commerce Data Exchange (CDX)、チャネル データベース、POS (Modern POS と Cloud POS の両方) に変更があります。 この例では、オフライン モードをサポートしていません。</td>
<td><ul>
<li>既存の Modern POS/クラウド POS の表示またはページを変更します。</li>
<li>Real-time Service を拡張します。</li>
<li>拡張プロパティを使用して、カスタム フィールド値をデータベースに格納します。</li>
</ul></td>
</tr>
<tr class="even">
<td>StoreHours</td>
<td>この例は、Retail とチャネルの両方に新しいビジネス エンティティ (StoreHours) を作成する方法を示しています。 テーブル、CDX、チャネル データベース、CRT、Retail サーバー、POS (Modern POS と Cloud POS の両方) に変更があります。 この例では、最新の POS オフライン モードをサポートしています。</td>
<td><ul>
<li>新しい CRT と Retail サーバーの拡張機能、または新しいサービスを作成します。</li>
<li>既存の MPOS/クラウド POS の表示またはページを変更します。</li>
<li>CDX を使用して、チャネルにカスタム テーブル データを送信します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>HealthCheck</td>
<td>この例は、機能を追加して既存の CRT サービスを拡張する方法を示しています。 この場合、その他のシステムの正常性は、既に存在する RunHealthCheckServiceRequest サービスの一環として確認することができます。 CRT および CRT テスト ホストに変更があります。</td>
<td></td>
</tr>
<tr class="even">
<td>ExtensionProperties</td>
<td>この例は、CRT の次のカスタマイズの戦略を示しています。
<ul>
<li>サービス、エンティティ、要求、および応答の拡張プロパティ</li>
<li>トリガー</li>
<li>通知</li>
<li>通知ハンドラー</li>
</ul></td>
<td>拡張プロパティを使用して、カスタム フィールド値をデータベースに格納します。</td>
</tr>
<tr class="odd">
<td>CommerceRuntime テスト ホスト</td>
<td>このツールは、Retail サーバーに似た通常の CRT ホストを模倣します。 Retail サーバーまたは UI クライアントでの変更を必要としない CRT 拡張機能の簡単なテストをサポートしています。 CRT に必要なサービスを登録して、それを実行するだけです。 <strong>注記:</strong> CRT 拡張機能の一部である可能性のある RealTimeTransaction サービスコールは正しく動作しません。 これらのサービス コールをテストするには、代わりに RetailServer テスト クライアント サンプルを使用します。</td>
<td></td>
</tr>
<tr class="even">
<td>RetailServer テスト クライアント</td>
<td>この単純なアプリケーションを使用すると、Retail サーバーの呼び出し、Retail プロキシを通してのオフライン モードの呼び出し、またはその両方を行なえます。 このサンプル アプリケーションはクライアントとして機能します。 POS クライアントと似ていますが、UI の変更は必要ありません。 したがって、迅速なテストと開発をサポートします。 このツールを使用すると、UI チームに渡す前に、チャンネル データベース、RTS、CRT、および/または Retail サーバーのカスタマイズを検証できます。</td>
<td></td>
</tr>
<tr class="odd">
<td>OnlineStore</td>
<td>この例は、Eコマース SDK の使用を紹介する ASP.NET の実装です。 これには、ストア フロントと公開ジョブの両方が含まれます。</td>
<td></td>
</tr>
<tr class="even">
<td>OpenIdConnectUtility</td>
<td>この例では、Google ID を使用して顧客コンテキスト (C2) で Retail サーバー を呼び出すことができます。</td>
<td></td>
</tr>
<tr class="odd">
<td>CashDispenser (HardwareStation)</td>
<td>この例は、現金自動支払機を統合できるように Retail ハードウェア ステーションをカスタマイズする方法を示しています。</td>
<td>新しいハードウェア ステーション プロジェクトを作成し、新しい周辺機器をサポートします。</td>
</tr>
<tr class="even">
<td>Rambler (HardwareStation)</td>
<td>この例は、新築平屋携帯カード リーダーを統合できるようにハードウェア ステーションをカスタマイズする方法を示しています。</td>
<td>新しいハードウェア ステーション プロジェクトを作成し、新しい周辺機器をサポートします。</td>
</tr>
</tbody>
</table>






