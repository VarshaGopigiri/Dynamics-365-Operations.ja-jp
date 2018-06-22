---
title: "電子メール受領を Retail Modern POS から送信"
description: "Retail Modern 販売時点管理 (MPOS) では、販売時点管理でトランザクションが支払/入金された時点でレシートの電子メールを送信できます。"
author: jashanno
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
ms.search.form: RetailParameters, SysEmailTable,
audience: IT Pro
ms.reviewer: josaw
ms.search.scope: Core, Operations, Retail
ms.custom: 252934
ms.assetid: 4b9f733b-bf28-4b85-94de-4f7adf67a62c
ms.search.region: global
ms.search.industry: Retail
ms.author: jashanno
ms.search.validFrom: 2016-11-30
ms.dyn365.ops.version: Version 1611
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 50c635d6321254faa1d3c157699eeff6c36ee299
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="send-email-receipts-from-retail-modern-pos"></a>電子メール受領を Retail Modern POS から送信

[!include [banner](includes/banner.md)]

Retail Modern 販売時点管理 (MPOS) では、販売時点管理でトランザクションが支払/入金された時点でレシートの電子メールを送信できます。  

<a name="prerequisite"></a>前提条件
------------

電子メールのレシートを送信する SMTP サーバーを構成する必要があります。 

## <a name="set-up-email-receipts"></a>電子メールのレシートを設定
### <a name="set-default-options-for-email-receipts"></a>電子メールのレシートの既定のオプションの設定

1.  **小売 &gt; 本社の設定 &gt; パラメーター &gt; 小売パラメーター**の順にクリックします。
2.  **転記**タブをクリックし、**電子メールのレシート**下の、**レシート オプション** フィールドで既定のオプションを選択します。
    -   **標準受領書** – 販売時点管理 レジスターからレシートを印刷します。
    -   **電子メール** - レシートを電子メール メッセージで顧客に送信します。
    -   **両方** - POS レジスターからレシートを印刷して、レシートを顧客に電子メールで送信します。

3.  **件名**フィールドに、電子メールで送信するレシートの件名行に既定で表示するテキストを入力します。

### <a name="set-email-receipt-options-for-a-customer"></a>顧客の電子メールのレシート オプションを設定します。

1.  **小売 &gt; 顧客 &gt; すべての顧客**の順にクリックします。
2.  **すべての顧客**リストページで、顧客を選択し、**編集**をクリックします。
3.  **顧客の詳細**ページの、**小売**のクイック タブで、**レシート オプション**フィールドでオプションを選択します。
    -   **標準受領書** – 顧客は印刷されたレシートのみを受信します。 印刷されたレシートは POS レジスターから生成されます。
    -   **電子メール** - 顧客は電子メールのレシートのみを受信します。
    -   **両方** - 顧客は印刷されたレシートと電子メールのレシートの両方を受け取ります。

4.  **受領書の電子メール** フィールドで、**電子メール**または**両方**のいずれかを**受領書オプション** フィールドで選択した場合、顧客の電子メール アドレスを入力します。

### <a name="set-up-an-email-template-for-receipts"></a>受信者の電子メール テンプレートを設定

1. **組織管理 &gt; 設定 &gt; 電子メール テンプレート**の順にクリックします。
2. 新しいテンプレートを作成するには、**CTRL**+**N** を押します。
3. **概要**タブで、次の情報を入力します。
   - **電子メール ID** - *EmailRecpt* を入力します。
   - **電子メールの説明**- 説明を入力します。
   - **既定の言語コード**- 言語を選択します。
   - <strong>送信者名** - 電子メールの送信者として表示する名前を指定します。この名前は電子メールで**送信元</strong>の名前として顧客に表示されます。
   - <strong>送信者の電子メール** - 有効な電子メール アドレスを指定します。この電子メール アドレスは**送信元</strong>電子メール アドレスとして顧客に表示されます。

4. 下部グリッドで次を構成します。
   - <em>*電子メール ID**- これは *EmailRecpt として既に入力されている必要があります。</em>
   - **件名** - 電子メール レシートのタイトルを入力します。
   - **言語**- 言語を指定します。
   - <em>*電子メール**: 次の文字列を挿入します: *&lt;pre&gt;%message%&lt;/pre&gt;。</em>
   - メッセージにレシート以上のものを載せる場合、**電子メール メッセージ** ボタンをクリックし、送信される電子メール メッセージの本文のテンプレートを記入します。 入庫を (MPOS で) 表示するには、プレースホルダー *%message%.* を挿入します。

これは、MPOS の領収書を送信するときに置き換えられる唯一のプレースホルダーです。 より多くのプレースホルダー オプションを取得するには、MPOS 側でカスタマイズを作成する必要があります。

設定した設定に応じて、それぞれの配布スケジュールジョブを実行して、変更を MPOS に同期させる必要があります。

-   **1010** - 顧客
-   **1070** - チャンネル コンフィギュレーション
-   **1090** - レジスター
-   **1110** - グローバル コンフィギュレーション

## <a name="mpos-transaction"></a>MPOS トランザクション
店舗への変更を同期した後、MPOS は、ユーザーに各トランザクションの電子メール アドレスも求めます (有効な場合)。 顧客の電子メール アドレスがファイルに既に割り当てられている場合、そのアドレスは、電子メール アドレス プロンプトに表示されます。 顧客名が指定されていない、または名前付きの顧客が電子メール アドレスを持っていない場合、電子メール アドレスを入力し、**送信**をクリックします。 トランザクションが確定すると、リアルタイム サービスによって、上記の構成の通りに、メッセージの本文にレシートが含まれる電子メールが顧客に送信されます。



