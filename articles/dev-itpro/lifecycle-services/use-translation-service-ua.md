---
title: "Microsoft Dynamics 365 翻訳サービス - ドキュメント ファイルの翻訳"
description: "このトピックでは、Microsoft Dynamics 製品またはソリューションのドキュメント ファイルを翻訳する方法について説明します。"
author: kfend
manager: AnnBe
ms.date: 03/29/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer, IT Pro
ms.reviewer: kfend
ms.search.scope: Operations
ms.custom: 6154
ms.assetid: 
ms.search.region: Global
ms.author: ejchoGIT
ms.search.validFrom: 2018-03-27
ms.dyn365.ops.version: AX 7.3.0
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: addcca4f3b21f4a8a8d8526f4ec621e9759874e3
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="microsoft-dynamics-365-translation-service---documentation-file-translation"></a>Microsoft Dynamics 365 翻訳サービス - ドキュメント ファイルの翻訳

[!include [banner](../includes/banner.md)]

このトピックでは、Microsoft Dynamics 製品およびソリューションのドキュメント ファイルを翻訳する方法について説明します。

## <a name="create-a-translation-request"></a>翻訳要求を作成する
1. Microsoft Dynamics Lifecycle Services (LCS) で、DTS ダッシュボードの**追加**を選択して新しい翻訳要求を作成します。

    ![追加ボタン](./media/dts-request1.png "追加ボタン")

    LCS ホーム ページから、またはプロジェクト内から、DTS ダッシュ ボードを開くことができます。 詳細については、[DTS にアクセス](./translation-service-overview.md#accessing-dts) を参照してください。

2. 要求ための必要な情報を入力します。

    | フィールド | 説明 |
    |-------|-------------|
    | 要求名 | 要求名を入力します。 |
    | ファイル タイプ | **ドキュメント** を選択します。 このオプションは、LCS の**Dynamics 365 翻訳サービス - ドキュメント翻訳サポート**プレビュー機能をオンにした場合にのみ使用できます。 詳細については、[LCS プレビュー機能へのアクセス](./translation-service-overview.md#accessing-lcs-preview-features) を参照してください。 |
    | 製品名 | 製品名を選択します。 LCS プロジェクト内から DTS にアクセスする場合、このフィールドは自動的に入力され、読み取り専用です。 |
    | 製品バージョン | 製品バージョンを選択します。 LCS プロジェクト内から DTS にアクセスする場合、このフィールドではプロジェクトからの既定の製品バージョン情報を表示されます。 ただし、別のバージョンを選択できます。 |
    | ターゲットの国/地域 | 翻訳したファイルをリリースする国または地域を選択します。 |
    | 翻訳元言語、翻訳先言語 | 翻訳対象の言語の組み合わせを選択します。 このフィールドには、選択した製品名とバージョンでサポートされているすべての言語がサポートされています。 **太字**タイプで表示される言語名は、Microsoft Dynamics の製品の一般提供 (GA) 言語です。 したがって、Microsoft で訓練された機械翻訳 (MT) システムは、これらの言語で使用できます。 つまり、MT システムは Microsoft Dynamics の用語でトレーニングされます。 GA 言語以外の場合、MT システムは一般的なドメイン トレーニングを使用します。 |

    > [!NOTE]
    > Microsoft のトレーニングを受けた Microsoft Dynamics 言語資産の MT システムを利用するには、ソース言語またはターゲット言語として **English – United States** を選択する必要があります。 次に例を示します。
    >
    > | 翻訳のソース言語 | 翻訳のターゲット言語 | 使用される MT システム |
    > |-----------------------------|-----------------------------|------------------------|
    > | 英語 – 米国 | 日本語 | Microsoft によるトレーニングされた MT システム |
    > | 日本語 | 英語 – 米国 | Microsoft によるトレーニングされた MT システム |
    > | ドイツ語 | 日本語 | 一般的な MT システムには、ユーザーが XML ローカライズ交換ファイル形式 (XLIFF) を使用する翻訳メモリ (TM) を提供しない限り、10,000 を超える翻訳単位 (TU) があります。 |

3. **作成** を選択します。

## <a name="upload-files"></a>ファイルのアップロード
各セクションでプラス記号 (**+**) を選択し、**ファイルのアップロード** ページを開きます。

### <a name="upload-the-files-to-translate-required"></a>翻訳するファイルをアップロードする (必須)
現在、Microsoft Word (.docx) 形式のファイルのみが翻訳に使用することができます。 変換するすべての .docx ファイルを含む ZIP ファイルを作成します。 zip ファイルは 1 つのみアップロードすることができます。

### <a name="upload-xliff-or-tmx-tm-files-optional"></a>XLIFF または TMX TM ファイル (オプション) のアップロード
以前の DTS リクエストからの Translation Memory eXchange (TMX) 形式の TM を使用している場合、または UI ファイル変換の XLIFF TM を使用している場合、これらの TM が、再提出する新しいドキュメントにリサイクルできるようにするために、これらの TM を添付できます。 すべての TM ファイルを含む ZIP ファイルを作成します。 zip ファイルは 1 つのみアップロードすることができます。

ファイルのアップロードが終了したら、**送信**を選択して翻訳プロセスを開始します。 要求を送信すると、新しい要求 ID が DTS ダッシュ ボードに作成されます。 要求 ID を選択し、要求の詳細ページで **依頼状況** タブを選択して、依頼の概要とそのステータスを表示します。

![ステータス タブの要求](./media/dts-request-status-ua.png "ステータス タブの要求")

処理時間は、DTS キューに入っている要求の数と、送信するソース ファイルの文字数に依存することに注意してください。

## <a name="after-translation-is-completed"></a>翻訳の完了後
翻訳要求の処理が完了すると、DTS から電子メール通知を受信します。 結果を要求詳細ページの **要求の出力** タブ上に表示することができます。

![出力タブの要求](./media/dts-output-ua.png "出力タブの要求")

文書翻訳の要求では、翻訳プロセスが完了した後、出力ファイルの 3 つのタイプが使用できます。

+ **翻訳レビュー対象ファイル** – このファイルをダウンロードすると、翻訳されたドキュメント文字列をテーブル ビューで確認および編集できます。 ファイルには、ソースとターゲットの言語セグメントが並べて表示されます。
+ **ソース形式で翻訳されたファイル** – 翻訳を編集または確認する予定がない場合は、このファイルをダウンロードしてください。 このファイルには、送信したソース .docx ファイルと同じ書式設定の書式 (タイトル、ヘッダー、テーブルなど) があり、すぐに使用できます。
+ **翻訳メモリ** – 次に元の文書の新しいバージョンを使用する翻訳要求を送信するときにこれらの翻訳をリサイクルするには、このファイルをダウンロードしてください。

### <a name="review-and-edit-the-translations"></a>翻訳を確認および編集
DTS は .docx 形式の翻訳レビュー ファイルを提供します。 要求の詳細ページの **要求の出力** タブからファイルをダウンロードして、Word で開くことができます。 ファイルは、次の図に示すように、便利なテーブルビューを提供します。 したがって、ソース言語とターゲット言語のテキストを簡単に比較することができます。 ファイルを確認した後は、ファイルを保存し DTS にアップロードして、送信した元の書式スタイルで更新された .docx ファイルの出力を生成します。

![確認用の .docx ファイル](./media/dts-doc-review.png "翻訳レビュー対象 .docx ファイル")
 
.docx レビュー ファイルを編集するときは、次のガイドラインに注意してください。

+ **ターゲット セグメント**列のテキストのみを編集します。
+ 追加または行を削除しないでください。
+ 行または列の順序を変更しないでください。
+ 追加または赤色のタグを削除しないでください。 ほとんどの赤いタグは、書式設定およびスタイルを表します。
+ 赤いタグを移動する必要がある場合は、開始タグ (たとえば、**\<116\>**) とその終了タグ (**\<116/\>**) を切り替えないように注意します。

### <a name="regenerate-output-files"></a>出力ファイルの再生成
.docx レビュー ファイルのレビューと編集が完了したら、出力ファイルをソース ドキュメント形式で再生成する必要があります。 最新の翻訳 (つまり、ユーザーが編集したバージョンの翻訳) をターゲット言語でドキュメント ファイルに適用することができます。

1. **要求の出力**タブで、**再生成**を選択します。 **再生成 (パートナーによる)** という名前の新しいタブが表示されます。
2. プラス記号 (**+**) を選択し、**ファイルのアップロード** ページを開きます。
3. 編集後の XLIFF ファイルを zip 圧縮してから、**アップロード** を選択します。 **要求の出力**タブの .docx レビュー ファイルに DTS が提供した名前を変更しないでください。
3. アップロード アクションを確認するように求められます。 DTS は、更新された .docx ファイルをソース ドキュメント スタイルで再生成します。 このプロセスには少し時間がかかることがあります。 それが完了したとき、自動電子メール通知を受け取ります。 最終出力ファイルを **再生成 (パートナーによる)** タブ上にダウンロードすることができます。

    ![再生成された出力](./media/dts-regenerate-output-ua.png "再生成された出力")

必要に応じて何度でも再生成プロセスを繰り返すことができます。

Microsoft Dynamics 365 翻訳サービス (DTS) に関する詳細については、[Microsoft Dynamics 365 - 翻訳サービスの概要](./translation-service-overview.md) を参照してください。 ユーザー インターフェイス (UI) ファイルを翻訳する方法については、[Microsoft Dynamics 365 翻訳サービス ユーザー ガイド - ユーザー インターフェイス ファイルの翻訳](./use-translation-service.md) を参照してください。

