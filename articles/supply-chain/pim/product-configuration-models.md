---
title: "製品コンフィギュレーション モデルの概要"
description: "この記事では、製品コンフィギュレーション モデルに関連する用語と概念を定義します。 製品コンフィギュレーション モデルを使用すると、単一の製品に多数の製品バリアントをコンフィギュレーションするのに使用できるノーブランド商品の構造を構築することができます。"
author: cvocph
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: PCProductConfigurationModelDetails, PCProductConfigurationModelListPage
audience: Application User
ms.reviewer: YuyuScheller
ms.search.scope: Core, AX 7.0.0, Operations, UnifiedOperations
ms.custom: 4031
ms.assetid: 70b968e8-e550-4731-823d-d713b8910f7b
ms.search.region: Global
ms.author: yuyus
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: c222f0d17be6eea0f776f5460c793b82d8b3e0ab
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---

# <a name="product-configuration-models-overview"></a>製品コンフィギュレーション モデルの概要

[!include[banner](../includes/banner.md)]


この記事では、製品コンフィギュレーション モデルに関連する用語と概念を定義します。 製品コンフィギュレーション モデルを使用すると、単一の製品に多数の製品バリアントをコンフィギュレーションするのに使用できるノーブランド商品の構造を構築することができます。

製品コンフィギュレーション モデルは、ノーブランド商品の構造を表すために作成されます。 製品コンフィギュレーション モデルを設定した後に、固有の部品表 (BOM) および固有の工順がある特徴的製品のバリアントをコンフィギュレーションできます。 製品コンフィギュレーション モデルは宣言制約と必須計算の両方を使用して、異なる製品バリアント間の関係と制限を処理します。 販売注文、販売見積、発注書、および製造オーダーの品目をコンフィギュレーションできます。 次の表に、テーブル制約ベースの条件および概念を示します。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>コンポーネント</td>
<td>コンポーネントは製品コンフィギュレーション モデルの主要な構成要素です。 コンポーネントは<strong>制約ベースの製品コンフィギュレーション モデルの詳細</strong>ページのツリー構造に表示されます。 コンポーネントは次の要素を含めることができます。
<ul>
<li>属性</li>
<li>制約</li>
<li>計算</li>
<li>サブコンポーネント</li>
<li>ユーザーの要件</li>
<li>BOM 明細行</li>
<li>工順工程</li>
</ul></td>
</tr>
<tr class="even">
<td>属性</td>
<td>属性は製品コンフィギュレーション モデルのすべての機能を表します。 属性は特徴的製品の構成時に選択できる機能の指定に使用できます。 属性は制約および条件に使用されます。 属性を作成して製品コンフィギュレーション モデルに追加する際には、関連する属性タイプが参照されます。 属性には既定値を設定できます。 既定値は、製品コンフィギュレーション モデルのコンフィギュレーション時に、コンフィギュレーション ユーザー インターフェイス (UI) で使用されます。 属性は、必須、読み取り専用、または非表示にするように指定できます。
<ul>
<li><strong>必須</strong> – 製品の構成時に属性に設定する必要がある値。</li>
<li><strong>読み取り専用</strong> – 属性値はコンフィギュレーション セッション中に表示されますが、変更することはできません。</li>
<li><strong>非表示</strong> – 属性値は制約と条件に含まれますが、コンフィギュレーション セッション中には表示されません。</li>
</ul>
また、属性の条件も指定できます。 条件を満たした場合は、必須属性に値を入力する必要があります。 条件は、製品コンフィギュレーション モデルに含める属性、BOM 明細行、および工順工程に対して満たす必要のある式です。 条件で参照する属性はすべて必須となります。 <strong>属性</strong>タブで必須として属性を選択することをお勧めします。これは、必須の属性を識別しやすいためです。 属性値は、コンフィギュレーションの再利用に重要な部分です。 システムは、コンフィギュレーション セッション中にユーザーが行った選択と一致するコンフィギュレーションがあるかどうかを、属性値を使用して判断します。</td>
</tr>
<tr class="odd">
<td>属性タイプ</td>
<td>属性タイプは、コンフィギュレーション製品モデルで使用されている属性のデータ型のセットを指定します。 次の属性タイプが使用されます。
<ul>
<li>範囲の有無にかかわらない<strong>整数</strong></li>
<li><strong>実数</strong></li>
<li>固定リストの有無にかかわらない<strong>テキスト</strong></li>
<li><strong>ブール値</strong></li>
</ul>
属性タイプが範囲のある<strong>ブール型</strong>、<strong>整数</strong>、または固定リストのある<strong>テキスト</strong>の場合、値のセットは製品コンフィギュレーション モデルが設定されている場合に使用できます。 [<strong>注記:</strong>] 製品コンフィギュレーション ソルバー では、[<strong>ブール型</strong>]、固定リストのある [<strong>テキスト</strong>]、および範囲のある [<strong>整数</strong>] のみを属性タイプとして認識します。 したがって、式の制約と条件ではこれらの属性タイプのみ使用できます。</td>
</tr>
<tr class="even">
<td>制約</td>
<td>制約はプロダクト モデルのコンフィギュレーションの制限を表します。 制約を使用することで、製品がコンフィギュレーションされている時に、必ず有効値のみが選択されるようになります。 制約は式の制約やテーブルの制約のいずれかです。
<ul>
<li>式の制約は関連付けられたコンポーネントにのみ使用できます。 コンポーネントの式の制約は、コンポーネントのサブコンポーネントの属性を参照できます。 製品 Solver configuration は制約の決済に使用されます。制約を書き込む際には Solver の構文を使用する必要があります。 詳細については、式の制約およびテーブルの制約に関するトピック リンクを参照してください。</li>
<li>テーブル制約は、製品コンフィギュレーション モデル内のコンポーネントに適用する前に定義する必要があります。 テーブルの制約は、ユーザーまたはシステムに定義されます。 ユーザー定義のテーブル制約は、属性タイプで定義されている属性値の組み合わせセットの説明に使用できるマトリックス タイプです。 たとえば、スピーカー生産の場合、ユーザー定義のテーブル制約のマトリックスには、スピーカーの表面処理とグリルの列を含めることができます。</li>
</ul>
<strong>例</strong> スピーカーの表面処理には黒、カシ、シタン、白色の 4 つが使用可能です。 スピーカーには、ブラック、メタル、またはホワイトの 3 つの前グリルがあります。 ブラック仕上げはすべてのグリルで利用できますが、他の仕上げは特定のグリルに限られています。 次の表には、<strong>テーブルの制約の編集</strong>ページの<strong>許可済み組み合わせ</strong>タブに表示される情報の例が表示されます。
<table>
<thead>
<tr class="header">
<th>キャビネットの仕上げ</th>
<th>前グリル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>黒</td>
<td>黒</td>
</tr>
<tr class="even">
<td>黒</td>
<td>メタル</td>
</tr>
<tr class="odd">
<td>黒</td>
<td>白</td>
</tr>
<tr class="even">
<td>カシ</td>
<td>黒</td>
</tr>
<tr class="odd">
<td>シタン</td>
<td>白</td>
</tr>
<tr class="even">
<td>白</td>
<td>黒</td>
</tr>
<tr class="odd">
<td>白</td>
<td>白</td>
</tr>
</tbody>
</table>
システム定義のテーブル制約は、属性タイプと Finance and Operations テーブルのフィールドとの間のマッピングを表します。 システム定義のテーブル制約は、属性タイプとフィールドを動的にリンクさせます。 このリンクを使用すると、製品コンフィギュレーション モデルの属性が、フィールドのデータを [Finance and Operations] テーブルに反映させることができます。</td>
</tr>
<tr class="odd">
<td>計算</td>
<td>計算は制約の補足を表します。 [<strong>小数</strong>] および [<strong>整数</strong>] 型の算術演算、または固定リストのある [<strong>テキスト</strong>] および [<strong>ブール</strong>] 型の属性に関係する論理工程を実行する計算を使用できます。 計算には計算式の結果を保持するターゲット属性があります。 式エディタを使用して計算式を構築します。</td>
</tr>
<tr class="even">
<td>サブコンポーネント</td>
<td>サブコンポーネントには、製品コンフィギュレーション モデルのツリー構造が反映されます。 サブコンポーネントは製品コンフィギュレーション モデル構造の作成に使用できます。 サブコンポーネントは既存のコンポーネントを参照します。 したがって、サブコンポーネントによって、複数の製品コンフィギュレーション モデルのコンポーネントの再利用が容易になります。 サブコンポーネントの <strong>BOM 明細行の詳細</strong>ページでは、サブコンポーネントに固有の値を選択できます。 また、製品コンフィギュレーション モデルの設定時に選択する値の属性を選択することもできます。 コンポーネントまたはサブコンポーネントとして製品を含めるには、製品の作成時に<strong>製品の作成</strong>ページの次の情報を指定する必要があります。
<ul>
<li>[<strong>製品タイプ</strong>] フィールドで、[<strong>品目</strong>] を選択します。</li>
<li>[<strong>製品サブタイプ</strong>] フィールドで、[<strong>製品マスター</strong>] を選択します。</li>
<li>[<strong>コンフィギュレーション テクノロジ</strong>] フィールドで、[<strong>制約ベースのコンフィギュレーション</strong>] を選択します。</li>
</ul>
リリースされた製品をコンポーネントまたはサブコンポーネントとして使用できるかどうかは、[<strong>リリース済製品の詳細</strong>] ページの [<strong>一般</strong>] タブで確認できます。 [<strong>コンフィギュレーション テクノロジ</strong>] フィールドで、[<strong>制約ベースのコンフィギュレーション</strong>] を選択した場合、製品はコンポーネントまたはサブコンポーネントとして使用できます。 サブコンポーネントは、コンフィギュレーション セッション中にユーザーに表示されないように、非表示にすることができます。 属性、サブコンポーネント、およびサブコンポーネントに関連付けられたユーザー要件も非表示になります。</td>
</tr>
<tr class="odd">
<td>ユーザーの要件</td>
<td>ユーザー要件は、ユーザー要件と特定のコンポーネントおよび属性との間の抽象的概念を表します。 ユーザー要件は品目にはマップできません。 たとえば、顧客がホーム シアター システムを購入しようとしているとします。 販売担当者は、システムをインストールする部屋のサイズを顧客に質問することで、必要なワットを決められます。 この例では、教室のサイズは、特定のコンポーネントの適切な属性値を決定する際のユーザーの要件となります。コンフィギュレーション セッション中にユーザーに表示されないように、ユーザーの要求を非表示にすることができます。 属性、サブコンポーネント、およびユーザー要件に関連付けられたユーザー要件も非表示になります。 ユーザー要件を非表示にするかどうかの条件は記述できます。 条件を記述するには、OML (Optimization Modeling Language) の構文を使用する必要があります。</td>
</tr>
<tr class="even">
<td>BOM 明細行</td>
<td>BOM 明細行は、製品コンフィギュレーション モデルのコンポーネントの個々の材料を表します。 <strong>BOM 明細行の詳細</strong>ページで、すべての品目を選択できます。 BOM 明細行には、特徴的製品のバリアントに対して選択した BOM 明細行が、製品コンフィギュレーション モデル設定時のユーザーの選択に基づいて変わるように条件を追加できます。 条件は、製品コンフィギュレーション モデルに含める属性、BOM 明細行、および工順工程に対して満たす必要のある式です。 <strong>BOM明細行の詳細</strong>ページで、固有の値を選択できます。 また、製品コンフィギュレーション モデルの設定時に選択する値の属性にマップさせることもできます。</td>
</tr>
<tr class="odd">
<td>工順工程</td>
<td><strong>工順工程の詳細</strong>ページで、固有の値を選択できます。 また、製品コンフィギュレーション モデルの設定時に選択する値の属性にマップさせることもできます。 条件は式の制約と同じように記述します。 条件は、製品コンフィギュレーション モデルに含める属性、BOM 明細行、および工順工程に対して満たす必要のある式です。</td>
</tr>
</tbody>
</table>





