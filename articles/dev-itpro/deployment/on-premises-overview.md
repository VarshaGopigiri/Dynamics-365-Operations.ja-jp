---
title: "Dynamics 365 for Finance and Operations オンプレミスの概要"
description: "Dynamics 365 for Finance and Operations は、オンプレミスまたはローカル ビジネス データ (LBD) の展開オプションを使用して、顧客データ センターでビジネス プロセスを実行することをサポートします。"
author: kfend
manager: AnnBe
ms.date: 06/13/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 60373
ms.assetid: 
ms.search.region: Global
ms.author: arifk
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: Platform Update 8
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 006edbe44f765ddc528c001da0b4b61092dee2cb
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---
# <a name="dynamics-365-for-finance-and-operations-enterprise-edition-on-premises-overview"></a>Dynamics 365 for Finance and Operations、(Enterprise edition オンプレミス) の概要 

[!include [banner](../includes/banner.md)]

Microsoft Dynamics 365 for Finance and Operations は、オンプレミスの配置オプションを使用して、顧客データ センターでの業務プロセスの実行をサポートします。 この配置オプションでは、アプリケーション サーバーおよび Microsoft SQL Server データベースは顧客のデータ センター内で実行されます。 顧客およびパートナーは、Microsoft Dynamics Lifecycle Services (LCS) を利用して、社内展開を管理します。 LCS は、クラウドおよびオンプレミスでの Microsoft Dynamics 365 for Finance and Operations 実装のアプリケーション ライフサイクルを管理するためのツールおよびサービスを提供するアプリケーション管理ポータルです。 業務プロセス モデリング、ソフトウェアの展開および修正、監視および診断などの LCS の機能は、オンプレミス配置をサポートするために使用されます。 
> [!IMPORTANT]
> Azure を含む、任意のパブリック クラウド インフラストラクチャでサポートされていない、Microsoft Dynamics 365 for Finance and Operations のオンプレミス配置。 

## <a name="architecture"></a>アーキテクチャ 

オンプレミス配置オプションは、Microsoft Azure Server Service Fabric スタンドアロン クラスターを使用して、オンプレミスで実行される Finance and Operations クラウド コンポーネントを使用します。 Service Fabric は、企業規模の大規模なアプリケーションを構築および管理するための次世代の Microsoft ミドルウェア プラットフォームです。 Service Fabric スタンドアロン クラスターは、Windows Server を実行しているどのコンピューターにも展開することができます。 

オンプレミスの設置では、製造環境用クラスターとサンドボックス環境用クラスターの2つのタイプの Service Fabric スタンドアロン クラスターを定義します。 両方のタイプのクラスターに、次のロールまたはノード タイプが配置されます。 

- Application Object Servers (AOS) – Finance and Operations アプリケーション機能をクライアント、バッチ、およびインポート/エクスポートのシナリオで実行する機能を提供します。 
- Management Reporter (MR) – 財務レポートの機能を提供します。 
- SQL Server Reporting Services (SSRS): ドキュメント レポート機能を提供します。 
- 環境オーケストレータ – LCS からオンプレミス環境管理を有効にします。 注記: Retail サーバーは現時点ではオンプレミス配置でサポートされていません。 

図 1 は、Service Fabric スタンドアロン クラスターで配置されるノード タイプの論理的な図を示します。 

[![Service fabric スタンドアロン クラスター](./media/on-premises-overview-01.png)](./media/on-premises-overview-01.png)

オンプレミス配置のアプリケーション ライフサイクル管理は、LCS を通じて調整されます。 顧客は、LCS の実績のあるツールと方法を使用して、社内展開を管理することができます (図2)。 開発経験は、1 ボックス VHD によるクラウド配置と同じです。 

[![ローカル ビジネス データ展開のアプリケーション ライフ サイクル管理](./media/on-premises-overview-02.png)](./media/on-premises-overview-02.png)

## <a name="data-storage"></a>データ ストレージ 
オンプレミス配置オプションは、オンプレミスのコア顧客データを格納します。 コア顧客データは、[Microsoft Trust Center](https://www.microsoft.com/en-us/trustcenter/privacy/how-microsoft-defines-customer-data) で提供される顧客データ定義のサブセットです。 表 1 では、LCS、Azure Active Directory、および Microsoft Office のサインアップ ポータルなどのサービスにより、米国内にある Microsoft Azure データ センターに格納されている顧客データのカテゴリについて説明します。 コア顧客データと呼ばれる他のすべての顧客データは、オンプレミスに保管されます。  

表 1: オンプレミス環境をサポートするサービスによって、米国内にある Microsoft Azure データ センターに格納されている顧客データ。 これらのサービスにより、サポート インシデントの初期オンボーディング、開始、追跡、サービスの更新とアップグレードが可能になります。  


| サポート サービス                   | 顧客データの定義                                                                                                                                                                                                                                                            |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Microsoft Dynamics Lifecycle Services | プロジェクトには、プロジェクトのコンテンツおよびファイルが格納されます。 これには、アプリケーション構成データ、コード、メタデータ、アプリケーションやビジネス プロセス モデルを構成するデータ アセットが含まれます。 匿名化されたユーザー活動ログおよびオンボーディング プロセス中に収集された情報に含まれます。 |
| Microsoft Office サインアップ ポータル        | オンボード プロセス中に収集された顧客情報。                                                                                                                                                                                                                                 |
| Microsoft Azure Active Directory      | LCS および Visual Studio Team Services の認証。                                                                                                                                                                                                               |
  

追加のサービスまたはコンポーネントは、必要に応じてオンプレミス配置を拡張するためにコンフィギュレーションすることができます。ただし、コンフィギュレーションの選択により、コア顧客データが顧客データ センターの外部に転送される可能性があります。 たとえば、オンプレミス配置の外部サービスを統合するために使用されるデータ管理機能のコンフィギュレーションにより、オンプレミス配置外のコア顧客データが転送される可能性があります。 

