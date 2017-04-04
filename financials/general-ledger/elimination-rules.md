---
title: "削除ルール"
description: "このトピックでは、削除の報告に削除ルール、さまざまなオプションについて説明します。"
author: RobinARH
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
ms.search.form: LedgerEliminationRule
audience: Application User
ms.reviewer: RobinARH
ms.search.scope: AX 7.0.0, Operations, Core
ms.custom: 13131
ms.assetid: 08fd46ef-2eb8-4942-985d-40fd757b74a8
ms.search.region: Global
ms.author: aolson
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: db4b05bc55d735513d7580ca5908a1e84eb760c6
ms.openlocfilehash: 152b63fdfc78b3c4e79b93340d18c5cf69257024
ms.lasthandoff: 03/31/2017


---

# <a name="elimination-rules"></a>削除ルール

このトピックでは、削除の報告に削除ルール、さまざまなオプションについて説明します。

親法人が 1 つ以上の関連法人とビジネスを行い、連結財務報告を使用するときは、削除トランザクションが必要です。 連結財務報告は、連結された組織とその組織の外部にある他のエンティティの間で発生するトランザクションのみを含む必要があります。 したがって、同じ組織の一部である法人間のトランザクションは、財務諸表に総勘定元帳から削除するため、表示、または削除する必要があります。 削除について報告する方法は複数あります。

-   連結会社または削除会社で削除ルールを作成し、処理します。
-   財務報告を使用して、特定の行または列で、削除の勘定および分析コードを示すことができます。
-   別の法人を使用して、手動トランザクション エントリを転記して削除を追跡することができます。

このトピックでは、連結または削除会社で処理する削除ルールを対象としています。 削除の相手方法人として指定されている法人内で削除トランザクションを作成するための削除ルールを設定できます。 相手方法人は削除法人と呼ばれます。 連結プロセス中に、または削除仕訳帳提案を使用することによってのいずれかで、削除仕訳帳を生成できます。 削除ルールを設定する前に、次の用語をよく理解しておく必要があります。

-   **ソース法人** – 削除される金額が転記された法人。
-   **相手方法人** – 削除ルールが転記される法人。
-   **削除の法人** – 削除の相手方の法人として指定される法人。
-   **連結法人** – 法人グループの財務結果を報告するために作成された法人。 グループ法人からの財務データはこの法人に連結され、連結されたデータを使用することによって財務レポートが作成されます。

次の表に、削除する必要がある可能性のあるトランザクション タイプを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トランザクション タイプ</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>販売注文入力および請求 (集中処理)</td>
<td>組織の別の法人に代わって顧客に製品を販売します。</td>
</tr>
<tr class="even">
<td>販売注文入力 (会社間/会社内) および請求</td>
<td>組織の法人間で製品を販売します。</td>
</tr>
<tr class="odd">
<td>発注書 (集中処理)</td>
<td>組織の別の法人に代わって仕入先から在庫品、供給品、サービス、固定資産、およびその他の製品を購入します。</td>
</tr>
<tr class="even">
<td>在庫管理 (会社間/会社内)</td>
<td><ul>
<li>組織の別の法人の固定資産に 1 つの法人の在庫を移動します。</li>
<li>組織の別の法人の在庫に 1 つの法人の在庫を移動します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>輸送中在庫追跡</td>
<td>同じ、法人の異なる地理的な場所にある倉庫間で品目を移動します。</td>
</tr>
<tr class="even">
<td>買掛金勘定集中請求処理</td>
<td>組織の別の法人に代わって請求書を記録します。</td>
</tr>
<tr class="odd">
<td>買掛金勘定集中支払処理</td>
<td>組織の別の法人に代わって請求書の支払いを行います。</td>
</tr>
<tr class="even">
<td>現金管理および資金 (集中処理)</td>
<td><ul>
<li>税金の支払、税金の払戻、利子、ローン、前払、配当金支払、および前払ロイヤリティまたはコミッションを処理します。</li>
<li>組織の別の法人に代わって経費の支払いを行います。 請求書は、相手先法人の帳簿に入力され、法人間で相互決済する必要があります。 たとえば、1 つの法人が別の法人の従業員の経費レポートの支払を行います。 この場合、従業員の経費レポートには別の法人に関連する経費があります。</li>
<li>1 つの法人から組織の別の法人に現金を移動します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>売掛金勘定 (集中処理)</td>
<td>別の法人の顧客請求書の現金を受け取り、その法人の銀行口座に小切手で預金します。</td>
</tr>
<tr class="even">
<td>給与 (集中処理、会社間/会社内)</td>
<td><ul>
<li>別の法人の給与を支払います。 たとえば、ある法人が従業員に自社の給与を支払いながら、その給与対象期間中に従業員が別の法人のために行った作業を請求する場合があります。 または、従業員は法人 A で半分働き、法人 B でも半分働いているが、福利厚生はすべての支払が対象になる場合があります。 このような場合、従業員の支払には両方の法人からの支払が含まれます。 給与が転記されるだけでなく、給与に対する税金、福利厚生、控除、および見越計上も転記されます。</li>
<li>部門間または事業部間で労働力を移動します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>固定資産 (会社間/会社内)</td>
<td>別の法人の固定資産または在庫に固定資産を転送します。</td>
</tr>
<tr class="even">
<td>配賦 (会社間/会社内)</td>
<td>会社の配賦を処理します。 配賦は、生成元のモジュールには関係のない、配賦される勘定に対する活動です。</td>
</tr>
</tbody>
</table>

## <a name="example"></a>例
自分の法人、法人 A は、組織内の別の法人、法人 B に製品を販売します。次の例では、2 つの法人の間で発生するトランザクションをどのように削除する必要があるかを示しています。

-   法人 A は、コスト 10.00 の製品を法人 B に 10.00 で販売します。
-   法人 A は、コスト 10.00 の製品を法人 B に 10.00で販売し、さらに、実際の送料 2.00 をプラスします。
-   法人 A は、コスト 10.00 の製品を法人 B に 15.00 で販売し、販売の利益幅を認識します。
-   法人 A は、コスト 10.00 の製品を法人 B に 15.00 で販売し、販売の利益幅の半分を認識します。 法人 B は、販売の利益幅の残りの半分を認識します。 したがって、収益は分割されます。 分割収益では、外部組織からの代わりに、組織の別の法人の注文にインセンティブが提供されます。

これらすべてのトランザクションで、貸し勘定および借り勘定に転記されている会社間のトランザクションが作成されます。 さらに、これらのトランザクションには、会社間の販売の量が販売された商品販売コストと等しくない場合に、値上げ金額および値下げ金額が含まれる場合があります。

## <a name="set-up-elimination-rules"></a>削除ルールの設定
Dynamics 365 for Operationsの削除ルールを設定すると、削除するための財務分析コードを作成することをお勧めします。 ほとんどの顧客名、類似する取引相手の何か。 財務分析コードを使用しないようにする会社間トランザクションの場合のみ特定の主要なアカウントを作成してください。 

削除の設定は統合のモジュールのエリアに設定できます。 ルールの説明を入力した後、削除仕訳帳が転記される会社を選択する必要があります。 これは、法人設定で**などの削除プロセスで使用**選択した会社必要があります。 

削除ルールの有効にすると、期限切れの日付を設定し、必要に応じて。 **有効** **、削除提案プロセスに使用できるされるように設定する必要があります**はい。 タイプを持つ仕訳帳名を選択します。**削除**。

基本を定義した後、[実際の処理ルールを定義できます。**行**。 差分変更金額を削除するか、または固定金額を定義する削除の二つのオプションがあります。 

ソース勘定を選択します。 ワイルド カードとしてアスタリスク (\*) を使用できます。 たとえば、1\*、\* のデータのソースとして1で始まるすべての勘定を選択します。 

ソース勘定を選択すると、**勘定の詳細**使用される相手方の会社の勘定が決まります。 **定義された**ソース**勘定で同じ主要な勘定を使用する場合に選択します**ソース。 **ユーザー定義の**選択すると、相手方の勘定を指定する必要があります。 

分析コードに指定されます。同様に処理されます。 **ソース**選択すると、ソースの会社に先の会社で同じ分析コードを使用します。 **ユーザー定義の**選択すると、**先の分析コード**メニュー項目をクリックして先の会社で分析コードを指定する必要があります。 

削除のソースとして使用されるソース分析コードと財務分析コードと値を選択します。

## <a name="process-elimination-transactions"></a>削除トランザクションの処理
オンライン連結の処理中に削除トランザクションを処理する二つの方法がありますまたは削除仕訳帳の実行を作成して削除提案が処理されます。 このセクションでは、仕訳帳の実行の作成に削除プロセス焦点を調整します。 

削除会社として定義されている会社で**統合のモジュールでは**削除仕訳帳選択します。 仕訳帳名を選択すると、をクリックして**行**。 **提案**メニューを選択し、選択によって提案を実行して**削除提案**。

連結されたデータのソースであるし、それらの処理するルールを選択します。会社を。 削除額の検索を削除額の終了する際に開始日と終了日を検索する日付を入力します。 ** GLの転記日付**フィールドは、総勘定元帳に仕訳帳の転記に使用される日付です。 **良い**クリックすると、金額を確認し、仕訳帳を転記できます。

