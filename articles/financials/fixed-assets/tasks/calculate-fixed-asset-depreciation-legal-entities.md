--- 
title: "法人間での固定資産減価償却の計算"
description: "この手順では、複数の法人組織に対して減価償却プロセスを設定して実行する方法を示します。"
author: saraschi2
manager: AnnBe
ms.date: 11/02/2017
ms.topic: business-process
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Operations
ms.search.region: Global
ms.author: saraschi
ms.search.validFrom: 2016-06-30
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: d804480167414cd038f8229db312dc9c52d131f8
ms.openlocfilehash: 4c45da124136b7fecb916d2ff9098c8ffeff6cb1
ms.contentlocale: ja-jp
ms.lasthandoff: 11/02/2017

---
# <a name="calculate-fixed-asset-depreciation-across-legal-entities"></a>法人間での固定資産減価償却の計算

[!include [task guide banner](../../includes/task-guide-banner.md)]

固定資産減価償却は、単一のステップで複数の法人に対して実行することができます。 この手順では、複数の法人組織に対してプロセスを設定して実行する方法を示します。 会計士の役割を使用します。  

このレコードでは、USMF デモ会社を使用します。


ステップ (16) サブタスク: 会社間の減価償却実行ジャーナルを設定します。 

1. 最初に、各法人で実行される会社間の減価償却で使用するジャーナルを設定する必要があります。 [固定資産] > [設定] > [固定資産パラメーター] の順に移動します。 
2. 固定資産提案セクションを展開します。 
3. 法人組織の各転記階層に使用する仕訳帳名を含むレコードを登録します。 伝票が総勘定元帳に転記されない場合、未転記レイヤーは、関連する仕訳で選択される必要があります。 [追加] をクリックします。 
4. [転記階層] フィールドで値を入力または選択します。 
5. [仕訳帳名] フィールドで値を入力または選択します。 
6. 各法人の固定資産のパラメータのページで仕訳帳の設定を繰り返します。 

下位タスク: 減価償却額を計算します。

1. 法人間で減価償却を開始するには、[減価償却提案の作成] ページを使用します。 [固定資産] > [仕訳入力] > [償却提案の作成] の順に移動します。 
2. [転記階層] フィールドで値を入力または選択します。 
3. 仕訳帳名は固定資産のパラメータが既定で使用されます。 現在の法人をここで変更できます。 
4. [終了日] フィールドで、日付を入力します。 
5. 減価償却の対象として法人を選択します。 固定資産パラメータページで固定資産提案に対して設定された仕訳を持つ法人のみがリストに表示されます。 
6. 有効になっている場合、転記仕訳帳のオプションは、減価償却の仕訳帳が作成されると自動的に転記します。 選択されていない場合、仕訳帳は作成されるが転記されないため、転記の前に詳細を確認できます。 [仕訳帳の転記] フィールドで、[はい] を選択します。 
7. フィルター フィールドには、この減価償却実行に対して選択された法人のすべての固定資産、グループ、および帳簿が含まれます。 
8. バッチ処理オプションが既定で有効になっています。 このオプションを有効にすると、減価償却の仕訳帳の作成と転記がバック グラウンドで実行されます。 
9. [仕訳帳の作成] をクリックします。 
10. それぞれの法人で作成された減価償却の仕訳帳を表示する必要があります。 [固定資産] > [仕訳入力] > [固定資産仕訳帳] の順に移動します。

