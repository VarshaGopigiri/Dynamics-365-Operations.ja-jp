---
title: "LCS ソリューションでのデータ パッケージの処理と使用"
description: "Microsoft Dynamics 365 for Finance and Operations データ パッケージは、多数のデータ エンティティに対して 1 つで構成できます。 標準的なデータ パッケージは、特定のタスク、プロセス、または機能のエンティティのグループで構成されます。 たとえば、総勘定元帳の設定に必要なデータ エンティティは、1 つのデータ パッケージの一部である可能性があります。 データ パッケージの形式は、パッケージ マニフェスト、パッケージ ヘッダー、および含まれているデータ エンティティの追加ファイルを含む圧縮ファイルです。"
author: kfend
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Lifecycle Services
ms.custom: 197113
ms.assetid: ff06961e-2d11-4e4c-addf-5e4b9528a924
ms.search.region: Global
ms.author: omarc
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 3124f8b803d31523ea6f93160c892fac3b434ca2
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="process-and-consume-data-packages-in-an-lcs-solution"></a>LCS ソリューションでのデータ パッケージの処理と使用

[!include [banner](../includes/banner.md)]

Microsoft Dynamics 365 for Finance and Operations データ パッケージは、多数のデータ エンティティに対して 1 つで構成できます。 標準的なデータ パッケージは、特定のタスク、プロセス、または機能のエンティティのグループで構成されます。 たとえば、総勘定元帳の設定に必要なデータ エンティティは、1 つのデータ パッケージの一部である可能性があります。 データ パッケージの形式は、パッケージ マニフェスト、パッケージ ヘッダー、および含まれているデータ エンティティの追加ファイルを含む圧縮ファイルです。

データ パッケージを作成する前に、何を含める必要があるかについて計画を立てます。 この方法で、正しいエンティティ、エンティティの順序、およびフィールドが含まれていることを確認します。 データ パッケージを作成するには、Finance and Operations の **データ管理** ワークスペースを使用します。 データ パッケージを作成するには、これらの手順に従います。

1.  Finance and Operations で、**システム管理** &gt; **ワークスペース** &gt; **データ管理 IT** をクリックします。
2.  **エクスポート** タイルをクリックし、次に、**名**フィールドに**データ プロジェクト**を入力します。
3.  **ターゲット データ形式**フィールドで、エクスポートの形式を選択します。 使用可能なデータ形式には、カンマ区切り値 (CSV) 形式と Microsoft Excel 形式があります。
4.  **エンティティ名**フィールドで、エンティティを入力または選択します。 複数のエンティティを追加することができますが、各エンティティは個別に追加する必要があります。
5.  **フィールドの選択**フィールドでフィールド設定を選択してから、**エンティティの追加**をクリックしてプロジェクトにエンティティを追加します。
6.  さらにエンティティをプロジェクトに追加するには、手順 4. と 5. を繰り返します。 **注記:** 各エンティティにプロジェクトを追加すると、エンティティの名前と、**マップの表示**および**フィルター**の 2 つのボタンを含むタイルが表示されます。 データ プロジェクトをエクスポートするときに自動的にデータパッケージを作成するには、**データパッケージの生成** オプションを **はい** に設定します。 このオプションを設定しない場合は、エクスポートの時点で、データ パッケージを作成できます。
7.  アクション ウィンドウで、**エクスポート**をクリックします。
8.  **ダウンロード**をクリックします。 パッケージは、ブラウザー セッションが実行されているコンピューターの **ダウンロード** フォルダーに保存されます。 データ パッケージを扱うときは、パッケージに含まれるエンティティの前提条件の計画および検討をする必要があります。 たとえば、顧客グループは、顧客を作成するために必要です。 したがって、顧客をインポートする前に顧客グループをパッケージにインポートするか、顧客をインポートする前に完了するデータ パッケージ内の顧客グループをシーケンスする必要があります。 たとえば、次の図では、優先順位がデータ パッケージ内で設定されます。 ご覧のように、顧客グループ エンティティと顧客エンティティは顧客データ プロジェクトの一部です。 [![顧客グループおよび顧客エンティティを含む顧客データプロジェクト](./media/pdp_03.png)](./media/pdp_03.png)

9.  アクション ウィンドウで、**エンティティの順序**をクリックして、**定義グループ エンティティの順序**ページを開きます。 現在の設定に基づいて、顧客グループのエンティティと顧客エンティティは同じレベルで実行されます。 ただし、この順序は理想的ではない場合があります。 [![同じ実行レベルの顧客グループおよび顧客エンティティ](./media/pdp_04.png)](./media/pdp_04.png)

10. より良いシーケンスを作成するには、**Customers** エンティティの値を選択し、**Execution unit** フィールドの値を **1** から **2** に更新します。 この変更により、顧客エンティティの実行前に顧客グループをインポートすることが保証されます。 

[![顧客の新規シーケンスおよび顧客グループのエンティティ](./media/pdp_05.png)](./media/pdp_05.png)

Microsoft Dynamics Lifecycle Services (LCS) には、実装時間を減らすために使用できる複数の基本データ パッケージが含まれています。 これらのパッケージには、最小要件を満たすために各モジュール/領域に必要な要素が含まれています。 高度な業務プロセスには、パッケージのリストに複数のエンティティを追加する必要があります。 Microsoft が LCS で公開するデータ パッケージは、モジュール、データ型、および順序に基づいた番号順序を使用します。 次に例を示します。

-   モジュール/領域番号 

[![Module/area number](./media/pdp_06.png)](./media/pdp_06.png)

-   データ型の番号付け 

[![データ型の番号付け](./media/pdp_07.png)](./media/pdp_07.png)

-   番号付けの形式 

[![番号付けの形式](./media/pdp_08.png)](./media/pdp_08.png)

データ パッケージの名前には番号付け形式があり、そのあとにモジュールの省略形と説明が続きます。 たとえば、次の図は、総勘定元帳データ パッケージを表示します。 

[![一般会計データ パッケージ](./media/pdp_09.png)](./media/pdp_09.png)

## <a name="process-data-packages"></a>プロセス データ パッケージ
プロセス データ パッケージ (PDP) は、データのインポート/エクスポート フレームワーク (DIXF) のデータ パッケージを統合されたバンドルに統合します。 PDP を使用して、1 つのビジネス プロセス ライブラリ内のビジネス プロセスまたはビジネス プロセス グループを構成します。 DIXF データ パッケージ、これらパッケージ間の依存関係、および構成のためにパッケージを必要とする業務プロセスはともに PDPを構成します。 ここでは、LCS ソリューション パッケージの PDP の作成方法について説明します。 PDP を作成するには、以下の項目と知識が必要です。

-   作業中の LCS プロジェクトのソリューションのための実装業務プロセス ライブラリです。
-   ベスト プラクティスに従った構成を持つ DIXF データパッケージです。 これらのパッケージには、ソリューション全体のマスター データと参照データが含まれている必要があります。
-   パッケージ内のデータ間の依存関係を理解します。
-   データ パッケージ間のデータ依存関係を理解します。

PDP を作成するには、これらの手順に従います。

1.  LCS で、**アセット ライブラリ** タイルをクリックします。
2.  **データ パッケージ** を資産タイプとして選択し、プラス記号をクリックして (**+**) データ パッケージを追加します。

単一 PDP の LCS にアップロードしたデータ パッケージを連結するには、これらの手順に従います。

1.  LCS で、**アセット ライブラリ** タイルをクリックします。
2.  **プロセス データ パッケージ** を資産タイプとして選択し、プラス記号をクリックして (**+**) PDP を追加します。
3.  PDP の名前と説明を入力し、**確定**をクリックします。
4.  手順 1、「業務プロセス ライブラリの追加」では、ソリューションが構築される実装業務プロセス ライブラリを選択し、次に**続行**をクリックします。
5.  手順 2、「データ パッケージの追加」では、**編集**をクリックして、システムをコンフィグレーションする、および実行する業務プロセス ライブラリ トランザクションを有効にするために必要なデータ パッケージを追加します。 データ パッケージの追加が終了したら、**選択** をクリックします。 PDP のデータ パッケージがシステムに読み込まれる順序は重要な場合があります。 たとえば、勘定科目表 (COA) が前に読み込まれ、法人設定および通貨が必要になります。 これらのデータ エンティティは 01.1.002 System Setup にあります。 したがって、03.1.1001 COA セットアップは 01.1.002 システム設定に依存します。 次の手順では、この依存関係を記録する必要があります。
6.  手順 3、「データ パッケージの依存関係の追加」では、データ パッケージを選択し、**編集**をクリックします。 選択したデータ パッケージの前に対象となる環境に読み込む必要がある依存データ パッケージを選択し、**選択** をクリックします。
7.  手順 4、「ビジネス プロセスとデータ パッケージの関連付け」では、プロセス ノードを構成するために使用する、業務プロセスを選択します。

## <a name="consume-a-pdp"></a>PDP の消費
消費フローでは、業務プロセスを確認し、必要な構成と、業務プロセスを Finance and Operations に実装するためのデータを適用することができます。 PDP を使用するには、次のアイテムが必要です。

-   作業中の LCS プロジェクトのソリューションのための実装業務プロセス ライブラリです
-   PDP
-   既存の法人を含むターゲット環境

PDP を使用するには、次の手順に従います。

1.  LCS で、**アセット ライブラリ** タイルをクリックします。
2.  **プロセス データ** **パッケージ** を資産タイプとして選択し、**消費** をクリックします。
3.  **プロセス データ パッケージの使用** ページには、既存の PDP 資産の一覧が表示されます。 プラス記号 (**+**) をクリックすると、新しい PDP の使用が作成されます。
4.  PDPの消費名を入力し、アセット ライブラリで作成および保存した PDP を選び、ターゲット環境を選択後、**作成**をクリックします。
5.  作成した Consume PDP は、PDP 資産の一覧に表示されます。 パッケージをクリックします。 **注記:** 作成した資産は、リンクされているターゲット環境でのみ消費することができます。

### <a name="review-and-approve-bpms"></a>BPM の確認および承認

-   手順1、「業務プロセスの確認」では、業務プロセス モデル (BPM) を確認し、**確認済としてマーク**をクリックします。 すべての依存プロセスのレビュー ステータスが更新され、その右側に緑色のバーが表示されます。 **確認者** フィールドと **完了日時** フィールドは、業務プロセスごとにも更新されます。[![緑色のバーがある確認済み業務プロセスと、値の更新された [確認者] および [完了]](./media/pdplcssolutions_04.jpg)](./media/pdplcssolutions_04.jpg)

### <a name="review-and-approve-data-packages-that-are-associated-with-a-bpm"></a>BPM に関連付けられているデータ パッケージの確認および承認

1.  確認した BPM ライブラリの左ウィンドウで **2 データ パッケージの承認**をクリックします。
2.  データ パッケージに関連付ける業務プロセスを選択します。 データ パッケージは、右側のペインの **プロセスの詳細** に表示されます。 右ウィンドウ内の**確認および承認**をクリックします。
3.  **プロセス データ パッケージの使用**ページで、パッケージを選択し、**ダウンロード**をクリックして、データ パッケージをダウンロードします。 パッケージをローカルに保存します。 ターゲット環境に特有なデータで、データ パッケージ内のデータ ファイルを更新することができます。 データ ファイルの更新を完了したら、**データ パッケージのアップロード** をクリックして変更内容をアップロードします。
4.  データ パッケージが更新され、完了した後、**承認**をクリックします。 状態が **承認済** に変わります。 データ パッケージは要な数だけ承認することができます。
5.  **戻る**ボタンをクリックし、**データ パッケージの承認**をもう一度クリックします。次に業務プロセスを選択します。 **プロセスの詳細** &gt; **依存パッケージ**の下の右側ウィンドウに、**承認済** ステータスが表示されます。

### <a name="apply-a-process-data-package"></a>プロセス データ パッケージの適用

1.  BPM ライブラリの左ウィンドウで **3 プロセス データ パッケージの適用**をクリックします。
2.  業務プロセスを選択し、右ウィンドウで **データ パッケージの適用** をクリックします。
3.  **プロセス データ パッケージの使用**ページで、パッケージを選択し、**適用**をクリックします。
4.  PDP にリンクされている対象の環境で相手方の会社を選択し、**適用** をクリックします。

### <a name="view-the-data-package-history"></a>データ パッケージの履歴の表示

-   **プロセス データ パッケージの使用**ページで、パッケージを選択し、**履歴**をクリックします。 データ パッケージの状態をレビューすることができます。 利用可能な情報には、ターゲット環境、会社、パッケージ名、開始時刻と終了時刻、データ エンティティ別のステータス、およびデータ パッケージの全体的なステータスがあります。 発生したエラーの詳細を表示するには、ターゲット環境にサインインします。


<a name="additional-resources"></a>その他のリソース
--------

[AppSource 向け LCS ソリューション ホームページ](lcs-solutions-app-source.md)



