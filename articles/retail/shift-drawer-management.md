---
title: "シフトとキャッシュ ドロワーの管理"
description: "この記事では、小売販売時点管理 (POS) シフトにおける 2 つのタイプの設定および使用方法について説明します - 共有およびスタンドアロン。 共有シフトは、複数の場所で複数のユーザーにより使用できますが、スタンドアロン シフトは、一度に 1 人の作業者しか使用できません。"
author: rubencdelgado
manager: AnnBe
ms.date: 02/15/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
ms.search.form: RetailHardwareProfile, RetailTerminalTable
audience: Application User
ms.reviewer: josaw
ms.search.scope: Core, Operations, Retail
ms.custom: 105011
ms.assetid: 49a0fcc9-d4db-45ad-8c4b-213ccaced82b
ms.search.region: global
ms.search.industry: Retail
ms.author: rubendel
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0, Retail July 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 8a24f8adc4f7886a1f942d83f7a4eb12e7034fcd
ms.openlocfilehash: c1483d3240d266845cea7789b70c038cb98fdfcc
ms.contentlocale: ja-jp
ms.lasthandoff: 03/22/2018

---

# <a name="shift-and-cash-drawer-management"></a>シフトとキャッシュ ドロワーの管理

[!include [banner](includes/banner.md)]

この記事では、小売販売時点管理 (POS) シフトにおける 2 つのタイプの設定および使用方法について説明します - 共有およびスタンドアロン。 共有シフトは、複数の場所で複数のユーザーにより使用できますが、スタンドアロン シフトは、一度に 1 人の作業者しか使用できません。

販売時点管理 (POS) シフトには 2 種類あります: スタンドアロンと共有です。 スタンドアロンのシフトは、1 回に 1 人の作業者しか使用できません。 共有のシフトは、複数の場所で複数のユーザーによって使用可能です。 したがって、店舗内の複数の作業者に 1 つのシフトを効果的に作成します。

## <a name="standalone-shifts"></a>スタンドアロン シフト
スタンドアロン シフトは、POS レジスターごとに現金を個別に調整する従来の固定 POS シ ナリオにおいて使用されます。 たとえば、食料品店での設定では、通常、いくつかの固定 POS レジスターがあり、レジ担当者が各レジスターに割り当てられています。 この場合では、各レジスターはスタンドアロン シフトを使用する可能性があり、レジ担当者は、そのレジスターでレジまたは現金の取扱いを担当します。 スタンドアロン シフトには、レジ担当者の勤務シフトにおけるそのレジスターのすべてのアクティビティが含まれています。 アクティビティには、レジに預金される開始金額、および銀行入金、釣銭入力、シフト終了時の支払/入金申告などの操作を含む現金削除および追加を含めることができます。

### <a name="set-up-a-stand-alone-shift"></a>スタンドアロン シフトの設定

スタンドアロン シフトは、キャッシュ ドロワーのレベルで指定されます。 この手順では、POS レジスターのスタンドアロンのシフトを設定する方法について説明します。

1.  [**小売り**] &gt; [**チャンネル設定**] &gt; [**POS 設定**] &gt; [**POS プロファイル**] &gt; [**ハードウェア プロファイル**] をクリックします。
2.  スタンドアロンのシフトを使用するハードウェア プロファイルを選択します。
3.  [**引き出し**] クイック タブで、[**共有シフトのドロワー**] オプションが [**いいえ**] に設定されていることを確認します。
4.  [**保存**] をクリックします。
5.  [**小売**] &gt; [**チャネル設定**] &gt; [**POS 設定**] &gt; [**レジスター**] をクリックします。
6.  スタンドアロンのシフトを必要とするレジスターを選択し、[**編集**] をクリックします。
7.  [**ハードウェア プロファイル**] フィールドで、手順 2 で選択したハードウェア プロファイルを選択します。
8.  [**保存**] をクリックします。
9.  [**小売**] &gt; [**小売 IT**] &gt; [**配送スケジュール**] の順にクリックします。
10. [**1090**] 配送スケジュールを選択して、[**今すぐ実行**] をクリックし、POS への変更を同期します。

### <a name="use-a-stand-alone-shift"></a>スタンドアロン シフトの使用

1.  POS へのサインイン
2.  シフトが開いていない場合は、[**新しいシフトのオープン**] を選択します。
3.  [**開始金額の申告**] 操作へ移動し、作業日を開始するのには、レジに追加されている現金の金額を指定します。
4.  一部のトランザクションを実行します。
5.  1 日の最後に、[**支払/入金の申告**] を選択し、キャッシュ ドロワー内に残っている現金の金額を申告します。
6.  現金金額を入力した後、[**保存**] をクリックし、支払/入金申告を保存します。
7.  [**シフトのクローズ**] を選択し、シフトを閉じます。

[**注記:**] 実行中のビジネス プロセスに応じて、他の操作はシフト中に利用可能です。 [**金庫保管**]、[**銀行入金**]、および [**支払/入金の削除**] 操作は、日中またはシフトを閉じる前に、レジからお金を削除するために使用することができます。 レジの現金が不足している場合、[**釣銭入力**] 操作は、レジに現金を追加するために使用することができます。

## <a name="shared-shifts"></a>共有シフト
共有シフトは、複数のレジ担当者が現金の引き出しや作業日全体での現金引き出しのセットを共有する環境で使用されます。 通常、共有シフトは、モバイル POS 環境で使用されます。 モバイル環境では、各レジ担当者が、1 つの現金引き出しに割り当てられる、または担当することはありません。 代わりに、すべてのレジ担当者は、売上への支払/入金を行い、最も近いキャッシュ ドロワーに現金を追加する必要があります。 このシナリオでは、レジ担当者間で共有されているキャッシュ ドロワーは共有シフトに含まれます。 共有シフトのすべてのキャッシュ ドロワーは、そのシフトの現金の管理に関連する活動の目的のために同じシフトに含まれます。 したがって、シフトの開始時の金額は、共有シフトに含まれているすべてのキャッシュ ドロワーの現金の合計に含める必要があります。 同様に、支払/入金申告も、共有シフトに含まれているすべてのキャッシュ ドロワーの現金の合計に含める必要があります。 **注記:** 一度に 1 つの共有シフトしか各店舗に開くことはできません。 共有シフトとスタンドアロンのシフトは同じ店舗で使用できます。

### <a name="set-up-a-shared-shift"></a>共有シフトの設定

1.  [**小売り**] &gt; [**チャンネル設定**] &gt; [**POS 設定**] &gt; [**POS プロファイル**] &gt; [**ハードウェア プロファイル**] をクリックします。
2.  共有のシフトに対して使用するハードウェア プロファイルを選択します。
3.  [**ドロワー**] クイック タブで、[**共有シフトのドロワー**] オプションを [**はい**] に設定します。
4.  [**保存**] をクリックします。
5.  [**小売**] &gt; [**チャネル設定**] &gt; [**POS 設定**] &gt; [**レジスター**] をクリックします。
6.  共有のシフトを必要とするレジスターを選択し、[**編集**] をクリックします。
7.  [**ハードウェア プロファイル**] フィールドで、手順 2 で選択したハードウェア プロファイルを選択します。
8.  [**保存**] をクリックします。
9.  [**小売**] &gt; [**小売 IT**] &gt; [**配送スケジュール**] の順にクリックします。
10. [**1090**] 配送スケジュールを選択して、[**今すぐ実行**] をクリックし、POS への変更を同期します。

### <a name="use-a-shared-shift"></a>共有シフトの使用

1.  POS へのサインイン
2.  POS がハードウェア ステーションにまだ接続されていない場合、[**非ドロワー操作**] を選択した後、[**ハードウェア ステーションの選択**] 操作を選択し、共有のシフトに対してハードウェア ステーションを有効にします。 この手順は、レジスターが共有シフト環境に初めて追加された時にのみ必要です。
3.  POS からサインアウトし、再度サインインします。
4.  [**新しいシフトの作成**] を選択します。
5.  [**開始金額の申告**] を選択します。
6.  共有シフトを使用している店舗のすべてのキャッシュ ドロワーの現金開始金を入力し、[**保存**] をクリックします。
    -   開始金額の一部を各後続のキャッシュ ドロワー追加するには、[**ハードウェア ステーションの選択**] 操作を使用し、ハードウェア ステーションを有効にします。
    -   レジを特定のキャッシュ ドロワーに追加するには、[**ドロワーを開く**] 操作を使用します。
    -   共有シフトのすべてのキャッシュ ドロワーに開始時の金額の一部が入るまで続行します。

7.  1 日の最後に、各キャッシュ ドロワーを開き、現金を削除します。
8.  最後のキャッシュ ドロワーから現金を削除した後は、すべてのキャッシュ レジスターからのすべての現金をカウントします。
9.  [**支払/入金の申告**] 操作を使用して、共有シフトに含まれるすべてのキャッシュ ドロワーの現金合計金額を申告します。
10. [**シフトのクローズ**] 操作を使用し、共有シフトを閉じます。

## <a name="shift-operations"></a>シフト操作
さまざまなアクションによってシフトの状態を変更、またはドロワーの合計金額を増減することができます。 以下のセクションでは、Retail Modern POS およびクラウド POS に対する Dynamics 365 のこれらのシフト操作について説明します。

**オープン シフト**

POSでは、販売、返品、顧客注文などの財務トランザクションにつながる操作を実行するために、ユーザーが有効で開かれたシフトを持つ必要があります。  

POS にログインすると、システムは最初に、ユーザーが現在のレジスターに使用可能な有効なシフトを持っているかをチェックします。 そうでない場合、システム コンフィギュレーションおよびそのアクセス許可に応じて、ユーザーは新しいシフトを開き、既存のシフトを再開し、または「ドロワー以外」モードでログインし続ける選択ができます。

**開始金額の申告**

多くの場合、この操作は新しく開いたシフトを取得する最初のアクションになります。 ユーザは、シフトのドロワーに現金の開始金額を指定します。 これは、シフトを終了するときに発生する超過/不足計算がこの合計量になるため重要です。

**釣銭入力**

釣銭入力は、有効なシフトで実行される販売以外のトランザクションであり、ドロワー内の現金の金額を増やします。 釣銭入力の一般的な例は、ドロワーが少ない場合にドロワーに追加の変更を加えることです。

**支払/入金の削除**

支払/入金の削除は、ドロワー内の現金金額を減らすために有効なシフトで実行される販売以外のトランザクションです。 これは、異なるシフトの釣銭入力と組み合わせて最もよく使用されます。 たとえば、レジスター 1 は変化が少ないため、レジスター 2 のユーザーがドロワー金額を削減するための支払/入金の削除を実行します。 そして、レジスター 1 のユーザは釣銭入力を行い金額を増加させます。

**シフトの中断**

ユーザーは、有効なシフトを中断して、別のユーザーの現在の登録を解放したり、別の登録にシフトを移すことができます (これは多くの場合「フローティング レジ」と呼ばれます)。 

シフトを中断すると、再開されるまで、新しいトランザクションやシフトの変更が防止されます。

**シフトの再開**

この操作により、ユーザは、有効なシフトをまだ持っていないレジスターで以前に中断したシフトを再開することができます。

**支払/入金申告**

支払/入金申告は、ユーザーが現時点でドロワー内にある現金の総額を指定するための、ほとんどの場合、シフトを終了する前に行うアクションです。 これは、超過/不足金額を計算するために予想されるシフトと比較される値です。

**金庫保管**

金庫保管は有効なシフトでいつでも実行できます。 この操作はドロワーから金銭を取り出すので、奥の部屋の金庫など、より安全な場所に移動することができます。 金庫保管に記録された合計金額は依然としてシフト合計に含まれますが、支払/入金申告の一部としてカウントする必要はありません。

**銀行入金**

金庫保管のように、銀行入金は有効なシフトでも実行されます。 この操作により、シフトからの金銭が取り出され、銀行預金の準備が整います。

**シフトのブラインド クローズ**

ブラインド クローズされたシフトは、有効ではなくなったが、完全に終了していないシフトです。 ブラインド クローズ済シフトは、中断されたシフトのように再開することはできませんが、開始金額の申告と支払/入金申告などの手順は、後で実行することも、または別のレジスターから実行することもできます。

ブラインド クローズ済シフトは、最初にこのシフトを完全にカウントし、調整し、閉じる必要がないため、新しいユーザーまたはシフトのためにレジスター解放するためによく使用されます。 

**シフトのクローズ**

この操作では、シフト合計、超過/不足金額が計算され、有効またはブラインド クローズされたシフトを完了します。 クローズされたシフトを再開または変更することはできません。  

**シフトを管理する**

この操作により、ユーザーはストアのすべての有効、中断、およびブラインド クローズされたシフトを表示できます。 アクセス許可に応じて、ユーザーは支払/入金申告などの最終決算手続きを実行し、ブラインド クローズ済シフトのシフトをクローズします。 この操作では、オフライン モードとオンライン モードの切り替え後にシフトが不適切な状態のままになっているまれなイベントの際に、無効なシフトを表示および削除することもできます。 これらの無効なシフトには、調整に必要な財務情報またはトランザクション データは含まれません。 

