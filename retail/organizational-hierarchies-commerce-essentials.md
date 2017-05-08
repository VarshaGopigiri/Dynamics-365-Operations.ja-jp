---
title: "組織と組織階層 (Commerce エッセンシャル)"
description: "Commerce エッセンシャルには、組織が業務プロセスを実行したり、目標を達成するのに役立つ 3 つの内部組織があります。"
author: josaw1
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
audience: Application User
ms.search.scope: AX 7.0.0, Operations, Core, Retail
ms.custom: 21251
ms.assetid: 2bfc6bfe-784b-42e8-8bf0-116e9f0a558e
ms.search.region: global
ms.search.industry: Retail
ms.author: rubendel
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: 0c6a7bdc4ba82dd57ab3e395e6dfb0ae4de31fc4
ms.openlocfilehash: 93711977ad8d861ca75ba80ee542ee112c8ddd2f
ms.lasthandoff: 03/31/2017


---

# <a name="organizations-and-organizational-hierarchies-commerce-essentials"></a>組織と組織階層 (Commerce エッセンシャル)

[!include[banner](includes/banner.md)]


Commerce エッセンシャルには、組織が業務プロセスを実行したり、目標を達成するのに役立つ 3 つの内部組織があります。 

組織とは、業務プロセスを実行したり目標の達成を協力して行ったりする人々の集まりです。 組織階層とは、組織を構成する事業単位の関係を表すものです。

## <a name="organizations"></a>組織
Commerce エッセンシャルでは、法人、作業単位、およびチームという 3 つの内部組織のタイプを定義できます。 Microsoft Dynamics AX では、すべての内部組織は [当事者] エンティティ タイプです。 したがって、これらの組織は、住所や他の連絡先情報を保存するためにアドレス帳機能を使用します。 当時者は、個人または組織のいずれかであり、1 つ以上のアドレス帳に含めることができます。
### <a name="legal-entities"></a>法人

法人とは、登記または法的手続きを済ませた法律上の構造を持つ組織です。 法人には、法的契約の締結が認められており、業績を報告する収支報告書の作成が義務付けられています。 会社は Microsoft Dynamics AX の法人の 1 つのタイプで、すべての法人は会社 ID と関連付けられています。 この関連付けは、データのセキュリティ区分として会社を使用しているデータ モデルで会社 ID または DataAreaId を使用するために設けられています。 ユーザーは、現在ログオン中の会社のデータにのみアクセスできます。

### <a name="operating-units"></a>作業単位

作業単位とは、事業における経済資源と運営プロセスの管理を振り分ける際に使用する組織です。 作業単位のメンバは、希少なリソースの有効活用、プロセスの改善、および業績に対する責任を担っています。 Commerce エッセンシャルでは、作業単位には、コスト センター、事業単位、バリュー ストリーム、部門、小売チャンネルなどのタイプがあります。 次の表に、作業単位の各タイプに関する詳細情報を示します。
|                         |                                                                                         |                                                                                                                                             |
|-------------------------|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| **作業単位のタイプ** | **説明**                                                                         | **目的**                                                                                                                                 |
| 事業単位           | 戦略的なビジネス目標達成のために作成された半自治の事業単位。 | 法人間で組織が係わる業界または製品ラインに基づいた財務報告の事業単位を使用します。 |
| 小売チャンネル          | 従来型の店舗を表す作業単位。                             | 法人内または法人間の 1 つまたは複数の店舗を管理および制御するために使用します。                                                               |

## <a name="organizational-hierarchies"></a>組織階層
Commerce エッセンシャルでは、各階層に目的が割り当てられます。 階層の目的により、階層に含めることができる組織のタイプが決まります。 この目的により、どのアプリケーションのシナリオで階層を使用できるかが決まります。 たとえば、小売階層を使用して、小売店で製品を売買することができます。 各階層の組織では、パラメータ、ポリシー、およびトランザクションを共有できます。 親組織のパラメータは、各組織で継承または上書きできます。 ただし、製品やアドレス帳などの共有マスタ データは組織全体に適用され、個々の組織では上書きすることはできません。
### <a name="best-practices-for-setting-up-an-organization-in-a-hierarchy"></a>階層に組織を設定するためのベスト プラクティス

組織階層を実装するとき、次のベスト プラクティスを考慮してください。
-   法人と業務単位間の交差を指定する部門を作成します。 その結果、部門から法人へデータを法定レポートのために、また部門から業務単位へデータを社内レポートのためにロール アップすることができます。
-   単一の法人では、同じ階層のために複数の階層を設定しないでください。
-   目的ごとに階層を作成しないでください。 通常、複数の目的に 1 つの階層を使用できます。 たとえば、作業単位の 1 つの階層を、すべてのポリシー関連の目的に割り当てることができます。
-   均衡階層を作成します。 階層では、ルート ノードから同じ距離にあるすべてのノードは、1 つのレベルとして定義されます。 均衡階層では、1 つのタイプの作業単位のみが各レベルで存在することが可能であり、ルート ノードから各レベルへの距離は一貫しています。 部門と法人または業務単位の間に中間レベルがある場合は、プレースホルダ組織は均衡階層を作成することが求められる場合があります。
-   法人の構造が運営構造でもある場合は、別の作業単位の階層を設定しないでください。 法人と作業単位が混合した階層は両方の目的を果たす場合があります。
-   主要な建て直しシナリオを設定する前に、階層の有効日数を使用して、影響分析および検証テストを実行します。
-   発行する前に階層を変更する可能性がある場合に、階層をドラフトとして保存します。
-   実稼働環境で階層から組織を追加または削除する権限を持つ人員の数を制限します。 番号が小さくなると、費用のかかる間違いが発生し、修正が必要となる可能性が少なくなります。

## <a name="retail-store-management"></a>小売店舗の管理
次の表に、組織階層を使用できる Commerce エッセンシャルのシナリオを示します。
| タスク                                                                           | 説明                                                                                                                                                                                                                                                                                                | 階層の目的    |
|--------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| 小売品揃えの管理                                                      | 各小売店舗で利用できる製品を識別します。                                                                                                                                                                                                                                             | 小売品揃え    |
| 小売補充の管理                                                    | 補充ルールに基づいて在庫を補充する店舗をグループ化します。                                                                                                                                                                                                                                          | 小売補充 |
| 店舗のデータの報告                                                         | レポートの対象となる店舗をグループ化します。                                                                                                                                                                                                                                                                                | 小売レポート     |
| 在庫の転記、明細書の計算、または店舗グループの明細書の転記 | バッチ ジョブに割り当てることができる店舗グループを作成します。 在庫の転記、明細書の計算、または明細書の転記をするバッチ ジョブを定義するとき、どの階層にバッチ ジョブを適用するかを指定できます。 店舗を階層に追加するとき、または階層から削除するとき、バッチ ジョブを変更する必要はありません。 | Retail POS の転記   |





