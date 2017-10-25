---
title: "POS での製品検索および顧客検索"
description: "このトピックでは、Dynamics 365 for Retail の製品および顧客検索機能に加えられた改良の概要を示します。"
author: shalabhjain
manager: AnnBe
ms.date: 08/16/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 
audience: Application user
ms.search.scope: Operations, Retail
ms.custom: 141393
ms.assetid: 
ms.search.region: Global
ms.search.industry: Retail
ms.author: shajain
ms.search.validFrom: 2017-06-30
ms.dyn365.ops.version: Retail April 2017 update
ms.translationtype: HT
ms.sourcegitcommit: 7e0a5d044133b917a3eb9386773205218e5c1b40
ms.openlocfilehash: 66859535ee118ffc04a847dfe6e8e0bae1cd9d6c
ms.contentlocale: ja-jp
ms.lasthandoff: 09/29/2017

---

# <a name="overview-of-product-and-customer-search-in-point-of-sale"></a>販売時点管理での製品および顧客検索の概要

Modern 販売時点管理 (MPOS) およびクラウド販売時点管理 (CPOS) は、店舗の従業員がすばやく製品および顧客の検索ができるよう、使いやすい検索機能を提供します。 検索バーは、従業員がすばやく製品および顧客を検索できるよう、常に MPOS および CPOS の上部に表示されています。

従業員は、現在の店舗に関連付けられている品揃えとカタログ、および会社内の他のどの店舗に関連付けられている品揃えとカタログで製品を検索できます。 したがって、レジ担当者は、店舗の品揃え外製品でも販売および返品をすることができます。 同様に、従業員は、現在の店舗または会社内の他のどの店舗に関連付けられている顧客でも検索できます。 また、従業員は、親組織内の別の会社に関連付けられている顧客も検索できます。

## <a name="product-search"></a>製品検索 

既定では、商品検索は、店舗の品揃えで実行します。 このタイプの検索は、[*ローカル製品検索*] と呼ばれます。 ただし、従業員は、現在の店舗に関連付けられている任意のカタログへ容易に切り替えることができ、または別の店舗で検索することができます。 このタイプの検索は、[*リモート製品検索*] と呼ばれます。 カタログを変更するには、ページの左側にある [**カテゴリ**] ボタンを選択します。 表示されるウィンドウの上部で [**カタログを変更**] ボタンを選択し、参照するのには使用可能なカタログのいずれかを選択します。 システムは、選択した製品のカタログを検索します。

[**カタログの変更**] ページで、従業員が任意の店舗を容易に選択し、またはすべての店舗間で製品を検索することができます。

![カタログを変更します](./media/Changecatalog.png "カタログを変更します")
 
ローカル商品検索は、次の製品プロパティ内で検索します。

- 製品番号
- 製品名
- 説明
- 分析コード
- バーコード
- 検索名

### <a name="enhancements-to-local-product-searches"></a>ローカル商品検索の機能拡張

ローカル商品検索の体験がよりわかりやすくなりました。 次の機能が拡張されています:

- 従業員が検索を実行する前に [**製品**] または [**顧客**] のいずれかを選択できるように、製品および顧客のドロップダウン メニューが検索バーに追加されました。 既定では、[**製品**] が選択されている場合は、次の図のようになります。
- 複数キーワード検索 (検索条件を使用して検索) では、小売業者は、任意の検索条件に一致するまたはすべての検索条件に一致する結果のみを含む検索結果かどうかをコンフィギュレーションできます。 この設定は、[**製品検索**] という名前の新しいグループの下で、POS 機能プロファイルで使用できます。 既定の設定は [**任意の検索条件に一致**] です。 この設定は、推奨される設定でもあります。 [**任意の検索条件に一致**] 設定が使用される場合、結果として完全または部分的に 1 つまたは複数の検索条件に一致するすべての製品が返され、その結果は自動的に最もキーワードの一致 (完全または部分的) がある製品の昇順で並べ替えられます。

    [**すべての検索条件に一致**] 設定は、すべての検索条件 (全体または一部) と一致する製品のみを返します。 この設定は、製品名が長くなる場合、および従業員が検索結果で限定されるた製品のみを表示したいときに役に立ちます。 ただし、このタイプの検索には、2 つの制限があります。

    - 個々の製品プロパティに対して検索が行われます。 たとえば、少なくとも 1 つの製品のプロパティに対して、すべての検索キーワードがある製品のみが返されます。
    - 分析コードは検索されません。

- 小売業者は、ユーザーが製品名を入力すると検索候補を表示する製品検索をコンフィギュレーションできるようになりました。 この機能の新しい設定は、[**製品検索**] という名前のグループの下で、POS 機能プロファイルで使用できます。 設定は [**入力中に検索提案を表示**] と呼ばれます。 この機能は、全体の名前を手動で入力する必要がないため、従業員が検索している製品をすばやく見つけるのに役立ちます。
- 製品検索アルゴリズムは、製品の [**検索名**] プロパティで検索された条件も検索するようになります。

![製品候補](./media/Productsuggestions.png "製品候補")

## <a name="customer-search"></a>顧客検索

顧客検索は、さまざまな目的で顧客を見つけるのに使用されます。 たとえば、レジ担当者は顧客の欲しい物リストまたは購入履歴を表示したり、またはトランザクションに顧客を追加するかもしれません。 複数キーワード検索の場合は、顧客検索アルゴリズムは、検索キーワードのいずれかに一致するすべての顧客を返します。 ただし、ほとんどのキーワードに一致する顧客は、結果の上部に表示されます。 この動作は、他の検索エンジンが結果を表示する方法と似ています。 最初に最も検索条件に一致する結果を表示し、それから検索キーワードに部分的に一致する結果を表示します。 この動作は、レジ担当者が検索に複数のキーワードを使用しているが、キーワードのいずれかにスペルの間違いがあるような状況で役に立ちます。

既定では、顧客検索は、店舗に関連付けられている顧客アドレス帳で実行されます。 このタイプの検索は、[*ローカル顧客検索*] と呼ばれます。 ただし、従業員は顧客をグローバルに検索することもできます。 つまり、会社の店舗間および他のすべての法人間を検索することができます。 このタイプの検索は、[*リモート顧客検索*] と呼ばれます。

グローバルに検索する場合、次の図に示すように、従業員はページの下部にある [**フィルター結果**] ボタンを選択でき、[**すべての店舗の検索**] オプションを選択できます。 この場合、顧客だけが返されるわけではありません。 本社で任意のアドレス帳の一部である関係者のすべてのタイプが返されます。 これらの関係者には、作業者、仕入先、連絡先、および競合他社が含まれます。

> [!NOTE]
> 結果が返されるリモート顧客検索用の最小 4 文字を入力する必要があります。

リモート顧客検索では、現在の会社でこれらの関係者用に顧客 ID が作成されていないため、他の法人からの顧客用に顧客 ID が表示されません。 ただし、従業員が顧客の詳細ページを開くと、システムは関係者の顧客 ID を自動的に生成し、また店舗の顧客アドレス帳を顧客に関連付けます。 したがって、後に行われるローカル店舗検索時には、顧客が表示されます。

![グローバル顧客検索](./media/Globalcustomersearch.png "グローバル顧客検索")

### <a name="enhancements-to-local-customer-searches"></a>ローカル顧客検索の機能拡張

ローカル顧客検索は、従業員が電話番号で顧客をすばやく見つけるのに役立ちます。 従業員は、スペース、ハイフン、かっこなどの顧客の電話番号に追加された任意の特殊文字を入力する必要はありません。 レジ担当者は任意の形式 (たとえば、かっこ、ハイフン、記号などを含めることができます) で電話番号を格納することができますが、部分的な電話番号を入力して顧客を検索できます。 レジ担当者が入力する電話番号に特殊文字が含まれた場合は、他のレジ担当者は、特殊文字の後に表示される番号を入力して、顧客を検索できます。 たとえば、入力された顧客の電話番号が [**123-456-7890**] の場合、レジ担当者は [**123**]、[**456**]、[**7890**]、または[**1234567890**]、または電話番号の最初のいくつかの番号を部分的に入力することで顧客を検索できます。
