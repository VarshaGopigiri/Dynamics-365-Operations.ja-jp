---
title: "財務分析コード"
description: "このトピックは、財務分析コードのさまざまなタイプと設定方法を説明します。"
author: aprilolson
manager: AnnBe
ms.date: 08/01/2017
ms.topic: article
ems.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: DimensionDetails, DimensionValueDetails, SysTranslationDetail
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Core, AX 7.0.0, Operations, UnifiedOperations
ms.custom: 25871
ms.search.region: Global
ms.author: aolson
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: c4f5dae90c5fcaaa52a7087d7c20b2de343b7da0
ms.openlocfilehash: b5615a6d9003554593981ce65be0283a249a7d93
ms.contentlocale: ja-jp
ms.lasthandoff: 08/01/2017

---

# <a name="financial-dimensions"></a>財務分析コード

[!include[banner](../includes/banner.md)]

このトピックは、財務分析コードのさまざまなタイプと設定方法を説明します。

共有勘定科目表の勘定の区分として使用する財務分析コードを作成するには、**財務分析コード**ページを使用します。 財務分析コードには、カスタム分析コードと、エンティティがサポートしている財務分析コードの 2 つのタイプがあります。 カスタム分析コードは法人間で共有され、値はユーザーにより入力され管理されます。 エンティティがサポートしている分析コードのために、[顧客] や [店舗] エンティティなどシステムの他の場所で値が定義されます。 エンティティがサポートしている分析コードには、法人間で共有されるものや、会社固有のものがあります。 

財務分析コードを作成した後、[**財務分析コード値**] ページを使用して、各財務分析コードに追加のプロパティを割り当てます。 

財務分析コードを使用して、法人を表すことができます。 Microsoft Dynamics 365 for Finance および Operations、Enterprise Edition では、法人を作成する必要はありません。 ただし、財務分析コードは、法人の運営や業務上の要件に対処するようには設計されていません。 Finance および Operations の単位間会計機能は、各トランザクションによって作成された勘定項目のみ対処するように設計されています。 

法人として財務分析コードを設定する前に、次の分野の業務プロセスを評価し、この設定が組織で使用できるかどうかを判断します:

- 棚卸資産
- 財務分析コードと法人間の販売および購買
- 売上税の計算および報告
- 業務レポート

次に、いくつか制限を示します。

- 法人でのみ売上税機能を使用できます。財務分析コードでは使用できません。
- 一部のレポートには、財務分析コードが含まれていません。 したがって、財務分析コードによるレポートは、レポートの修正が必要な場合があります。

## <a name="custom-dimensions"></a>カスタム分析コード

ユーザー定義の財務分析コードを作成するには、[**値の使用元**] フィールドで**&lt;カスタム分析コード&gt;**を選択します。 また主勘定マスクを指定して、分析コード値に対して入力できる情報の量やタイプを制限することもできます。 文字またはハイフン (-) など、各分析コード値の変化しない文字を入力できます。 また、分析コード値が作成されるたびに変更される、番号と文字のプレースホルダーとなる番号記号 (\#) とアンパサンド (&) を入力できます。 番号のプレースホルダーとして番号記号 (\#)、文字のプレースホルダーとしてアンパサンド (&) を使用します。 マスクの書式設定のためのフィールドは、[**値の使用元**] フィールドで**&lt;カスタム分析コード&gt;**を選択した場合にのみ使用できます。

**例**

分析コード値を文字 2 桁 (CC)、番号 3 桁に制限するには、マスクの書式設定として **CC-\#\#\#** を入力します。

## <a name="entity-backed-dimensions"></a>エンティティがサポートする分析コード

エンティティがサポートする分析コードを作成するには、[**値の使用元**] フィールドで、財務分析コードの基になるシステム定義エンティティを選択します。 財務分析コード値がそのエンティティから作成されます。 たとえば、プロジェクトの分析コード値を作成するには、[**プロジェクト**] を選択します。 各プロジェクト名に対して分析コード値が作成されます。 **財務分析コード値**ページには、エンティティの値が表示されます。 それらの値が会社固有のものである場合、そのページでは会社も表示されます。

## <a name="activating-dimensions"></a>分析コードの有効化

財務分析コードを有効にすると、財務分析コードの名前が含まれるようテーブルが更新されます。 削除された分析コードは削除されます。 財務分析コードを有効にする前に、分析コード値を入力することができます。 ただし、財務分析コードは有効化されていないと消費できません。 たとえば、財務分析コードが有効化される前に、勘定構造に財務分析コードを追加することはできません。 **有効化**をクリックすると、すべての分析コードが更新され、ステータスの変更を表示します。 

## <a name="translations"></a>翻訳

[**テキスト翻訳**] ページでは、様々な言語で、選択した財務分析コードのテキストを入力することができます。 [**主勘定翻訳**] ページでは、様々な言語で、主勘定のテキストを入力することができます。 

## <a name="legal-entity-overrides"></a>法人の上書き

分析コードには、ある法人に対して有効でないものもあります。 また、一部の分析コードは、特定の期間にだけ有効な場合があります。 これらのケースでは、[**法人の上書き**] セクションを使用して、分析コードを保留にする法人の指定、法人のオーナーの指定、分析コードの有効期間の指定ができます。

## <a name="deleting-financial-dimensions"></a>削除中の財務分析コード

データの整合性を維持するために財務分析コードを削除されることはほとんどありません。 財務分析コードを削除しようとする場合は、次の基準が評価されます。

- 財務分析コードが転記済または未転記のトランザクションで使用されている、もしくは任意の分析コード値の組み合わせであるか。
- 財務分析コードは有効な勘定構造、詳細なルール構造、もしくは財務分析コードセットで使用されているか。
- 財務分析コードは、既定の財務分析コードの統合形式の一部であるか。
- 財務分析コードは既定の分析コードとして設定されているか。

条件が合致した場合は、財務分析コードを削除することはできません。


詳細については、次のトピックを参照してください。
- [財務分析コードの定義](tasks/define-financial-dimensions.md)
- [財務分析コード用の既定テンプレートの管理](tasks/maintain-financial-dimension-default-templates.md)
