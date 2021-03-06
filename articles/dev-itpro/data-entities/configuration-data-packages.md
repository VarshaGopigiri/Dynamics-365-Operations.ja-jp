---
title: "コンフィギュレーション データ パッケージ"
description: "このトピックでは、Microsoft Dynamics 365 for Finance and Operations の 2017 年 7 月リリースの構成データ パッケージの概要を示します。"
author: saraschi2
manager: AnnBe
ms.date: 12/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: margoc
ms.search.scope: Operations
ms.custom: 
ms.search.region: Global
ms.author: saraschi
ms.search.validFrom: 2017-06-26
ms.dyn365.ops.version: Platform update 8
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 6ca555ea9eaeba36253bd032fd78a3fa5bb3c61c
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="configuration-data-packages"></a>コンフィギュレーション データ パッケージ

[!include [banner](../includes/banner.md)]

> [!IMPORTANT]
> このトピックは、Microsoft Dynamics 365 for Finance and Operations の 2017 年 7 月リリースにのみ適用されます。 今後のリリースを実行している場合、「[コンフィギュレーションのコピー](copy-configuration.md)」というトピックを参照します。 

コンフィギュレーション データ パッケージは、Microsoft Dynamics Lifecycle Services (LCS) からプロセス データ パッケージとして入手できます。 これらのデータ パッケージは、実装の再現性を向上させ、Microsoft Dynamics 365 for Finance and Operations の設定を迅速化します。

データ パッケージにはコンフィギュレーション エンティティ スプレッドシートが含まれています。 これらのエンティティ スプレッドシートには、初期のゴールデン ビルドを作成するために使用できるベスト プラクティス データが含まれています。 データ パッケージ内のデータ エンティティも適切に順序付けされ、1 回のクリックによるインポートを成功させるのに役立ちます。 

エンティティのスプレッドシートには、次の 3 種類のデータが含まれます。

- **業務データ** - スプレッドシートには、中規模の貿易会社または小売企業の標準的なビジネス データが含まれています。 このデータは、ベスト プラクティスとビジネス標準を組み合わせて、構成の始点として使用できます。
- **サンプル データ** – スプレッドシートには、ビジネス特有のデータの例として使用できるデータが含まれています。 このデータは例としてインポートして使用できますが、個々の業務内容で変更する必要があります。
- **データなし** – スプレッドシートにデータが含まれていません。 製品のいくつかの領域は、各業務とその業務内容に固有です。 これらの領域は組織専用に設定する必要があります。 これらのスプレッドシートは、必要に応じて組織のために見直し、更新する必要があります。

パッケージデータで、エンティティ スプレッドシートに含まれるデータのタイプの詳細については、このトピックの [データ パッケージ](#data-packages-system) セクションを参照してください。 データ パッケージをインポートする前に個々のスプレッドシートを修正するか、提供されるときにデータ パッケージをインポートしてからシステムでデータを更新することができます。

## <a name="using-configuration-data-packages"></a>コンフィギュレーション データ パッケージの使用
LCS から構成データ パッケージにアクセスすることができます。 それらを LCS 環境に適用するか、Finance and Operations に手動でインポートすることができるようにダウンロードすることができます。

1.  LCS プロジェクトを開いて、アセット ライブラリを開きます。
2.  アセット タイプの一覧で、**プロセス データ パッケージ**を選択します。
3.  **インポート** をクリックします。
4.  コンフィギュレーション データ パッケージを選択します。
5.  **ピック**をクリックします。

この時点で**消費**関数を使用してプロセス データ パッケージを LCS 環境に適用することができます。 

また、個々のデータ パッケージ ファイルを **データ パッケージ** 領域からダウンロードすることができます。 Finance and Operations の **データ管理** ワークスペースを使用して、LCS からデータ パッケージをインポートします。 コンフィギュレーションをインポートおよびエクスポートする方法の詳細については、[会社間でのコンフィギュレーション データのコピー](copy-configuration.md) を参照してください。

## <a name="special-considerations"></a>特別な注意事項
### <a name="system-setup"></a>システム設定
システム データ パッケージは、他のデータ パッケージの前にインポートする必要があります。 既定では、システム データ パッケージは **ST01** という名前の新しい法人を作成します。 モジュールのエリアのデータ パッケージは、この法人によって異なります。

### <a name="general-ledger"></a>一般会計
一般的な勘定科目表は、コンフィギュレーション データ パッケージに含まれます。 このデータが主勘定エンティティ スプレッドシートで定義されているように使用されると、システム全体の転記プロファイルには既定の転記データが入力されます。 勘定科目表に使用される勘定を変更する場合は、個々の転記プロファイルおよび転記領域ごとの勘定も更新する必要があります。

## <a name="data-packages-system"></a>データ パッケージ: システム

### <a name="010--system-setup"></a>010 - システム設定

|                                         | スプレッドシートの内容 |                 |             |
|-----------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**                  | **業務データ**   | **サンプル データ** | **データなし** |
| 住所と連絡先情報の目的 | x                   |                 |             |
| アドレス帳                           |                     |                 | x           |
| 住所書式行                    | x                   |                 |             |
| 住所の形式                          | x                   |                 |             |
| 住所パラメーター                      | x                   |                 |             |
| カレンダー                                |                     |                 | x           |
| 市町村                                  | x                   |                 |             |
| 市区郡                                | x                   |                 |             |
| CountryRegions                          | x                   |                 |             |
| 通貨                              | x                   |                 |             |
| 地域                               | x                   |                 |             |
| 為替レート                          |                     | x               |             |
| グローバル アドレス帳パラメーター          | x                   |                 |             |
| グローバル アドレス帳                     |                     |                 | x           |
| 法人                          |                     | x               |             |
| 名前の接辞                            | x                   |                 |             |
| 名前の順序                          | x                   |                 |             |
| 作業単位                          |                     | x               |             |
| 組織階層の目的         |                     |                 | x           |
| 組織階層タイプ             |                     |                 | x           |
| 組織階層                  |                     |                 | x           |
| 関係者の連絡先                          |                     |                 | x           |
| 関係者の配送先                  |                     |                 | x           |
| 関係者のリレーションシップ                     |                     |                 | x           |
| 郵便番号                            | x                   |                 |             |
| 関係タイプ                      | x                   |                 |             |
| 都道府県                                  | x                   |                 |             |
| システム パラメーター                       | x                   |                 |             |
| チーム タイプ                              |                     |                 | x           |
| チーム                                   |                     |                 | x           |
| 単位換算                        | x                   |                 |             |
| 単位の変換                       | x                   |                 |             |
| 単位                                   | x                   |                 |             |
| ユーザー グループ                             |                     |                 | x           |
| ユーザー情報                        |                     |                 | x           |

## <a name="data-packages-financials"></a>データ パッケージ: 財務 

### <a name="020--gl-shared"></a>020 - GL 共有

|                                        | スプレッドシートの内容 |                 |             |
|----------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**                 | **業務データ**   | **サンプル データ** | **データなし** |
| 勘定構造の有効化           |                     | x               |             |
| 勘定構造の許可値       |                     | x               |             |
| 勘定構造                     |                     | x               |             |
| 詳細ルールの基準                 |                     | x               |             |
| 詳細ルール構造の有効化     |                     | x               |             |
| 詳細ルール構造の許可値 |                     | x               |             |
| 詳細なルール構造               |                     | x               |             |
| 詳細ルール                         |                     | x               |             |
| 勘定科目表                      | x                   |                 |             |
| 連結グループおよび勘定      |                     | x               |             |
| 分析コード属性の有効化         |                     | x               |             |
| 財務分析コード形式             |                     | x               |             |
| 財務分析コード セット               |                     | x               |             |
| 財務分析コードの翻訳       |                     |                 | x           |
| 財務分析コード値の翻訳 |                     |                 | x           |
| 財務分析コード値             |                     |                 | x           |
| 財務分析コード                   |                     | x               |             |
| 会計カレンダー期間                 |                     | x               |             |
| 会計カレンダー                        |                     | x               |             |
| 主勘定カテゴリ                | x                   |                 |             |
| 主勘定                           | x                   |                 |             |
| 番号順序コード                   |                     | x               |             |
| 番号順序グループ                  |                     |                 | x           |
| 番号順序の参照             |                     | x               |             |

### <a name="025--gl"></a>025 - GL

|                                                  | スプレッドシートの内容 |                 |             |
|--------------------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**                           | **業務データ**   | **サンプル データ** | **データなし** |
| 自動トランザクションの勘定              | x                   |                 |             |
| 残高統制勘定                         |                     |                 | x           |
| カレンダー                                         |                     |                 | x           |
| 日付範囲                                   | x                   |                 |             |
| 既定の説明                             |                     | x               |             |
| 分析コード パラメーター                             | x                   |                 |             |
| ドキュメント タイプ                                   | x                   |                 |             |
| 財務分析コード値法人手数料 |                     |                 | x           |
| 財務理由                                | x                   |                 |             |
| 仕訳帳の説明                             | x                   |                 |             |
| 仕訳帳名                                    | x                   |                 |             |
| 元帳配賦基準の入力元                   |                     |                 | x           |
| 元帳配賦基準                          |                     |                 | x           |
| 元帳配賦ルールの出力先               |                     |                 | x           |
| 元帳配賦ルールの入力元                    |                     |                 | x           |
| 元帳配賦ルール                           |                     |                 | x           |
| 元帳の会計カレンダー期間                    |                     | x               |             |
| 元帳の会計暦年                      |                     | x               |             |
| 元帳パラメーター                                | x                   |                 |             |
| Ledger                                           |                     | x               |             |
| 主勘定法人の上書き              |                     |                 | x           |
| 組織の電子メール テンプレート メッセージ              |                     |                 | x           |
| 組織の電子メール テンプレート                      |                     |                 | x           |
| 補助元帳仕訳転送ルール                  | x                   |                 |             |
| ワークフロー組織パラメーター                 |                     |                 | x           |
| 作業時間                                    |                     |                 | x           |

### <a name="100--bank"></a>100 - 銀行

|                                                   | スプレッドシートの内容 |                 |             |
|---------------------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**                            | **業務データ**   | **サンプル データ** | **データなし** |
| 銀行口座                                     |                     | x               |             |
| 銀行融資のグループ                              |                     |                 | x           |
| 銀行融資タイプ                               |                     |                 | x           |
| 銀行グループ                                       |                     | x               |             |
| 銀行パラメーター                                   | x                   |                 |             |
| 銀行転記プロファイル                             |                     |                 | x           |
| 一般仕訳帳の口座取引明細書のインポート方法 |                     |                 | x           |
| 銀行トランザクション グループ                           | x                   |                 |             |
| 銀行トランザクション タイプ                             | x                   |                 |             |
| レイアウトの確認                                      |                     | x               |             |
| 顧客請求金額グループ                            |                     |                 | x           |
| 支払目的コード                             |                     |                 | x           |
| 調整照合ルール セット                 |                     |                 | x           |
| 調整照合ルール                     |                     |                 | x           |
| 取引コードのマッピング                          |                     |                 | x           |

### <a name="120--ap"></a>120 - AP

|                                             | スプレッドシートの内容 |                 |             |
|---------------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**                      | **業務データ**   | **サンプル データ** | **データなし** |
| エイジング期間の定義                    |                     |                 | x           |
| 業務区分                           |                     |                 | x           |
| 業務サブ区分                        |                     |                 | x           |
| 購入担当グループ                                |                     |                 | x           |
| 現金割引                               |                     |                 | x           |
| 配送の諸費用グループ                     |                     |                 | x           |
| 出荷先コード                            |                     |                 | x           |
| 急送コード                              |                     |                 | x           |
| 品目請求金額グループ                          |                     |                 | x           |
| 行割引仕入先グループ                 |                     |                 | x           |
| 業種                            |                     | x               |             |
| 荷渡方法                           |                     |                 | x           |
| 複数行割引仕入先グループ            |                     |                 | x           |
| 支払カレンダー ルール                       |                     |                 | x           |
| 支払カレンダー                            |                     |                 | x           |
| 支払期日明細行                           |                     | x               |             |
| 支払スケジュール行                      |                     | x               |             |
| 支払スケジュール                            |                     | x               |             |
| 価格仕入先グループ                         |                     |                 | x           |
| 調達請求コード                    |                     |                 | x           |
| 製品カテゴリ                          |                     |                 | x           |
| 製品カテゴリ階層                |                     |                 | x           |
| 製品カテゴリ階層ロール            |                     |                 | x           |
| 製品カテゴリ階層の翻訳     |                     |                 | x           |
| 購買管理グループ                              |                     |                 | x           |
| 消費税グループ                            |                     |                 | x           |
| 配送条件                           |                     |                 | x           |
| 支払条件                            | x                   |                 |             |
| 割引合計仕入先グループ                |                     |                 | x           |
| 仕入先の銀行口座                        |                     |                 | x           |
| 仕入先の諸費用グループ                        |                     |                 | x           |
| 仕入先例外グループ                     |                     |                 | x           |
| 仕入先グループ                               |                     |                 | x           |
| "仕入先請求書" フォーム印刷構成 |                     |                 | x           |
| 仕入先請求ポリシー ルール タイプ            |                     |                 | x           |
| 仕入先の勘定科目                      | x                   |                 |             |
| 仕入先パラメーター                           | x                   |                 |             |
| 仕入先支払手数料                          |                     |                 | x           |
| 仕入先支払形式                       |                     |                 | x           |
| 仕入先支払方法の詳細         |                     |                 | x           |
| 仕入先支払方法                       |                     | x               |             |
| 仕入先転記プロファイル                      | x                   |                 |             |
| 仕入先価格許容範囲グループ               |                     |                 | x           |
| 仕入先の理由                              | x                   |                 |             |
| 仕入先、フォーム パラメーター                     |                     |                 | x           |
| 仕入先                                     |                     |                 | x           |

### <a name="130--tax"></a>130 - Tax

|                                    | スプレッドシートの内容 |                 |             |
|------------------------------------|---------------------|-----------------|-------------|
| **エンティティ スプレッドシート**             | **業務データ**   | **サンプル データ** | **データなし** |
| 消費税所轄官庁              |                     | x               |             |
| 消費税コードの上限              |                     |                 | x           |
| 消費税コードの値              |                     | x               |             |
| 消費税コード                    |                     | x               |             |
| 消費税非課税コード              | x                   |                 |             |
| 消費税非課税番号           |                     |                 | x           |
| 消費税グループの詳細            |                     | x               |             |
| 消費税グループ                   |                     | x               |             |
| 消費税品目グループ              |                     | x               |             |
| 消費税元帳転記グループ    | x                   |                 |             |
| 消費税パラメーターの事前設定エンティティ |                     |                 | x           |
| 消費税パラメーター               | x                   |                 |             |
| 消費税期間の設定             |                     | x               |             |
| 消費税レポート コード          |                     |                 | x           |
| トランザクション コード                  |                     |                 | x           |
| 源泉徴収税コードの値        |                     | x               |             |
| 源泉徴収税コード              |                     | x               |             |
| 源泉徴収税グループの詳細      |                     |                 | x           |
| 源泉徴収税グループ             |                     | x               |             |
| 源泉徴収税の上限             |                     |                 | x           |

### <a name="140--ar"></a>140 - AR

|                                                         |      スプレッドシートの内容       |                              |                          |
|---------------------------------------------------------|--------------------------------|------------------------------|--------------------------|
|           <strong>エンティティ スプレッドシート</strong>           | <strong>業務データ</strong> | <strong>サンプル データ</strong> | <strong>データなし</strong> |
|                エイジング期間の定義                 |               x                |                              |                          |
|                    業務区分                    |                                |                              |            x             |
|                  業務サブ区分                   |                                |                              |            x             |
|                      現金割引                      |                                |                              |            x             |
|     "督促状" フォーム印刷構成      |                                |                              |            x             |
|                 督促状の設定                 |               x                |                              |                          |
|                 手数料計算                  |                                |                              |            x             |
|                コミッション顧客グループ                |                                |                              |            x             |
|                  コミッション品目グループ                  |                                |                              |            x             |
|                 コミッション売上グループ                  |                                |                              |            x             |
| "顧客勘定明細書" フォーム印刷構成 |                                |                              |            x             |
|                 顧客の銀行口座                  |                                |                              |            x             |
|                 顧客請求金額グループ                  |                                |                              |            x             |
|                  顧客の定義                   |                                |                              |            x             |
|                    顧客の詳細                     |                                |                              |            x             |
|      "顧客フェーシング" フォーム印刷構成       |                                |                              |            x             |
|                     顧客グループ                     |                                |              x               |                          |
|                顧客の勘定科目                 |               x                |                              |                          |
|                   顧客パラメーター                   |               x                |                              |                          |
|                  顧客支払手数料                   |                                |                              |            x             |
|          顧客支払方法の詳細          |                                |                              |            x             |
|                 顧客支払方法                 |                                |              x               |                          |
|                顧客転記プロファイル                |               x                |                              |                          |
|                    顧客の理由                     |                                |                              |            x             |
|             顧客損金処理理由コード             |               x                |                              |                          |
|                        顧客                        |                                |                              |            x             |
|                 配送の諸費用グループ                 |                                |                              |            x             |
|                     急送コード                      |                                |                              |            x             |
|     "自由書式の請求書" フォーム印刷構成      |                                |                              |            x             |
|                利息コードと手数料                 |                                |                              |            x             |
|               利息コードと範囲                |                                |                              |            x             |
|                     利息コード                      |               x                |                              |                          |
|       "利子計算書" フォーム印刷構成        |                                |                              |            x             |
|                   品目請求金額グループ                    |                                |                              |            x             |
|              行割引顧客グループ              |                                |                              |            x             |
|                    業種                     |                                |                              |            x             |
|                    荷渡方法                    |                                |                              |            x             |
|                    支払カレンダー                     |                                |                              |            x             |
|                    支払期日明細行                    |                                |                              |            x             |
|                 支払スケジュール行                  |                                |                              |            x             |
|                    支払スケジュール                     |                                |                              |            x             |
|                  価格顧客グループ                  |                                |                              |            x             |
|                   印刷済フォームのメモ                    |                                |                              |            x             |
|                   売上諸掛コード                    |                                |                              |            x             |
|                     販売地域                     |                                |                              |            x             |
|                    販売注文プール                    |                                |                              |            x             |
|                    統計グループ                     |                                |                              |            x             |
|                    配送条件                    |                                |                              |            x             |
|                    支払条件                     |                                |                              |            x             |
|             割引合計顧客グループ              |                                |                              |            x             |


