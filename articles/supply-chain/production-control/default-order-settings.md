---
title: "分析コードおよび製品バリアントの既定の注文設定"
description: "既定の注文設定は、品目が供給または保管されるサイトおよび倉庫、取引または在庫管理のために使用される最小、最大、複数、標準数量、リード タイム、停止フラグ、注文納期メソッドを定義します。"
author: roxanadiaconu
manager: AnnBe
ms.date: 11/03/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: InventItemOrderSetup
audience: Application User
ms.reviewer: yuyus
ms.search.scope: Core, Operations, Retail
ms.custom: 223084
ms.assetid: fbfbcd7b-dc75-44ab-bffc-8bad576804a4
ms.search.region: global
ms.search.industry: Manufacturing
ms.author: roxanad
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Version 1611
ms.translationtype: HT
ms.sourcegitcommit: a0739304723d19b910388893d08e8c36a1f49d13
ms.openlocfilehash: d0e8d1ac8b775f9c728d6bfa6ba219dd889bf8a2
ms.contentlocale: ja-jp
ms.lasthandoff: 03/26/2018

---

# <a name="default-order-settings-for-dimensions-and-product-variants"></a>分析コードおよび製品バリアントの既定の注文設定

[!include [banner](../includes/banner.md)]

[!include [retail name](../includes/retail-name.md)]

Microsoft Dynamics 365 for Finance and Operations の既定の注文設定は、品目が供給または保管されるサイトおよび倉庫、取引または在庫管理のために使用される最小、最大、複数、標準数量、リード タイム、停止フラグ、注文納期メソッドを定義します。 既定の注文設定は、発注書、販売注文、移動オーダー、在庫仕訳帳の登録時、および計画オーダーを生成するマスタープランを作成時に使用されます。 既定の注文設定は、品目固有、サイト固有、製品バリアント固有、または製品分析コード固有です。

[既定の注文設定] ページで、既定の注文設定を定義できます。 このページを開くには、[製品情報管理] &gt; [製品] &gt; [リリース済製品] &gt; [リリース済製品の選択] &gt; [計画] または [在庫の管理] アクションペイン上 &gt; [注文設定] &gt; [既定の注文設定] に移動します。

## <a name="default-order-settings"></a>既定の注文設定
購買、販売、在庫の 3 つのタイプの既定の注文設定があります。 購買の既定の注文設定は作成時に使用されます:

-   購買注文明細行
-   購買契約明細行
-   見積依頼明細行
-   購買要求明細行
-   委託販売補充明細行
-   計画発注書

販売の既定の注文設定は作成時に使用されます:

-   販売注文行
-   販売契約明細行
-   販売見積明細行
-   返品注文明細行および品目交換明細行
-   需要予測の明細行

既定の販売注文設定も作成時に適用されます:

-   プロジェクト在庫品目要求
-   サービス注文品目の要件

在庫の既定の注文設定は作成時に使用されます:

-   在庫仕訳帳
-   移動オーダー
-   計画移動オーダー

既定の在庫注文設定も作成時に適用されます:

-   検査指示
-   品質指示
-   製造オーダー
-   BOM 明細行
-   計画製造オーダー

## <a name="full-definition-of-a-released-product"></a>リリースされた製品の完全な定義
トランザクションを作成するときは、Finance and Operations が既定の注文設定を識別しようとする前に、明細行にリリースされた製品の完全な定義を指定する必要があります。 リリースされた製品の完全な定義は、品目番号およびすべての有効な製品分析コード、コンフィギュレーション、サイズ、スタイル、色などが、トランザクションで指定されることを意味しています。 たとえば、リリースされた製品バリアントの購買注文明細行を手動で作成する場合、サイト、倉庫、数量、リード タイムが注文明細行に既定で表示される前に、必要な製品分析コードすべてを指定する必要があります。 

注文または仕訳帳明細行を作成時に、既定の注文設定パラメーターのすべてが適用されるわけではありません。 数量とリード タイムは必要に応じて既定でのみ表示されます。 たとえば、仕訳帳明細行を集計する場合、明細行の作成時にサイトと倉庫だけが既定で表示されます。 明らかに、明細行を作成したりまたは仕訳帳を転記する際に、倍数および最小での既定の数量もしくはチェックは実行されません。 

注文または仕訳帳明細行の作成時に、システムは常に既定のサイトおよび倉庫を検索しようとします。 サイトは注文設定から常に既定で表示されるわけではありません。 たとえば、販売注文または発注書が作成されると、注文ヘッダーからのサイトは自動的に注文明細行で使用されます。 BOM 明細行を作成すると、BOM ヘッダーからのサイトが使用されます。 サイトが決定されると、その後倉庫の既定として使用できるサイト固有の注文設定の検索として使用されます。 

既定の注文タイプ、購買、在庫のリード タイムは、**品目補充** ページの品目の補充ルールによって上書きできます。 既定の注文設定は、生産と転送のリード タイムの区別は許可されていませんが、品目補充ルールは許可されています。 ただし、品目補充設定は、計画生産および計画移動オーダーの作成時に MRP によってのみ使用され、生産および移動オーダーを手動で作成する場合は適用されません。 

## <a name="default-order-settings-rules"></a>既定の注文設定ルール
一般的な既定の注文設定、およびサイトまたは特定の製品分析コードまたは製品分析コードの組み合わせなどの特定の条件下でのみ適用する任意の数の既定の注文設定ルールを定義できます。 倉庫固有の注文設定を定義することはできません。

### <a name="rank-in-default-order-settings"></a>既定の注文設定のランク

既定の注文設定ルールにはランクがあります。 ランクが高いほど、ルールの重要性は高まり、高い優先順位があり、低いランクのルールの前に使用されることを意味します。 一般的な既定の注文設定には、変更できないランク ゼロがあります。 ランク ゼロのルールは 1 つだけです。 ルールは適用する分析コードが異なって指定された場合、同じランクを持つことができます。 これは、サイト固有の注文設定をモデリングするのに役立ちます。 新しい既定の注文設定が作成されると、注文値、停止フラグなどの値は、ランク ゼロのルールから継承されますが、上書きすることができます。

### <a name="default-order-settings-for-released-products"></a>リリースされた製品の既定の注文設定

特徴的なリリース製品のために、一般的な注文設定またはサイト固有の注文設定を定義できます。 一般的な注文設定は、常にランク ゼロになります。 新しい販売、購買、在庫注文の設定を同時に一緒に設定する場合は、[既定の注文設定] ページで、[詳細ビュー] を使用することをお勧めします。 詳細ビューに切り替えるには、[オプション] アクション ペイン &gt; [ページ オプション] &gt; [ビューの変更] &gt; [詳細ビュー] に移動します。

### <a name="site-specific-order-settings"></a>サイト固有の注文設定

サイト固有の注文設定を作成するには、[新規] をクリックします。 [詳細ビュー] で、[適用可能な設定] &gt; [サイト] フィールドのサイトに入力します。 [グリッド ビュー]で、[サイト] 列のサイトに入力します。 新しいルールは、自動的にゼロより高い、新しいランク値を取得します。 必要に応じてサイト固有のルールを必要なだけ作成でき、すべてのサイト固有のルールに同じランクを割り当て、それらが均等に重要であることをモデル化することができます。 

[詳細ビュー] では、品目に対して作成されたルールの概要を取得することはできません。 [リストの表示/非表示] ボタンを切り替えて、概要情報を表示します。 任意のタイプの注文明細行が作成され、サイトが提供されない場合は、Finance and Operations はサイトが指定していないルール検索します。 これは、注文明細行の既定のサイトを決定するのに役立ちます。 このサイトは、既定の倉庫が設定されているサイト固有のルールを検索するために使用されます。 この倉庫が注文明細行に適用されます。

### <a name="specific-order-settings-for-product-dimension"></a>製品分析コードの特定の注文設定

有効な製品分析コードの任意の有効な製品分析コードまたは組み合わせの注文設定のルールを定義できます。 製品分析コード フィールドが空である場合、ルールは製品分析コードのすべての値に適用されます。 

以下の製品例について考えます。

|                                                     |                                         |
|-----------------------------------------------------|-----------------------------------------|
| **製品名**                                    | 光電センサー                    |
| **品目番号**                                     | XW56                                    |
| **コンフィギュレーション** (光のタイプをモデル化するために使用される) | C1 - 可視赤色光、C2 - 赤外線 |
| **スタイル** (リバース エンジニアリングをモデル化するために使用される)  | R1、R2、R3                              |

この例では、製品が調達され、生産されないとします。 また、コンフィギュレーション C1 がより一般的に使用されるため、リード タイムもより短いとします。 

このシナリオをモデル化するには、次の既定の注文設定を作成します。

| ランク | サイト | 構成 | スタイル | 購買 - 既定の設定の上書き | 購買のリード タイム | 購買 - 停止済 | 販売 - 既定の設定の上書き | 販売 - 停止済 |
|------|------|---------------|-------|--------------------------------------|--------------------|--------------------|-----------------------------------|-----------------|
| 10   |      | C1            |       | 有                                  | 2                  |                    |                                   |                 |
| 0    |      |               |       |                                      | 5                  |                    |                                   |                 |

XW56、コンフィギュレーション C1 に対して購買注文明細行、または計画発注書が作成された場合、明細書が配置されているリビジョンまたはサイトに関係なく、リード タイムは 2 と見なされます。 R3 以外のすべてのリビジョンが停止するとします。

次の既定の注文設定ルールを作成できます。

| ランク | サイト | 構成 | スタイル | 購買 - 既定の設定の上書き | 購買のリード タイム | 購買 - 停止済 | 販売 - 既定の設定の上書き | 販売 - 停止済 |
|------|------|---------------|-------|--------------------------------------|--------------------|--------------------|-----------------------------------|-----------------|
| 20   |      |               | R2    | 有                                  |                    | 有                | 有                               | 有             |
| 20   |      |               | R1    | 有                                  |                    | 有                | 有                               | 有             |
| 10   |      | C1            |       | 有                                  | 2                  |                    |                                   |                 |
| 0    |      |               |       |                                      | 5                  |                    |                                   |                 |

古いリビジョンを停止するための 2 つのルールは同じランキングを持ち、均等に重要です。 両方ともコンフィギュレーション C1 のルールよりも高いランクを持ち、コンフィギュレーション C1 のルールより優先されます。 

この例では、ランクの必要性を説明しています。 ランクがない場合、発注書がコンフィギュレーション C1 とリビジョン R2 に作成されると、R2 と C1 について定義された 2 つのルールはあいまいです。 あいまい性を解決するために、Finance and Operations はランクの降順のルールで検索し、最初に該当するルールを適用します。 現在の例では、購買注文明細行がコンフィギュレーション C1 とリビジョン R2 に対して作成されると、品目が保留中であること、およびリビジョン値によって生じているという警告メッセージが表示されます。 コンフィギュレーション ルールがリビジョンの 1 つよりも高いランクを持つ場合、コンフィギュレーション C1 とリビジョン R2 の購買注文明細行の作成は成功し、ユーザーに「品目保留中」のメッセージは与えられません。 

次の既定の注文設定ルールについて考えます。

| ランク | サイト | 構成 | スタイル | 既定のサイト | 既定の倉庫 | 購買 - 既定の保管分析コードの上書き | 購買倉庫 |
|------|------|---------------|-------|--------------|-------------------|------------------------------------------------|--------------------|
| 20   | 2    |               |       |              |                   | 有                                            | 22                 |
| 10   |      | C1            |  R2   |  2           |  21               |                                                |                    |
| 0    |      |               |       | 1            | 11                |                                                |                    |

システムは、サイトと倉庫を決定するためにルール セットを 2 回行表示します。 購買注文明細行がコンフィギュレーション C1、スタイル R2 に対して作成されると、サイトはランク 10 でルールに基づいて決定されます。 その後、システムは倉庫を決定するためにサイト 2 のルールを検索します。 ルール 20 が見つかり、高いランクであるため、購買注文明細行の倉庫は、21 ではなく、22 になります。 

一般的なガイダンスとして、他の分析コードより重要である特定のルールおよび分析コードのルールは高いランクを取得し、より一般的なルールは低いランクを取得します。 

ランク ゼロのルールは、セーフティー ネットとして使用されます。 他のルールがヒットしない場合、ルール ゼロから既定の注文設定が使用されます。 

ランク番号はとても重要なので、[既定の注文設定] のアクション ペインで、ルールを上下に移動してルール番号を移動する、およびルールの番号を再割り当てする機能があり、それらは常に 10 の単位で表示されます。 

リリースされた製品に対して作成されたルールの番号が多数存在する場合があります。 それぞれのルールが何を上書きしているのか、なぜそれが必要なのかを理解するために、[既定の注文設定] ページの [グリッド ビュー] を使用することをお勧めします。 グリッド ビューを有効にするには、[オプション] アクション ペイン &gt; [ページ オプション] &gt; [ビューの変更] &gt; [グリッド ビュー] を選択します。 グリッドに表示される列数は、特に販売および在庫のタブで、かなり重要です。 グリッドに表示される列の数を制限するには、[既定の注文設定] &gt; [列の表示] メニューのボタンを使用して、列のグループを非表示または表示することができます。

### <a name="specific-order-settings-for-released-product-variant"></a>リリース済製品バリアントの特定の注文設定

既定の注文設定のルール システムが煩雑すぎる場合は、各製品バリアントの既定の注文設定を単に定義するオプションがあります。 次の例は、これが製品および上記のケースをどのように検索するかを示しています。

| ランク | サイト | 構成 | スタイル | 購買 - 既定の設定の上書き | 購買のリード タイム | 購買 - 停止済 | 販売 - 既定の設定の上書き | 販売 - 停止済 |
|------|------|---------------|-------|--------------------------------------|--------------------|--------------------|-----------------------------------|-----------------|
| 10   |      | C2            | R3    | 有                                  | 5                  |                    |                                   |                 |
| 10   |      | C2            | R2    | 有                                  | 5                  | 有                | 有                               | 有             |
| 10   |      | C2            | R1    | 有                                  | 5                  | 有                | 有                               | 有             |
| 10   |      | C1            | R3    | 有                                  | 2                  |                    |                                   |                 |
| 10   |      | C1            | R2    | 有                                  | 2                  | 有                | 有                               | 有             |
| 10   |      | C1            | R1    | 有                                  | 2                  | 有                | 有                               | 有             |
| 0    |      |               |       |                                      | 5                  |                    |                                   |                 |

このケースのランクは重要ではないので、非表示にすることができます。 このソリューションは、メンテナンスの問題が発生する可能性があります。 ただし、製品ライフサイクル管理 (PLM) と統合することを検討する場合、この設定を使用することを検討できます。




