---
title: "データ エンティティの動作プロパティ"
description: "このトピックでは、そのエンティティのデータ ソースであるテーブルまたはビューのプロパティ値をオーバーライドさせるビヘイビア データ エンティティのプロパティについて説明します。"
author: Sunil-Garg
manager: AnnBe
ms.date: 10/26/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: margoc
ms.search.scope: Operations
ms.custom: 25341
ms.assetid: 8e214c95-616b-4ee1-b5a4-fa5ce5147f2c
ms.search.region: Global
ms.author: sunilg
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 49a292f2b6f2997bbbc9e04c3626c891e0d791db
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="behavioral-properties-on-data-entities"></a>データ エンティティの動作プロパティ

[!INCLUDE [banner](../includes/banner.md)]

すべてのデータ エンティティには、そのエンティティのデータソースであるテーブルまたはビューの同じプロパティ値をオーバーライドできるようにするプロパティがあります。 選択内容は、エンティティの動作に影響します。 次の表では、最初の列に、このトピックで説明したプロパティが一覧表示されています。 一番上の行には、エンティティ デザイナーでプロパティが見つかったレベルが表示されます。 レベルは、精度の細かい順に一覧表示されます。データ ソース レベルはエンティティ レベルよりも細かく、フィールド レベルほどは細かくはありません。

|                   | エンティティ レベル | データ ソース レベル | フィールド レベル |
|-------------------|--------------|-------------------|-------------|
| ReadOnly          | 適用      | 適用           | .           |
| AllowEdit         | .            | .                 | 適用     |
| AllowEditOnCreate | .            | .                 | 適用     |
| 必須         | .            | .                 | 適用     |

## <a name="entity-level"></a>エンティティ レベル
データ エンティティのデザイナーで、ルート ノードの名前をクリックすると、**プロパティ** ウィンドウに**読み取り専用**プロパティがあります。 次のテーブルは、このプロパティの **Yes** と **No** 値の間の動作上の相違点を示しています。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>グループ化</th>
<th>プロパティ名</th>
<th>表示名</th>
<th>値</th>
<th>既定</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>動作</td>
<td>IsReadOnly</td>
<td>読み取り専用です。</td>
<td>いいえ、はい</td>
<td>無</td>
<td><ul>
<li><strong>いいえ:</strong> エンティティのデザイナー内の個別のデータ ソース ノードが <strong>IsReadOnly</strong> = <strong>はい</strong>に設定されて<em>いない限り</em>、データ変更操作 (CUD) <em>は</em>許可されます。</li>
<li><strong>はい:</strong> エンティティのデザイナ内の個々のデータソースノードの <strong>IsReadOnly</strong> 設定に関係なく、読み取り操作のみが許可されます。</li>
</ul></td>
</tr>
</tbody>
</table>

主にエクスポートに使用されるエンティティに対して、**IsReadOnly** を **はい** に設定します。

## <a name="data-source-level"></a>データ ソース レベル
データ エンティティに 3 つのデータ ソースがある場合は、その中から 2 つではなく、1 つのデータ ソースのデータを変更するために、エンティティを使用するためのプロセスを許可する場合があります。 読み取り専用データ ソースは、参照目的で使用できます。 エンティティ デザイナーを使用すると、この非常に制度の高い制御を達成することができます。 エンティティの **メタデータ**&gt;**データ ソース** ノードで、エンティティ ノードを選択すると、その 1 つのデータソースの**IsReadOnly** プロパティの値を設定できます。 次のテーブルでは、データ ソース レベルの **IsReadOnly** 設定とエンティティ レベルの相互作用について説明します。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>グループ化</th>
<th>プロパティ名</th>
<th>表示名</th>
<th>値</th>
<th>既定</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>動作</td>
<td>IsReadOnly</td>
<td>読み取り専用です。</td>
<td>いいえ、はい</td>
<td>無</td>
<td><ul>
<li><strong>いいえ:</strong> <strong>IsReadOnly</strong> がエンティティ レベルで<strong>はい</strong>に設定されて<em>いない限り</em>、データ変更操作 (CUD) <em>は</em>データ ソースで許可されます。</li>
<li><strong>はい:</strong> エンティティの <strong>IsReadOnly</strong> 設定に関係なく、操作のみが許可されます</li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="field-level"></a>フィールド レベル
フィールド レベルにおいて、<strong>AllowEdit</strong> と <strong>AllowEditOnCreate</strong> プロパティは <strong>IsReadOnly</strong> プロパティの代わりに利用可能です。 2 つの <strong>Allow\</strong>* プロパティには、3 番目に利用可能な値として <strong>Auto</strong> が含まれています。 <strong>自動</strong> 値は、基になっているテーブルのフィールドにある値を継承します。 <strong>注記:</strong> <strong>自動</strong>の値は、計算フィールドや仮想フィールドなどのマップされていないフィールドでは使用できません。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th>グループ化</th>
<th>プロパティ名</th>
<th>表示名</th>
<th>先頭値</th>
<th>既定</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>動作</td>
<td>AllowEditOnCreate</td>
<td>作成時の編集を許可</td>
<td>自動、いいえ、はい</td>
<td>自動</td>
<td><ul>
<li><strong>自動:</strong> 基になるテーブル フィールドから、プロパティを継承します。 <strong>注記:</strong> <strong>自動</strong>の値は、計算フィールドや仮想フィールドなどのマップされていないフィールドでは使用できません。</li>
<li><strong>いいえ:</strong> ユーザーは、このフィールドのデータを新しいレコードで変更することはできません。</li>
<li><strong>はい:</strong> ユーザーは、このフィールドのデータを新しいレコードに対して変更することができます。</li>
</ul>
この動作は、すべてのコンシューマー (X++、OData など) に適用されます。 <strong>重要:</strong> <strong>いいえ</strong>および<strong>はい</strong>の値は、基になるテーブル内のフィールドの設定を上書き<em>しません</em>。</td>
</tr>
<tr class="even">
<td>動作</td>
<td>AllowEdit</td>
<td>編集を許可</td>
<td>自動、いいえ、はい</td>
<td>自動</td>
<td>動作は、<strong>AllowEditOnCreate</strong> の動作と同じですが、作成されている新しいレコードではなく、<em>既存の</em>レコードへの更新に適用されます。 この動作は、すべてのコンシューマー (X++、OData など) に適用されます。</td>
</tr>
<tr class="odd">
<td>動作</td>
<td>必須</td>
<td>必須</td>
<td>自動、いいえ、はい</td>
<td>自動</td>
<td><strong>自動:</strong> 基になるテーブル フィールドから、プロパティを継承します。 この動作は、すべてのコンシューマー (X++、OData など) に適用されます。 <strong>重要:</strong> <strong>いいえ</strong>および<strong>はい</strong>の値は、基になるテーブル内のフィールドの設定を上書き<em>しません</em>。</td>
</tr>
</tbody>
</table>






