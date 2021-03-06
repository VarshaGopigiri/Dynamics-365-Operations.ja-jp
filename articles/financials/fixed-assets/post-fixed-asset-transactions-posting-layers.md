---
title: "転記階層への固定資産トランザクションを転記する"
description: "この記事は、固定資産トランザクションの転記階層機能の概要を示します。"
author: twheeloc
manager: AnnBe
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
ms.search.form: AssetBookTable, LedgerJournalTransAsset
audience: Application User
ms.reviewer: twheeloc
ms.search.scope: Core, Operations
ms.custom: 3001
ms.assetid: 7dabde57-0843-47c3-85ef-f36b6f472e30
ms.search.region: Global
ms.author: saraschi
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.translationtype: HT
ms.sourcegitcommit: 2771a31b5a4d418a27de0ebe1945d1fed2d8d6d6
ms.openlocfilehash: b210bddf640dff2d65e2aec63a18c27acebdc5a8
ms.contentlocale: ja-jp
ms.lasthandoff: 11/03/2017

---

# <a name="post-fixed-asset-transactions-to-posting-layers"></a>転記階層への固定資産トランザクションを転記する

[!include [banner](../includes/banner.md)]

この記事は、固定資産トランザクションの転記階層機能の概要を示します。

固定資産の減価償却は多くの場合、目的に応じて異なる方法で行われます。 税申告用の減価償却は、税引前の減価償却が可能な限り最大になるように現在の税制を使用して計算されますが、報告のための減価償却は、会計法および標準に従って計算されます。 さまざまな種類の減価償却が計算されて、それぞれ異なる転記階層に記録されます。

固定資産に関連付けられる各帳簿は、全体的な減価償却の目的を持つ特定の転記階層に対して設定されます。 次の 10 の転記階層があります。現在、操作、税金、および 7 つのカスタム階層。 [総勘定元帳への転記] フィールドを [いいえ] に設定すると、帳簿の総勘定元帳への転記を無効にすることもできます。 [転記階層] フィールドが [なし] に自動的に設定されます。 通常、総勘定元帳に転記しない帳簿は、税務報告のために使用されます。 この方法によって資産帳簿の履歴トランザクションが総勘定元帳にコミットされなかったため、さらに柔軟に削除を行えます。

固定資産仕訳帳は、[総勘定元帳]、[仕訳帳の設定]、[仕訳帳名] の順に表示して、[仕訳帳名] ページを使用して定義できます。 減価償却を転記できる各仕訳帳は、単独の転記階層に対して仕訳帳名で定義されます。 仕訳帳の転記階層は変更できません。 この制限は、各転記階層のトランザクションが分離しておくのを保証するのに役立ちます。 個々の転記階層には、仕訳帳名を少なくとも 1 つ作成する必要があります。 総勘定元帳に転記しない帳簿を使用している場合は、転記階層が [なし] に設定されている仕訳帳を作成する必要もあります。

[固定資産転記プロファイル] ページで、固定資産トランザクションのための勘定科目を指定できます。 各転記プロファイルに対して、関連するトランザクション タイプと帳簿を選択してから、勘定科目を指定する必要があります。 総勘定元帳に転記する各帳簿の転記プロファイルのレコードを設定します。

> [!NOTE] 
> 派生帳簿を使用することによって、複数の転記階層にトランザクションを同時に転記することができます。 帳簿の転記階層に対応する転記階層の仕訳帳で、基本帳簿のトランザクションを作成します。 転記の際には、派生帳簿のトランザクションが、適切な転記階層に転記されます。

詳細については、「[派生帳簿](derived-books.md)」および「[派生帳簿による転記](post-derived-value-models.md)」を参照してください。




