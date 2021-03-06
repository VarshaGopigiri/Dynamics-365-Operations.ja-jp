---
title: "フィールドのカスタマイズのヘルプ"
description: "この記事では、既存のフィールドの説明をカスタマイズし、独自の説明を追加する方法について説明します。"
author: YuyuScheller
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 
audience: Developer
ms.reviewer: rschloma
ms.search.scope: Operations
ms.custom: 92013
ms.assetid: 94d555d7-28f3-4d94-91b4-6038e2be5047
ms.search.region: Global
ms.author: yuyus
ms.search.validFrom: 2016-05-31
ms.dyn365.ops.version: AX 7.0.1
ms.translationtype: HT
ms.sourcegitcommit: 879eb9f2a63a8514791f74965005ed3e22bc0de7
ms.openlocfilehash: 397a563c8882ed68f49f27d06af0d3f810bf87ab
ms.contentlocale: ja-jp
ms.lasthandoff: 04/20/2018

---

# <a name="customize-field-help"></a>フィールドのカスタマイズのヘルプ

[!include [banner](../includes/banner.md)]

この記事では、既存のフィールドの説明をカスタマイズし、独自の説明を追加する方法について説明します。

より複雑なフィールドの説明がいくつかあります。 フィールド上に置くと、これらの説明が表示されます。 会社固有の情報を追加する場合などに、これらの説明をカスタマイズすることができます。 また、追加フィールドの説明を追加することもできます。 フィールドの説明を作成するには、フィールド コントロールの **HelpText** プロパティを使用します。 **HelpText** プロパティは、以前のバージョンのように、テーブル フィールドとデータ型に指定されなくなりました。 また、データ型とテーブル フィールドからフォーム コントロールへの **HelpText** プロパティの継承は廃止されました。 フィールドの説明は、他のコントロールおよびページで使用可能な情報のコンテキストである、個々のフィールドに対して固有のものです。 フィールドの説明を追加およびカスタマイズするには、開発環境へのアクセスが必要です。 その他のメタデータの変更と同様に、Operations の新しいバージョンがリリースされるとき、新しい説明は上書きされるを防ぐために新しいモデルに追加する必要があります。 詳細については、[カスタマイズ: オーバーレイおよび拡張機能](../extensibility/customization-overlayering-extensions.md) を参照してください。

## <a name="customize-a-field-description-or-add-a-new-description"></a>フィールドの説明をカスタマイズするか、新しい説明を追加する
同じ手順を使用して、既存のフィールド記述をカスタマイズし、新しいフィールド記述を追加します。 ただし、既存の説明をカスタマイズする場合に、既存のラベルの参照を置き換えます。

1.  アプリケーション エクスプローラーで、関連するページ (フォーム) を検索し、プロジェクトに追加します。
2.  ページのノードで、関連するフィールド コントロールを探します。 ラベル ID の一部として使用することができるように、名前をメモしておきます。
3.  説明の新しいラベルを追加します。 Microsoft が使用する規則に従い、フィールドの説明のためのラベル ファイルに名前を付け、ラベル ファイル ID を作成することができます。 詳細については、次のセクションを参照してください。
4.  フィールド制御の **HelpText** プロパティで、ラベルへの参照を追加します。

## <a name="label-file-names-and-label-ids"></a>ラベル ファイル名とラベル ID
Microsoft が提供するフィールドの説明は、別のラベル ファイルに格納されています。 モデルごとのモジュールごとに 1 つのラベル ファイルがあります。 ラベル ファイル名のパターンは、FieldDescriptions\_*ModuleName*\_*ModelName*.*CountryCode*.label.txt です。 次にいくつか例を挙げます。

-   FieldDescriptions\_AccountsPayable\_ApplicationFoundation.en-US.label.txt
-   FieldDescriptions\_SystemAdministration\_ApplicationFoundation\_en-US.txt

ラベル ID のパターンは @FieldDescriptions\_*ModuleName:PageName*\_*ControlName* です。 次にいくつか例を挙げます。

- @FieldDescriptions\_AccountsPayable:CustSettlement\_CustSettlement\_OffsetCompany は、<strong>顧客決済</strong>ページ (CustSettlement) の<strong>会社コード</strong>フィールド (CustSettlement\_OffsetCompany) のラベルの ID です。
- @FieldDescriptions\_ProcurementAndSourcing:PurchLineBackOrder\_LinkViewCheckBox は、 <strong>受注残購買明細行</strong>ページ (PurchLineBackOrder) <strong>変更ビューのリンク</strong>オプション (LinkViewCheckBox) のラベルの ID です。


<a name="additional-resources"></a>その他のリソース
--------

[クライアントでローカライズ可能なラベルを作成する](create-localizable-labels-client.md)

[フィールド説明の表示およびエクスポート](../../fin-and-ops/get-started/view-export-field-descriptions.md)




