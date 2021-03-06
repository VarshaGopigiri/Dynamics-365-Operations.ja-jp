--- 
title: "電子申告 (ER) 用にドメイン固有のデータ モデルを設計する"
description: "次の手順では、システム管理者または電子申告開発者の役割のユーザーが、電子支払ドキュメントのデータ モデルを含む新しい電子申告 (ER) のコンフィギュレーションを作成する方法を説明します。"
author: NickSelin
manager: AnnBe
ms.date: 12/21/2016
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: kfend
ms.search.scope: Operations
ms.search.region: Global
ms.author: nselin
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: f827b4787506cfdec8b9a91c4a68f3293190158a
ms.openlocfilehash: fadc5bc54654faf9e91e0831bdd0ff087cea3164
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---
# <a name="design-a-domain-specific-data-model-for-electronic-reporting-er"></a>電子申告 (ER) 用にドメイン固有のデータ モデルを設計する

[!include [task guide banner](../../includes/task-guide-banner.md)]

次の手順では、システム管理者または電子申告開発者の役割のユーザーが、電子支払ドキュメントのデータ モデルを含む新しい電子申告 (ER) のコンフィギュレーションを作成する方法を説明します。 このデータ モデルは、支払ドキュメントの形式を作成するときに後でデータ ソースとして使用されます。



この例では、サンプル会社 Litware, Inc. のコンフィギュレーションを作成します。ER コンフィギュレーションはすべての会社間で共有されるため、これらの手順はすべての会社で実行されます。 これらの手順を完了するには、先に「コンフィギュレーション プロバイダーの作成および有効なプロバイダーとしてのマーク付け」の手順の各ステップを完了する必要があります。

1. [組織管理] > [ワークスペース] > [電子申告] の順に移動します。
    * サンプル会社、「Litware、Inc.」のコンフィギュレーション プロバイダーを選択します。 このコンフィギュレーション プロバイダーが表示されない場合は、「コンフィギュレーション プロバイダーの作成および有効なプロバイダーとしてのマーク付け」という手順の最初のステップを完了する必要があります。  
2. [コンフィギュレーションをレポートする] をクリックします。
    * 電子支払ドキュメントのデータ モデルを含むコンフィギュレーションを作成します。 このデータ モデルは支払ドキュメントの形式を作成するするときに後でデータ ソースとして使用されます。  

## <a name="create-a-new-data-model-configuration"></a>新しいデータ モデル コンフィギュレーションの作成
1. [コンフィギュレーションの作成] をクリックすると、ドロップ ダイアログが開きます。
2. [名前] フィールドに、「支払 (単純化モデル)」と入力します。
    * 支払 (単純化モデル)  
3. [説明] フィールドに、「支払モデル コンフィギュレーション」と入力します。
    * 支払モデル構成  
    * 有効なコンフィギュレーション プロバイダーは自動的にここに入力されます。 このプロバイダーはこのコンフィギュレーションを管理できます。 他のプロバイダーはこのコンフィギュレーションを使用できますが、管理できません。  
4. コンフィギュレーション作成タスクを実行するのは、[コンフィギュレーションの作成] ボタンをクリックします。

## <a name="create-a-data-model"></a>データ モデルの作成
    * 選択したコンフィギュレーションの新しいデータ モデルを作成しています。 このコンフィギュレーション バージョンにはドラフトのステータスがあります。  
1. [デザイナー] をクリックします。

## <a name="define-the-structure-of-a-party-participating-in-a-payment-process"></a>支払プロセスに関与している当事者の構造を定義します。
1. [新規] をクリックすると、ドロップ ダイアログが開きます。
2. [名前] フィールドに、「当事者」を入力します。
    * 関係者  
3. [追加] をクリックします。
4. [新規] をクリックすると、ドロップ ダイアログが開きます。
5. [名前] フィールドに、「名前」と入力します。
    * 氏名  
6. [品目タイプ] フィールドで、「String」を選択します。
7. [追加] をクリックします。
8. [検索] フィールドに、「当事者」を入力します。
    * 関係者  
9. [前を検索] をクリックします。

## <a name="define-the-bank-structure-for-this-model"></a>このモデルの銀行構造の定義
1. [新規] をクリックすると、ドロップ ダイアログが開きます。
2. [名前] フィールドに、「代理店」と入力します。
    * 代理店  
3. [品目タイプ] フィールドで、「レコード」を選択します。
4. [追加] をクリックします。
5. [説明] フィールドで、「当事者 (債務者/債権者) の口座を提供する金融機関 (例: 銀行)」と入力します。
    * 当事者 (債務者/債権者) の口座を提供する金融機関 (例: 銀行)。  
6. [新規] をクリックすると、ドロップ ダイアログが開きます。
7. [名前] フィールドに、「名前」と入力します。
    * 氏名  
8. [品目タイプ] フィールドで、「String」を選択します。
9. [追加] をクリックします。
10. [新規] をクリックすると、ドロップ ダイアログが開きます。
11. [名前] フィールドに、「SWIFT」と入力します。
    * SWIFT  
12. [追加] をクリックします。
13. [説明] フィールドに、「銀行 ID コード」を入力します。
    * 銀行 ID コード  
14. [新規] をクリックすると、ドロップ ダイアログが開きます。
15. [名前] フィールドに、「RoutingNumber」と入力します。
    * RoutingNumber  
16. [追加] をクリックします。
17. [説明] フィールドに、「銀行支店コード」を入力します。
    * 銀行支店コード  
18. [前を検索] をクリックします。

## <a name="define-the-bank-account-structure-for-this-model"></a>このモデルの銀行口座構造の定義
1. [新規] をクリックすると、ドロップ ダイアログが開きます。
2. [名前] フィールドに、「口座」と入力します。
    * アカウント  
3. [品目タイプ] フィールドで、「レコード」を選択します。
4. [追加] をクリックします。
5. [説明] フィールドに、「当事者の金融機関 (たとえば、銀行) の口座の ID」を入力します。
    * 当事者の金融機関 (たとえば、銀行) の口座の ID。  
6. [新規] をクリックすると、ドロップ ダイアログが開きます。
7. [名前] フィールドで、「通貨」と入力します。
    * 通貨  
8. [品目タイプ] フィールドで、「String」を選択します。
9. [追加] をクリックします。
10. [説明] フィールドに、「通貨コード」を入力します。
    * 通貨コード  
11. [新規] をクリックすると、ドロップ ダイアログが開きます。
12. [名前] フィールドに、「番号」と入力します。
    * 数値  
13. [追加] をクリックします。
14. [新規] をクリックすると、ドロップ ダイアログが開きます。
15. [名前] フィールドに、「IBAN」と入力します。
    * IBAN  
16. [追加] をクリックします。
17. [説明] フィールドに、「会社の国際銀行番号」を入力します。
    * 国際銀行番号  

## <a name="define-the-payment-message-structure-for-credit-transfer-payment-type"></a>口座振替の支払タイプの支払メッセージ構造を定義します。
1. [新規] をクリックすると、ドロップ ダイアログが開きます。
2. [新しいノード] フィールドに、「モデル ルート」を入力します。
3. [名前] フィールドに「CustomerCreditTransferInitiatio」と入力します。
    * CustomerCreditTransferInitiation  
4. [追加] をクリックします。
5. [検索] フィールドに「CustomerCreditTransferInitiation」を入力します。
    * CustomerCreditTransferInitiation  
6. [前を検索] をクリックします。
7. [新規] をクリックすると、ドロップ ダイアログが開きます。
8. [名前] フィールドで、「MessageIdentification」と入力します。
    * MessageIdentification  
9. [追加] をクリックします。
10. [説明] フィールドに、「メッセージを明確に識別するために、指示者によって割り当てられる (および次の当事者に送信される) ポイント ツー ポイントの参照」を入力します。
    * メッセージを明確に識別するために、指示者によって割り当てられる (および次の当事者に送信される) ポイント ツー ポイントの参照です。  
11. [新規] をクリックすると、ドロップ ダイアログが開きます。
12. [名前] フィールドに、「ProcessingDateTime」と入力します。
    * ProcessingDateTime  
13. [品目タイプ] フィールドで、「DateTime」を選択します。
14. [追加] をクリックします。
15. [説明] フィールドに、「支払メッセージが作成された日時」を入力します。
    * 支払メッセージが作成された日時。  
16. [新規] をクリックすると、ドロップ ダイアログが開きます。
    * このモデルの支払トランザクション構造を定義します。  
17. [名前] フィールドに、「支払」と入力します。
    * 支払利息  
18. [品目タイプ] フィールドで、「レコード リスト」を選択します。
19. [追加] をクリックします。
20. [説明] フィールドに、「現在のメッセージの支払明細行」と入力とします。
    * 現在のメッセージの支払明細行  
21. [新規] をクリックすると、ドロップ ダイアログが開きます。
22. [名前] フィールドに、「債権者」と入力します。
    * 作成者  
23. [品目タイプ] フィールドで、「レコード」を選択します。
24. [追加] をクリックします。
25. [説明] フィールドに、「金銭が支払われる当事者」を入力します。
    * 金銭が支払われる当事者。  
26. [品目参照の切り替え] をクリックします。
27. [検索] フィールドに、「当事者」を入力します。
    * 関係者  
28. [次を検索] をクリックします。
29. [OK] をクリックします。
30. [検索] フィールドに、「支払」を入力します。
    * 支払利息  
31. [次を検索] をクリックします。
32. [新規] をクリックすると、ドロップ ダイアログが開きます。
33. [名前] フィールドに、「債務者」と入力します。
    * 債務者  
34. [追加] をクリックします。
35. [説明] フィールドに、「(最終的な) 債権者に金銭を支払う義務を負う当事者」を入力します。
    * (最終的な) 債権者に金銭を支払う義務を負う当事者。  
36. [品目参照の切り替え] をクリックします。
37. [検索] フィールドに、「当事者」を入力します。
    * 関係者  
38. [次を検索] をクリックします。
39. [OK] をクリックします。
40. [次を検索] をクリックします。
41. [新規] をクリックすると、ドロップ ダイアログが開きます。
42. [名前] フィールドに、「説明」と入力します。
    * 説明  
43. [品目タイプ] フィールドで、「String」を選択します。
44. [追加] をクリックします。
45. [新規] をクリックすると、ドロップ ダイアログが開きます。
46. [名前] フィールドで、「通貨」と入力します。
    * 通貨  
47. [追加] をクリックします。
48. [説明] フィールドに、「通貨コード」を入力します。
    * 通貨コード  
49. [新規] をクリックすると、ドロップ ダイアログが開きます。
50. [名前] フィールドに、「TransactionDate」と入力します。
    * TransactionDate  
51. [品目タイプ] フィールドで、「日付」を選択します。
52. [追加] をクリックします。
53. [説明] フィールドに、「トランザクション日付」を入力します。
    * 取引日付  
54. [新規] をクリックすると、ドロップ ダイアログが開きます。
55. [名前] フィールドに、「InstructedAmount」と入力します。
    * InstructedAmount
   
56. [品目タイプ] フィールドで、「実数」を選択します。
57. [追加] をクリックします。
58. [説明] フィールドに、「手数料を控除する前の、債務者と債権者の間を移動する金額」を入力します。 金額は開始側の指示通りの通貨で表示する必要があります。
    * 手数料を控除する前に債務者と債権者の間を移動する金額です。 金額は開始側の指示通りの通貨で表示する必要があります。  
59. [新規] をクリックすると、ドロップ ダイアログが開きます。
60. [名前] フィールドに、「End2EndID」と入力します。
    * End2EndID  
61. [品目タイプ] フィールドで、「String」を選択します。
62. [追加] をクリックします。
63. [説明] フィールドに、「開始側が割り当てる固有 ID」を入力します。 この ID は、エンド ツー エンド チェーン全体に渡され、不変のものです。
    * 開始側が割り当てる固有 ID です。 この ID は、エンド ツー エンド チェーン全体に渡され、不変のものです。  
64. [名前] フィールドに「PaymentModel」と入力します。
    * 「PaymentModel」の名前は支払形式の定義済インターフェイスに対応します。  
65. [保存] をクリックします。
66. ページを閉じます。


