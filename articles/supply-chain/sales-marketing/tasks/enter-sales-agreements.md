--- 
title: "販売契約書の入力"
description: "この手順では、一定期間に特別割引で、同意した金額の製品を購入するよう顧客の 1 人にコミットする販売契約書を作成する方法を示します。"
author: omulvad
manager: AnnBe
ms.date: 11/10/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: kfend
ms.search.scope: Operations
ms.search.region: Global
ms.search.industry: Service industries
ms.author: omulvad
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: f827b4787506cfdec8b9a91c4a68f3293190158a
ms.openlocfilehash: 8c11164f7edb8e05b93f3c58b9707c0bf2482228
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="enter-sales-agreements"></a>販売契約書の入力

[!include[task guide banner](../../includes/task-guide-banner.md)]

この手順では、一定期間に特別割引で、同意した金額の製品を購入するよう顧客の 1 人にコミットする

販売契約書を作成する方法を示します。 この手順は、デモ データの会社 USMF で、または独自のデータで実行できます。


## <a name="set-up-sales-agreement-header"></a>販売契約書ヘッダーの設定
1. [販売とマーケティング] > [販売契約書] > [販売契約書] に移動します。
2. [新規] をクリックします。
3. [顧客口座] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
4. 一覧で、目的のレコードを見つけ、選択します。
5. 一覧で、選択された行のリンクをクリックします。
6. [販売契約書の分類] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
7. 一覧で、選択された行のリンクをクリックします。
8. [一般] セクションを展開します。
9. [既定の確約] フィールドで、[製品価値確約] を選択します。
    * 確約タイプは、契約が満了する方法を定義する契約に割り当てる必要がある必須の基準です。 4 つの定義済みのタイプにより、数量または値として表現される、顧客の確約のターゲットを設定できます。 数量の確約タイプは特定の製品にのみ適用されますが、値ベース タイプは特定および不特定の製品の両方の販売に適用されます。  
10. [有効期限] フィールドで、契約の期限が切れる将来の日付を設定します。
11. [OK] をクリックします。

## <a name="set-up-product-value-commitment-lines"></a>製品価値確約明細行の設定
1. [明細行の追加] をクリックします。
2. [品目番号] フィールドで、ドロップ ダウン ボタンをクリックし、ルックアップを開きます。
3. 一覧で、目的のレコードを見つけ、選択します。
4. 一覧で、選択された行のリンクをクリックします。
    * 契約のために選択した確約のタイプは、契約項目に入力できる情報の種類に影響します。 たとえば、値ベースの契約の場合は、顧客が商品を購入するためにコミットする合計正味金額 (合意された通貨で) を指定する必要があります。 この例では、顧客が製品の特定の値を購入する契約を作成しているため、明細行の [数量] および [単位] フィールドは使用できません。   
5. [正味金額] フィールドに、顧客が購入することを確定した金額を入力します。
6. [割引率] フィールドでは、この契約にリンクされている顧客の販売注文明細行に適用されるパーセンテージ値を入力します。
7. [明細行の詳細] セクションを展開します。
8. [最大値の適用] フィールドで [はい] に設定します。
    * [最大値の適用] の選択は、確約の特別価格を使用するすべての販売注文明細行の合計金額を意味し、割引や支払条件は確約で指定された金額を超えることはできません。  
    * 最小および最大のリリースの金額は、選択した契約を使用する各販売注文で販売する必要がある値の範囲を指定します。   
9. [販売契約書ヘッダー] のセクションを展開します。
    * 契約のステータスが [有効] に設定されていない限り、販売注文はその契約に関連付けることはできません。したがって販売注文は、その契約のフルフィルメントに使用されません。 ステータスをこの段階で手動で変更できます。 ただし、ステータスは通常、顧客の契約を確認するときに変更されます。  
10. [アクション ペイン] で、[販売契約書] をクリックします。
11. [確認] をクリックします。
    * [契約を有効としてマークします] オプションが [はい] に設定されていることを確認してください。  
12. [レポートの印刷] フィールドで、[はい] を選択します。
13. [OK] をクリックします。
14. ページを閉じます。
    * 契約は現在有効であり、顧客の注文を契約にリンクすることを開始して、確定済ターゲットに対して相殺できます。  

