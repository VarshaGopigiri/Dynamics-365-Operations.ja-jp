---
title: "顧客フォームの構築"
description: "このラボでは、マスター詳細フォームを作成し、適切なフォームのパターンおよびサブパターンを適用します。 マスター詳細フォームには、多数のフィールドが含まれるプライマリ データが表示されます。 たとえば、作成するフォームは、顧客情報を表示します。"
author: jasongre
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: robinr
ms.search.scope: Operations
ms.custom: 20401
ms.assetid: 78199ae8-0631-4cf4-b206-b952f09b92a9
ms.search.region: Global
ms.author: jasongre
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: d75e76c09ab179240dc980adad9239e65d80856f
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="build-the-customer-form"></a>顧客フォームの構築

[!include [banner](../includes/banner.md)]

このラボでは、マスター詳細フォームを作成し、適切なフォームのパターンおよびサブパターンを適用します。 マスター詳細フォームには、多数のフィールドが含まれるプライマリ データが表示されます。 たとえば、作成するフォームは、顧客情報を表示します。

<a name="prerequisites"></a>前提条件
-------------

このチュートリアルでは、リモート デスクトップを使用して環境にアクセスし、インスタンスの管理者としてプロビジョニングされる必要があります。 詳細については、「[アクセス インスタンス](../dev-tools/access-instances.md)」を参照してください。

## <a name="overview"></a>概要
フォームを作成するには、既存のフォーム **FmtCustomer** から開始します。 フォームは、古いマスター詳細テンプレートをテーブルします。 チュートリアルの一環として、このフォーム タイプに一貫した構造を実行するマスターの詳細パターンを適用します。 次の図は、**FmtCustomer** 開始コンポーネントを示しています。 

[![CustForm1](./media/custform1.png)](./media/custform1.png)

## <a name="key-concepts"></a>重要な概念
-   マスター詳細フォームを作成します。
-   フォームにフォーム パターンを適用します。
-   Visual Studio のパターン アドインを使用して、フォーム/モデル パターンのカバレッジに関する情報を取得します。
-   フォーム コントロールにサブパターンを適用します。
-   Visual Studio とブラウザーを使用してフォームを表示します。
-   モデル内で残っているパターンの作業の量を決定します。

## <a name="setup"></a>段取り
### <a name="import-the-tutorial-project-and-transactional-data"></a>チュートリアル プロジェクトおよびトランザクション データのインポート

Visual Studio を使用して、チュートリアル プロジェクトをインポートします。 チュートリアル プロジェクトには、このチュートリアルを完了するために使用する成果物が含まれています。 Visual Studio を使用して FMTutorial プロジェクトを開き、チュートリアル用のデータを読み込みます。 フリート管理チュートリアルのデータを読み込むために、FMTDataHelper クラスを使用します。 これが作業する最初のチュートリアルである場合は、[アクセス インスタンス](../dev-tools/access-instances.md)を確認し、ローカル VM で作業している場合に、管理者ユーザーを提供するかどうかを確認します。

1.  フリート管理のサンプルを <https://github.com/Microsoft/FMLab> からダウンロードし、**C:\\** に保存してから解凍します。
2.  デスクトップで、Visual Studio ショートカットをダブルクリックして、開発環境を開きます。
3.  **Finance and Operations** メニューで、**プロジェクトのインポート**をクリックします。
4.  **プロジェクトのインポート** ウィンドウで、**ファイル名**テキスト ボックスの隣にある、省略記号ボタンをクリックします。
5.  **インポートするファイルの選択**ウィンドウで、**C:\FMLab** を参照して FMTutorialDataModel.axpp をクリックしてから**開く**をクリックします。
6.  **プロジェクト ファイルの場所**テキスト ボックスに、**C:\FMLab** と入力します。
7.  **要素の上書き** オプションをオンにし、**現在のソリューション** ラジオ オプションをオンにします。 次の図は、完了した **インポート プロジェクト** ダイアログ ボックスを示しています。 

    ![CustForm2](./media/custform2.png)

8.  **OK** をクリックします。
9.  **ソリューション エクスプローラー**で、**クラス**を展開して、**FMTutorial** プロジェクトで **FMTDataHelper** を右クリックしてから、**スタートアップ オブジェクトとして設定**をクリックします。
10. **ビルド**メニューで、**ソリューションの再構築**をクリックします。 タイムスタンプに関係なく、プロジェクトのすべてのファイルを確実に作成するには、リビルドを使用します。 出力ウィンドウでビルドの進行状況を表示できます。
11. ビルドが完了すると、**Ctrl + F5** を押してプロジェクトを実行します。 ブラウザーが開き、データをインポートするクラスが実行されます。

## <a name="open-the-fmtutorial-project"></a>FMTutorial プロジェクトを開く
Visual Studio を使用して、FMTutorial プロジェクトを開きます。 Visual Studio を開き、FMTutorial プロジェクトが既に読み込まれている場合は、次のセクションに続行することができます。

1.  開発環境がまだ開いていない場合は、デスクトップで開発環境への Visual Studio ショートカットをダブルクリックします。
2.  **ファイル**メニューで、**開く** &gt; **プロジェクト/ソリューション**をクリックします。
3.  **プロジェクトを開く**ダイアログ ボックスで、C:\FmLab\FMTutorial を参照し、**FMTutorial** ソリューションを選択してから**開く**をクリックします。
4.  FMTutorial プロジェクトが**ソリューション エクスプローラー**に表示されます。

## <a name="use-a-template-to-create-the-form"></a>テンプレートを使用してフォームを作成
Visual Studio を使用し、**FmtCustomer** フォームを作成します。 テンプレートを使用して、新しいマスターの詳細フォームを作成します。 このチュートリアルのデータ ソースは、スターター形式によって提供されています。 ただし、グリッドと詳細ビューにフィールドを追加し、マスター詳細フォーム パターンを適用します。

1.  **ソリューション エクスプローラー**で、**FMTutorial** プロジェクトを右クリックして**追加**をポイントしてから**既存の項目**をクリックします。
2.  **既存の品目を追加**ウィンドウで、C:\FmLab を参照し、**AxForm\_FmtCustomer** を選択してから**追加**をクリックします。 ソリューション エクスプローラーの **FMTutorial** プロジェクトの下に **FmtCustomer** フォームが表示されます。
3.  ソリューション エクスプローラーで、**FmtCustomer** をダブルクリックします。 フォーム デザイナーで、フォームを開きます。
4.  フォーム デザイナーで、**デザイン**をクリックします。 **プロパティ** ウィンドウで、次の値を指定します。

    | **プロパティ** | **値**   |
    |--------------|-------------|
    | データ ソース  | FmtCustomer |
    | キャプション      | 顧客   |

5.  フォーム デザイナーで、**デザイン** &gt; **GridDetailsTab** &gt; **TabPageGrid** &gt; **MainGrid** とクリックしてから **MainGrid** をクリックします。
6.  **プロパティ** ウィンドウで、**データ ソース**をクリックしてから **FmtCustomer** を選択して **FmtCustomer** テーブルをグリッドにバインドします。 データ ソースからのフィールドを使用して、グリッドに列を追加できるようになりました。
7.  **データ ソース** &gt; **FmtCustomer** &gt; **フィールド**とクリックし、グリッドにフィールドを追加します。
    1.  **名**をクリックし、**Ctrl**キーを押しながら、表示された順序で次の追加フィールドを選択します。
        - 姓
        - CellPhone
        - DriverLicense
        - 電子メール

    2.  協調表示されたフィールドを **Design** &gt; **GridDetailsTab**&gt; **TabPageGrid** &gt; **MainGrid** にドラッグします。 次の図は、グリッド ノードを展開してフィールドを追加した後のグリッドを示しています。 

        ![CustForm3](./media/custform3.png)     

8.  **保存** をクリックします。
9.  **デザイン** &gt; **GridDetailsTab** &gt; **TabPageDetails** &gt; **TitleGroup** の順にクリックし、レコード ヘッダーを詳細ビューに追加します。
10. **HeaderTitle** をクリックします。 **プロパティ** ウィンドウで、次の値を指定します。

    | **プロパティ** | **値**   |
    |--------------|-------------|
    | データ ソース  | FmtCustomer |
    | データ メソッド  | titleFields |

11. 詳細ビューにコンテンツを追加するには、**デザイン** &gt; **GridDetailsTab** &gt; **TabPageDetails** &gt; **DetailsBodyTab** &gt; **一般**をクリックします。
    1.  **FmtCustomer** &gt; **データ ソース** &gt; **FmtCustomer** &gt; **フィールド**とクリックし、Ctrl キーを押したまま、次のフィールドを選択します。
        -   名
        -   姓
        -   CellPhone
        -   DriverLicense
        -   電子メール

    2.  協調表示されたフィールドを**一般**にドラッグし、**保存**をクリックします。

## <a name="view-the-form"></a>フォームの表示
正しく読み込まれることを確認するためにフォームを実行します。

1.  **ソリューション エクスプローラー**で、**FmtCustomer** を右クリックしてから、**スタートアップ オブジェクトとして設定**をクリックします。
2.  **Ctrl+F5** キーを押します。 グリッド ビューは、次の図のように表示する必要があります。 

    [![CustForm4](./media/custform4-1024x567.png)](./media/custform4.png)

3.  アプリケーション バーで、**Microsoft Office を開く** &gt; **Excel にエクスポート&gt;顧客**をクリックして、グリッド ビューの情報を Microsoft Excel スプレッドシートに送信します。 (ページを終了するかどうかを確認するダイアログが表示されたら、「このページを終了」をクリックします。) 求められたら、**開く**をクリックして Excel でデータを表示します。
4.  Excel を閉じます。
5.  **Tony** をクリックしてそのレコードの詳細ビューに移動します。 

    [![CustForm5](./media/custform5-1024x567.png)](./media/custform5.png)

6.  **閉じる**またはブラウザーの 戻る ボタンをクリックすると、グリッド ビューに戻ります。

## <a name="apply-a-pattern-to-the-form"></a>フォームにパターンを適用します
Visual Studio を使用して **顧客** フォームに Master Details のフォーム パターンを適用します。 フォーム パターンを適用すると、フォームに期待される構造が確実に適用されます。 また、パターンの一部であるノードでプロパティの値を自動的に設定することでデザイン体験を簡素化します。

1.  **デザイン** を右クリックして **パターンの適用** をポイントし、**詳細マスター** をクリックします。

    [![CustForm6](./media/custform6.png)](./media/custform6.png)

    [![CustForm7](./media/custform7.png)](./media/custform7.png)

2.  欠落しているナビゲーション リスト グループを追加します。 パターン情報パネルが赤色でハイライトされると、このコントロールがないことを示します。
    1.  **デザイン** を右クリックして **新規** をクリックし、**グループ** をクリックします。
    2.  **プロパティ** ウィンドウの**名前**プロパティに、**SidePanel** と入力します。
    3.  **SidePanel** をクリックし、**Alt + ↑**を押してこのグループを **GridDetailsTab (タブ)** の上の移動します。

3.  **デザイン**を再度クリックします。 **ナビゲーション リスト**と**パネル タブ**の周りの黄色のハイライトは、パターンが正常に適用される前にこれらの各ノードの下で解決する必要のある問題があることを示します。

    [![CustForm8](./media/custform8.png)](./media/custform8.png)

    [![CustForm9](./media/custform9.png)](./media/custform9.png)

4.  パターン情報パネルで **SidePanel** をクリックします。

    [![CustForm10](./media/custform10.png)](./media/custform10.png)

    [![CustForm11](./media/custform11.png)](./media/custform11.png)

5.  欠落しているコントロールを追加します。
    1.  **SidePanel** を右クリックして **新規** をクリックし、**QuickFilter** をクリックします。
    2.  **プロパティ** ウィンドウで、次の値を指定します。

        | **プロパティ** | **値**      |
        |--------------|----------------|
        | 氏名           | SidePanelQuickFilter                            |
        | ターゲット コントロール | MainGrid *この QuickFilter には、フォーム上の主要なグリッドと同じフィルター処理に使用できる列が必要です* |

    3.  **SidePanel** を右クリックして **新規** をクリックし、**グリッド** をクリックします。

        | **プロパティ** | **値**      |
        |--------------|----------------|
        | 氏名         | NavigationList |
        | データソース   | FmtCustomer    |

6.  ナビゲーション リストに識別するフィールドを追加します。 **NavigationList** を右クリックして **新規** をポイントし、**文字列** をクリックします。
    1.  **プロパティ** ウィンドウで、次の値を指定します。

        | **プロパティ** | **値**             |
        |--------------|-----------------------|
        | DataSource   | FmtCustomer           |
        | DataMethod   | fullName              |
        | 氏名         | FmtCustomer\_FullName |

    2.  電話番号を簡易リストに追加するには、**データ ソース**&gt;**FmtCustomer**&gt;**フィールド**を展開します。
    3.  **CellPhone** フィールドを **Design &gt; SidePanel &gt; NavigationList** の下のグリッドにドラッグします。

7.  **SidePanel** をクリックします。 **パターン情報パネル**は、このサブツリーのコントロールがパターンに完全に準拠していることを示しています。

    ![CustForm12](./media/custform12.png)

    ![CustForm13](./media/custform13.png)

8.  **デザイン** &gt; **GridDetailsTab** とクリックします。 サブノードの周りの黄色のハイライトは、フォーム パターンが正常に適用される前に両方のノードの下で解決する必要のある問題があることを示します。

    [![CustForm14](./media/custform14.png)](./media/custform14.png)

    [![CustForm15](./media/custform15.png)](./media/custform15.png)

9.  パターンは**グリッド パネル**が**詳細パネル**の後に配置されることを期待します。 **TabPageGrid** をクリックし、**Alt + ↓**キーを押してそのタブを**詳細パネル**の下に移動します。
10. **GridDetailsTab** をクリックします。 **TabPageDetails** タブ ページはパターンに準拠するようになりました。 ただし、**TabPageGrid** タブ ページには更なる注意が必要です。

    [![CustForm16](./media/custform16.png)](./media/custform16.png)

    [![CustForm17](./media/custform17.png)](./media/custform17.png)

11. **TabPageGrid** をクリックします。 デザイナーでフォーカスがすぐに **TabPageGrid** がオンになり、**パターン情報パネル**が更新されています。

    [![CustForm18](./media/custform18.png)](./media/custform18.png)

    [![CustForm19](./media/custform19.png)](./media/custform19.png)

12. **パターン情報パネル** には、**TabPageGrid** コンテナーの上部で欠落しているグループ コントロールが表示されるようになりました。
    1.  **TabPageGrid** を右クリックして **新規** をポイントし、**グループ** をクリックします。
    2.  **Alt+上方向**キーを 2 回押して、そのグループをグループの最初のコントロールとして配置します。
    3.  **プロパティ** ウィンドウの**名前**プロパティに、**GridCustomFilterGroup** と入力します。 [![CustForm20](./media/custform20.png)](./media/custform20.png)

13. パターンが、**GridCustomFilterGroup** に適用されるサブパターンをお探しています。 **GridCustomFilterGroup** を右クリックして **パターンの適用** をポイントし、**カスタムおよびクイック フィルター** をクリックします。

    [![CustForm21](./media/custform21.png)](./media/custform21.png)

    [![CustForm22](./media/custform22.png)](./media/custform22.png)

14. **カスタムおよびクイック フィルター** サブパターンには、QuickFilter コントロールが必須です。
    1.  **GridCustomFilterGroup** を右クリックして **新規** をクリックし、**QuickFilter** をクリックします。
    2.  **プロパティ** ウィンドウで、次の値を指定します。

        | **プロパティ**   | **値**           |
        |----------------|---------------------|
        | 氏名           | MainGridQuickFilter |
        | ターゲット コントロール | MainGrid            |

15. コントロール ツリーを参照して設計し、各コントロールで**パターン情報パネル**に問題が表示されなくなった方法に注意てください。
16. **Ctrl+S** キーを押してフォームを保存します。

## <a name="view-the-details-form"></a>詳細フォームの表示
詳細ビューとグリッド ビューに表示するフォームを実行します。

1.  **Ctrl+F5** キーを押してプロジェクトを実行します。 次の図は、グリッド ビューの表示方法を示しています。

    [![CustForm23](./media/custform23-1024x599.png)](./media/custform23.png)

2.  **Phil** をクリックしてそのレコードの詳細ビューに移動します。 

    [![CustForm24](./media/custform24-1024x599.png)](./media/custform24.png)

3.  ナビゲーション リストを開くには、フォームの左側にある**リストを表示**ボタンをクリックします。 

    [![CustForm25](./media/custform25-1024x597.png)](./media/custform25.png)

4.  グリッド表示に戻るには、**閉じる** (またはブラウザーの [戻る] ボタン) をクリックします。
5.  Visual Studio に戻ります。

## <a name="add-subpatterns"></a>サブパターンの追加
1.  Visual Studio のフォーム デザイナーで、**FmtCustomer** を右クリックし、**アドイン**をポイントしてから、**フォーム統計情報**を選択します。 

    [![CustForm26](./media/custform26.png)](./media/custform26.png) 

    **フォーム統計** アドインは、フォームの状態に関するいくつかの役に立つデータ ポイントを提供します。 これには、次のものが含まれます。
    -   **パターン = 未指定のカウント** – フォーム パターンまたはサブパターンが適用されていないノードの数。
    -   **パターン = カスタム カウント** – カスタム パターンが適用されたノードの数。構造が既存のパターンに適合しなかったことを意味します。
    -   **パターン カバレッジ** – フォーム上のコントロールのうち、フォーム パターンまたはサブパターンの対象となるものの割合。 100% の値は、完全に対象となるフォームを示します。 

        [![CustForm27](./media/custform27.png)](./media/custform27.png)

2.  このフォームのパターン カバレッジを完成させるには、Pattern = Unspecified カウントをゼロにする必要があります。 Visual Studio のフォーム検索を使用して、フォーム内の「指定されていない」すべてのインスタンスを検索します。 

    [![CustForm28](./media/custform28.png)](./media/custform28.png)

3.  **一般**タブ ページには入力コントロールのみが含まれており、このクイックタブにはカスタム レイアウトが不要なため、応答レイアウトを保証するためにフィールドおよびフィールド グループのパターンを適用する必要があります。 **全般** を右クリックして **パターンの適用** をポイントし、**フィールドおよびフィールド グループ** を選択します。
4.  画面の右端で、**検索のクリア**をクリックします。 

    [![CustForm29](./media/custform29.png)](./media/custform29.png)

5.  **Ctrl+S** キーを押してフォームを保存します。
6.  手順 1 を繰り返して **フォーム統計** アドインを再度実行し、フォームがパターンによって完全にカバーされていることを確認します。 

    [![CustForm30](./media/custform30.png)](./media/custform30.png)

7.  **Ctrl+F5** キーを押してプロジェクトを実行し、更新されたフォームを表示します。
8.  **里美 (サンプル)** をクリックし、詳細ビューに移動します。 次の図は、フィールドおよびフィールド グループのサブパターンを適用し、フィールドが反応しやすいようにレイアウトした後に詳細ビューがどのように表示されるかを示しています。 ブラウザーの幅を変更することで、ブラウザーの幅を十分に埋めるためにフィールド レイアウトがどのように調整されるのかが分かります。 

    [![CustForm31](./media/custform31-1024x674.png)](./media/custform31.png)

9.  Visual Studio に戻る

## <a name="determine-the-amount-of-remaining-patterns-work-in-a-model"></a>モデル内で残っているパターンの作業の量を決定する
1.  **Finance and Operations** をクリックし、**アドイン**をポイントし、**フォーム パターン レポートを実行**を選択します。 

    [![CustForm32](./media/custform32-1024x469.png)](./media/custform32.png) 

    フォームのパターン レポートが生成されたときに表示される通知ダイアログです。 

    [![CustForm33](./media/custform33.png)](./media/custform33.png)

2.  PatternsReport ファイルを Excel で開きます。
3.  フリート管理チュートリアル モデルへのレポートをフィルター処理します。
    1.  **データ** &gt; **フィルター**の順にクリックします。
    2.  FleetMgmntTutorial への**モデル**列をフィルター処理します。 

        [![CustForm34](./media/custform34-1024x422.png)](./media/custform34.png)


レポートには、現在適用されている最上位のフォーム パターンと、パターンでカバーされているフォーム上のコントロールの割合など、このモデルのフォームに関するパターン関連の情報が表示されます。 これは、1 つまたは複数のモデルの残りのパターンの作業を追跡するために使用できます。  



