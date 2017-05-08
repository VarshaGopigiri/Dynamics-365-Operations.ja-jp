---
title: "注文入力時に製品および製品のバリアントを検索する"
description: "手動で販売注文明細行または購買注文明細行を作成する場合、[<strong>品目番号</strong>] フィールドを使用して製品と製品バリアントを検索します。  これにより、コンフィギュレーションの文字列のみがある場合、または製品分析コードの 1 つが利用可能な場合に、製品バリアントをすばやく検索することが可能になります。"
author: YuyuScheller
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
ms.search.form: MCRFullTextIndexField, MCRFullTextParameters, PurchTable, SalesTable
audience: Application User
ms.search.scope: Operations, Core
ms.custom: 248534
ms.assetid: 99dd5ce1-0029-4f06-90e7-865e6d46d86e
ms.search.region: global
ms.search.industry: Manufacturing
ms.author: roxanad
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Version 1611
translationtype: Human Translation
ms.sourcegitcommit: 9ccbe5815ebb54e00265e130be9c82491aebabce
ms.openlocfilehash: 5b0f3c1a853f8f5e61dedaf588b6f9d2da3a53b5
ms.lasthandoff: 03/31/2017


---

# <a name="search-for-products-and-product-variants-during-order-entry"></a>注文入力時に製品および製品のバリアントを検索する

[!include[banner](../includes/banner.md)]


手動で販売注文明細行または購買注文明細行を作成する場合、[<strong>品目番号</strong>] フィールドを使用して製品と製品バリアントを検索します。  これにより、コンフィギュレーションの文字列のみがある場合、または製品分析コードの 1 つが利用可能な場合に、製品バリアントをすばやく検索することが可能になります。

するべきことがとても多い状況には入りたくない場合があります。これは類似した数多くの製品を販売する場合には特に真実です。品目番号を記憶したり、販売品目に配置するために正しい製品を見つけるために製品名を検索するために努力します。 検索フィールドとして販売注文明細行または購買注文明細行で **品目番号** フィールドを使用できます。 製品名、番号、または分析コードの一部を入力すると、検索された語に一致するすべての品目を表示するルックアップが表示されます。

## <a name="how-search-works"></a>検索の仕組み
製品または製品のバリアントを検索する場合、検索機能が入力したテキストに一致する製品を検索する方法を理解することが重要です。 検索結果を表示する主要な検索ルールを次に示します。

-   検索結果は、検索テキストが入力されたフィールドを無視して、一致するすべてのレコードを返します。
-   検索テキストは、すべてのテキストが一致するレコードに存在している必要があります。
-   検索テキストが一致するレコードのテキスト文字列の間にあったとしても検索結果に表示されます。 テキスト文字列の先頭に表示される必要はありません。
-   検索テキストは、空白が含まれている場合でも単一のテキスト文字列として処理されます。

### <a name="examples"></a>例

次の例では、製品および製品バリアントを使用して、さまざまなシナリオでどのように検索が処理されるかを示します。 **前提条件:** **販売とマーケティング &gt; 設定 &gt; 検索 &gt; 検索パラメーター** &gt; **検索タイプ**で、**完全一致** オプションを選択します。

| 製品タイプ     | 製品名    | 製品番号の表示 | 品目番号 | 構成 |
|------------------|-----------------|------------------------|-------------|---------------|
| 特徴的製品 | SpeakerMidRange | D0001                  | D0001       | NA            |
| 製品バリアント  | 有効なスピーカー  | D0010:::Black:         | D0010       | 000005        |
| 製品バリアント  | 有効なスピーカー  | D0010:::White:         | D0010       | 白         |

[**品目番号**] フィールドに「speak」と入力した場合、上記のすべての製品が結果としてルックアップに表示されます。 [**品目番号**] フィールドに「black」と入力した場合、表示された製品番号に「black」のテキストがあるため、結果として 2 番目の製品が表示されます。 これら 2 つの例は、検索がフィールドの最初のみに限定されず、一致するレコードのテキストの途中に検索文字がある場合でもヒットすることを示しています。  

「05」と入力すると 2 番目の製品バリアントが表示されます。「05」がコンフィギュレーションにあるからです。 これは [**検索条件**] ページのすべての有効なフィールドが検索されることを示しています。  

「speak 05」と入力した場合、結果は表示されません。 これは、検索が入力されたすべてのテキストを検索するからです。 検索は「speak」を見つけようとせず、「05」を含むように結果を絞り込みます。  

**販売とマーケティング &gt; 設定 &gt; 検索 &gt; 検索パラメーター** ページの **結果の件数** フィールドを使用して検索結果数を制限します。 このフィールドを 0 に設定すると、すべての検索結果が返されます。 例えば 10 に設定すると、最大 10 の検索結果を返します。

## <a name="configure-the-product-search"></a>製品検索を設定する
製品および製品バリアントの検索機能を使用する前に、製品検索を設定するには、次の手順に従います。 [![製品検索\_AXAppFall をコンフィギュレーションするための 3 つのステップ](./media/3-steps-to-configure-product-search_axappfall.png)](./media/3-steps-to-configure-product-search_axappfall.png)

### <a name="step-1-include-all-the-relevant-product-and-product-variant-identifiers-and-dimensions-in-the-search-criteria"></a>手順 1: 検索基準にすべての関連する製品、および製品バリアント識別子を含めます。

検索可能な製品、製品バリアントおよび分析コードの例としては、 **[製品名]、[品目番号]**、**[製品番号の表示]、[設定]、[色]、[サイズ]、[スタイル]、[検索名]、など** があります。  

**販売とマーケティング &gt; 設定 &gt; 検索 &gt; 検索基準** のページへ移動します。 **[検索条件]** ページでは、顧客、見込顧客、および製品検索の基準を定義することができます。 製品検索基準を使用してページをフィルターしていることを確認します。 ページ メニューの [**製品**] を切り替えることによりこれが可能です。  

検索基準に表示製品番号を追加するには、ページメニューで **新規** をクリックします。 これは **検索基準** グリッドの新しいレコードを追加します。 [**フィールド名**] 列のルックアップを開き、[**DisplayProductNumber**] を選択します。 検索基準に製品のコンフィギュレーションを追加するには、新しいレコードを **検索基準 **グリッドで作成し、**フィールド名** 列で **configId** を選択します。 同様に、カラー分析コードが [**フィールド名**] [**InventColorId**]、サイズ分析コードが [**InventSizeId**]、スタイル分析コードが [**InventStyleId**] のレコードを作成します。

### <a name="step-2-populate-the-database-table-that-is-used-for-product-search"></a>手順 2: 製品検索に使用するデータベース テーブルを設定します。

[**検索基準**] ページで、[**検索データの更新**] ボタンをクリックします。 [**検索データの更新**] ダイアログ ボックスで、[**ソース**] が [**製品**] に設定されていることを確認して、[**OK**] をクリックします。 システムは、ステップ 1 で指定されたすべての選択された検索基準を 1 つの表に集計します。 複数の製品および製品バリアントがある場合、この操作には長い時間がかかり警告メッセージが表示されることもあります。 サーバーが極端にビジー状態ではない時間に、バッチ サーバーで検索テーブル設定をスケジュールするようにお勧めします。  

テーブルが設定されるまで、製品検索は正確な結果を表示しません。 検索結果を取得できない場合、このテーブルが設定されていることを確認します。  

検索基準が変更された場合にのみ、テーブルを設定する必要があります。 新しくリリースされた製品とバリアントがテーブルに自動的に追加されます。 削除された製品とバリアントがテーブルから自動的に削除されます。

### <a name="step-3-enable-the-lookup-for-product-search-on-sales-and-purchase-order-lines"></a>手順 3: 販売と発注書明細行の製品検索のルックアップを有効にします。

この機能は **販売とマーケティング &gt; 設定 &gt; 検索 &gt; 検索パラメーター** の順に移動して、**一般** タブの **検索のルックアップを有効化** を **はい** に設定することにより有効化できます。  

販売注文明細行の入力の場合、既定の動作は [**品目番号**] フィールドで入力を開始したときに [**製品検索**] ページを開き、次に [**タブ**] キーを押します。 [**製品検索**] ページが、注文明細行の作成時にコンテキストを変更し、不要と見なす場合があります。 検索結果をルックアップで表示し、注文明細行入力時にコンテキストを非表示にしないようにする場合、代わりに検索ルックアップを使用できます。 製品または製品バリアントを検索し、ルックアップに何も選択せずに [**タブ**] キーを押した場合、[**製品検索**] ページが表示されます。



