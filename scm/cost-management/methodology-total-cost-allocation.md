---
title: "原価配賦合計の方法"
description: "この記事は、原価配賦の合計 (TCA) を使用するためのガイドラインを提供します。 TCA は、バッチ オーダーの主要式品目および式に定義される連産品の間のコストを計算する方法です。"
author: YuyuScheller
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
ms.search.form: BOMConsistOf, PmfFormulaCoBy
audience: Application User
ms.search.scope: AX 7.0.0, Operations, Core
ms.custom: 83852
ms.assetid: 7c14c3e5-9476-4a79-a210-e77fc91cc7fc
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: mguada
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: 9ccbe5815ebb54e00265e130be9c82491aebabce
ms.openlocfilehash: c26dcc5a8caa461bce90f931bb5c584f1816526b
ms.lasthandoff: 03/31/2017


---

# <a name="total-cost-allocation-method"></a>原価配賦合計の方法

この記事は、原価配賦の合計 (TCA) を使用するためのガイドラインを提供します。 TCA は、バッチ オーダーの主要式品目および式に定義される連産品の間のコストを計算する方法です。

原価配賦の合計 (TCA) は、バッチ オーダーの主要式品目および式に定義される連産品の間のコストを計算する方法です。 このメソッドは動的になります。 式品目と連産品に対して完了報告された数量間の加重平均としてコストを計算します。 TCA を使用すると、バッチ オーダーのコスト配賦を確認する必要がありません。 TCA を使用しない場合、式計算は既存の機能を使用します。

## <a name="using-tca-for-coproducts"></a>coproductsのトリクロロを使用して酸
連産品で TCA を使用するためのガイドラインをいくつか示します。

-   式バージョンの [**原価配賦の合計**] スライダーを [**はい**] に設定すると、連産品に 0 (ゼロ) より大きいコスト価格を指定する必要があります。 値は同じサイトのコスト バージョンから、またはサイト固有でない式の最初のサイトから取得できます。 この条件は、式が承認されると検証されます。
-   式バージョンの [**原価配賦の合計**] スライダーを [**はい**] に設定し、次の条件に当てはまる場合、コスト配賦方法は [**TCA**] を使用し、コスト配賦率は不変です。
    -   連産品を追加済み。
    -   連産品に異なるコスト配賦方法を使用済み。
-   式バージョンの [**原価配賦の合計**] スライダーを [**いいえ**] に設定し、次の条件に当てはまる場合、コスト配賦方法は [**手動**] に変更され、コスト配賦率は不変です。
    -   連産品を追加済み。
    -   コスト配賦率が 0 (ゼロ) を超えます。
-   正常に式計算を実行する前に、コスト配賦率を見積もる必要があります。 手動で、または [**連産品**] ページの [**見積原価**] オプションを使用してこのステップを完了できます。 **メモ:** [**見積原価**] オプションは [**原価配賦の合計**] スライダーが式バージョンで [**はい**] に設定されている場合にのみ使用できます。 完了済として報告されたバッチ オーダーの数量が式に表示される数量と一致する場合、予測配賦を表示できます。
-   バッチ オーダーが手動で作成されるか、または計画バッチ オーダーが確定されると、式バージョンの [**原価配賦の合計**] スライダーの値がバッチ オーダーにコピーされます。 ただし、バッチ オーダー上でこの設定は変更できます。 [**原価配賦の合計**] スライダーが式バージョンで [**いいえ**] に設定され、バッチ オーダーで [**はい**] に変更した場合、[**手動**] に設定されていた各行のコスト配賦方法が [**TCA**] に変更されます。 [**なし**] のコスト配賦は不変です。 [**原価配賦の合計**] スライダーが式バージョンで [**はい**] に設定され、バッチ オーダーで [**いいえ**] に変更した場合、[**製造**] タイプの各連産品のコスト配賦方法が [**手動**] に変更されます。 コスト配賦率のすべての見積が不変です。
-   [**連産品原価配賦**] ページに計算済コスト配賦率が表示されます。 [**バッチ オーダー**] ページから、このページを開くことができます。 この情報は、バッチ オーダーで予定済みまたは開始済みの数量と異なると報告された製品および数量に便利です。 コストが完了すると、TCA からの新しい配賦割合は [**連産品原価配賦**] ページに表示されます。

## <a name="calculating-the-burden-for-byproducts"></a>副産物の負担金額の計算
[**連産品**] ページの [**副産物原価配賦**] フィールドは副産物でのみ使用される列挙子のフィールドです。 連産品の場合、このフィールドの値は常に [**なし**] です。 副産物明細行の場合、このフィールドにより副産物明細行のコスト量が製品の合計コストにどのように追加されるかが決まります。 次のオプションがあります。

-   [**なし**] ─ この副産物明細行の生産の合計コストにはどの量も追加されません。
-   [**パーセンテージ**] ─ コスト量は生産で消費される原材料に対する合計コストの割合として計算されます。 計算に使用するパーセンテージは、フィールドで入力されます。
-   [**生産数**] ─ コスト量は製造オーダーの標準的なバッチ サイズあたりの量として計算されます。 この量は、生産の完了報告された数量には依存しません。 計算に使用する量はフィールドに入力されます。
-   [**数量あたり**] ─ コスト量は、生産の式品目の報告された数量あたりの量として計算されます。 計算に使用する量はフィールドに入力されます。


