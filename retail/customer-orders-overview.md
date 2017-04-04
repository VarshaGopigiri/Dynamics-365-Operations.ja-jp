---
title: "顧客注文の概要"
description: "このトピックでは、Retail POSの現代 (MPOS) の顧客注文に関する情報を提供します。 顧客注文エイリアス特別注文です。 トピックでは、関連パラメータおよびトランザクション フローの説明を示します。"
author: josaw1
manager: AnnBe
ms.date: 04/04/2017
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 
audience: Application User
ms.search.scope: AX 7.0.0, Operations, Core
ms.custom: 260594
ms.assetid: 6fc835ef-d62e-4f23-9d49-50299be642ca
ms.search.region: global
ms.search.industry: Retail
ms.author: anpurush
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
translationtype: Human Translation
ms.sourcegitcommit: 0c6a7bdc4ba82dd57ab3e395e6dfb0ae4de31fc4
ms.openlocfilehash: 2f466dfe53ccf0be15ed0793b4a6dd371bdacc0d
ms.lasthandoff: 03/31/2017


---

# <a name="customer-orders-overview"></a>顧客注文の概要

このトピックでは、Retail POSの現代 (MPOS) の顧客注文に関する情報を提供します。 顧客注文エイリアス特別注文です。 トピックでは、関連パラメータおよびトランザクション フローの説明を示します。

omniチャンネルのRetailに、ではさまざまな製品および処理の要件を満たす、複数の小売業者は、顧客注文、または特別注文のオプションが用意されています。 ある一般的なシナリオを挙げます。:

-   顧客が製品に特定の日付である住所に配送する場合。
-   顧客、顧客がその製品を購入した店舗または場所とは異なる店舗または場所から製品の出庫元とします。
-   顧客は、誰かの人に顧客が購入した製品を取得する場合。

小売業者は、商品が異なる時間や場所に渡される、または実行できるため、標準的な発生をそれぞれが別の方法でかは、注意販売を最小限にする顧客注文を使用します。

## <a name="set-up-customer-orders"></a>顧客注文設定
顧客注文がどのように処理するかを定義するパラメータ** **]ページで設定できるパラメータの一部を挙げます。:

-   **既定の預金残高の割合** –は、注文を確定する前に支払が顧客と預金がある金額を指定します。 既定の廃棄物量は割合としての値として計算されます。 [特権によって、店舗の関連を使用して金額を上書きできるかもしあります。**預金の上書き**。
-   **キャンセル料の割合**顧客注文のキャンセルと請求が適用されると–は、その雑費の金額を指定します。
-   **キャンセルされた雑費コード**顧客注文のキャンセルと請求が適用されると–は、Microsoft Dynamics AXの販売注文の雑費コードの下部に、その雑費反映されます。 キャンセルされた雑費コードを定義している場合でも、このパラメータを使用します。
-   **出荷費用コード** –の小売業者が顧客に出荷の商品の特別手数料を請求することができます。 その出荷費用の金額は、Dynamics AXの販売注文の雑費コードの下に反映されます。 顧客注文の出荷費用に出荷費用コードをマップする場合でも、このパラメータを使用します。
-   **未使用の出荷費用**顧客注文に関連付けられる出荷費用が未使用可能にするかどうかを–が指定されます。
-   **承認がない最大金額**出荷費用が未使用可能な場合–は、返品注文に出荷費用の払い戻しの最大値を指定します。 この金額を超えた場合、マネージャの上書きは、払い戻しに進むために必要です。 次のシナリオに対応するには、出荷費用の払い戻しには、まずで支払われた金額を超えるできます:
    -   雑費は、販売注文ヘッダー レベルで適用され、製品ラインの数量が返されたときに、製品、および数量に対して許可される出荷費用の最大払い戻しは、すべての[施設で勤務する方法を決定することはできません。
    -   出荷費用は、出荷のすべてのインスタンスに負われます。 小売業者は、返品の出荷費用の原価に耐えることを顧客が製品の繰り返しを返す場合、小売業者のポリシーに指定した場合、返品の出荷費用は、実際の出荷の詳細です。

## <a name="transaction-flow-for-customer-orders"></a>顧客注文のトランザクション フロー
### <a name="create-a-customer-order-in-retail-modern-pos"></a>Retail POSでの現代顧客注文を作成します。

1.  トランザクションに顧客を追加します。
2.  買い物カゴに品目を追加します。
3.  [**顧客注文を作成します。**、注文タイプを選択します。 注文タイプは、**顧客注文**または指定できます**見積依頼**。
4.  [**選択した出荷** **、またはすべてを出荷する**製品が顧客の住所の出荷するに、指定出荷日を指定し、出荷費用を指定します。
5.  [**選択または選択します** **すべてのピックアップします。**特定の日付の現在の店舗または異なる店舗から取り出す製品を選択します。
6.  預金が必要な場合は、預金物量を集めてします。

### <a name="edit-an-existing-customer-order"></a>既存の顧客注文を編集します。

1.  ホーム ページで、をクリックして**順序を指定します。**。
2.  注文の検索および編集します。 ページの下部に、をクリックして** **編集します。

### <a name="pick-up-an-order"></a>注文を取得する

1.  ホーム ページで、をクリックして**順序を指定します。**。
2.  取りあげるため注文を選択します。 ページの下部に、をクリックして**ピッキングと梱包**。
3.  **取りあげて**クリックします。

### <a name="cancel-an-order"></a>注文をキャンセルします。

1.  ホーム ページで、をクリックして**順序を指定します。**。
2.  キャンセルするに順序を選択します。 ページの下部に、をクリックして**キャンセル**。

#### <a name="create-a-return-order"></a>返品注文の作成

1.  ホーム ページで、をクリックして**順序を指定します。**。
2.  商品が返品できるように戻るに注文を選択して注文の請求書を選択し、[製品ラインを選択します。
3.  ページの下部に、をクリックして**返品注文**。

## <a name="asynchronous-transaction-flow-for-customer-orders"></a>顧客注文の非同期トランザクション フロー
顧客注文は同期モードまたは非同期モードで(POS)のPOSクライアントで作成できます。

### <a name="enable-customer-orders-to-be-created-in-asynchronous-mode"></a>非同期モードで作成された有効の顧客注文

1.  Dynamics AXの[** [小売りとコマース** &gt; **チャンネル**設定 &gt; **設定されているPOS ** &gt; ** POSのプロファイル** &gt; **機能プロファイル**。
2.  **概要** FastTabで、** asyncモードで顧客注文を作成します。**オプションを設定します。**はい**。

** asyncモードで顧客注文を作成します。**オプションに**はい**設定すると、顧客注文は非同期モードでRetail Transaction Service (RTS)が使用できる、常に作成されます。 ** **このオプションを設定して、顧客注文は同期モードでRTSを使用して常に作成されます。 顧客注文が非同期モードで作成されると、プル (P) ジョブによってDynamics AXに引っ張られ、挿入されます。 対応する販売注文は、Dynamics AXで**注文を同期します**手動でまたはバッチ処理によって実行されたときに作成されます。

<a name="see-also"></a>参照
--------

[ハイブリッド顧客注文] (ハイブリッド顧客orders.md) 

